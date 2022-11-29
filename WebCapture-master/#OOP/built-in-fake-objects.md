# Built-in Fake Objects

_Captured: 2017-08-03 at 07:20 from [www.yegor256.com](http://www.yegor256.com/2014/09/23/built-in-fake-objects.html)_

While mock objects are perfect instruments for unit testing, mocking through mock frameworks may turn your unit tests into an unmaintainable mess. Thanks to them we often hear that "mocking is bad" and "mocking is evil."

The root cause of this complexity is that our objects are too big. They have many methods and these methods return other objects, which also have methods. When we pass a mock version of such an object as a parameter, we should make sure that all of its methods return valid objects.

This leads to inevitable complexity, which turns unit tests to [waste](https://news.ycombinator.com/item?id=7353767) almost impossible to maintain.

Take the `Region` interface from [jcabi-dynamo](http://dynamo.jcabi.com) as an example (this snippet and all others in this article are simplified, for the sake of brevity):
    
    
    public interface Region {
      Table table(String name);
    }

Its `table()` method returns an instance of the `Table` interface, which has its own methods:
    
    
    public interface Table {
      Frame frame();
      Item put(Attributes attrs);
      Region region();
    }

Interface `Frame`, returned by the `frame()` method, also has its own methods. And so on. In order to create a properly mocked instance of interface `Region`, one would normally create a dozen other mock objects. With [Mockito](http://mockito.org) it will look like this:
    
    
    public void testMe() {
      // many more lines here...
      Frame frame = Mockito.mock(Frame.class);
      Mockito.doReturn(...).when(frame).iterator();
      Table table = Mockito.mock(Table.class);
      Mockito.doReturn(frame).when(table).frame();
      Region region = Mockito.mock(Region.class);
      Mockito.doReturn(table).when(region).table(Mockito.anyString());
    }

And all of this is just a [scaffolding](http://www.yegor256.com/2015/05/25/unit-test-scaffolding.html) before the actual testing.

Let's say, you're developing a project that uses jcabi-dynamo for managing data in [DynamoDB](https://aws.amazon.com/dynamodb/). Your class may look similar to this:
    
    
    public class Employee {
      private final String name;
      private final Region region;
      public Employee(String empl, Region dynamo) {
        this.name = empl;
        this.region = dynamo;
      }
      public Integer salary() {
        return Integer.parseInt(
          this.region
            .table("employees")
            .frame()
            .where("name", this.name)
            .iterator()
            .next()
            .get("salary")
            .getN()
        );
      }
    }

You can imagine how difficult it will be to unit test this class, using Mockito, for example. First, we have to mock the `Region` interface. Then, we have to mock a `Table` interface and make sure it is returned by the `table()` method. Then, we have to mock a `Frame` interface, etc.

The unit test will be much longer than the class itself. Besides that, its real purpose, which is to test the retrieval of an employee's salary, will not be obvious to the reader.

Moreover, when we need to test a similar method of a similar class, we will need to restart this mocking from scratch. Again, multiple lines of code, which will look very similar to what we have already written.

The solution is to create fake classes and ship them together with real classes. This is what [jcabi-dynamo](http://dynamo.jcabi.com) is doing. Just look at its [JavaDoc](http://dynamo.jcabi.com/apidocs-0.16.1/index.html). There is a package called `com.jcabi.dynamo.mock` that contains only fake classes, suitable only for unit testing.

Even though their sole purpose is to optimize unit testing, we [ship them](http://www.yegor256.com/2014/08/19/how-to-release-to-maven-central.html) together with production code, in the same JAR package.

This is what a test will look like, when a fake class `MkRegion` is used:
    
    
    public class EmployeeTest {
      public void canFetchSalaryFromDynamoDb() {
        Region region = new MkRegion(
          new H2Data().with(
            "employees", new String[] {"name"},
            new String[] {"salary"}
          )
        );
        region.table("employees").put(
          new Attributes()
            .with("name", "Jeff")
            .with("salary", new AttributeValue().withN(50000))
        );
        Employee emp = new Employee("Jeff", region);
        assertThat(emp.salary(), equalTo(50000));
      }
    }

This test looks obvious to me. First, we create a fake DynamoDB region, which works on top of `H2Data` storage (in-memory H2 database). The storage will be ready for a single `employees` table with a hash key `name` and a single `salary` attribute.

Then, we put a record into the table, with a hash `Jeff` and a salary `50000`.

Finally, we create an instance of class `Employee` and check how it fetches the salary from DynamoDB.

I'm currently doing the same thing in almost every open source library I'm working with. I'm creating a collection of fake classes, that simplify testing inside the library and for its users.

BTW, a great article on the same subject: [tl;dw: Stop mocking, start testing](http://nedbatchelder.com/blog/201206/tldw_stop_mocking_start_testing.html) by Ned Batchelder.

PS. Check this out, on a very similar subject: [Mocking of HTTP Server in Java](http://www.yegor256.com/2014/04/18/jcabi-http-server-mocking.html).
