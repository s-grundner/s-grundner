# REST API Industry Debate: OData vs GraphQL vs ORDS

_Captured: 2017-05-05 at 23:57 from [dzone.com](https://dzone.com/articles/rest-api-industry-debate-odata-vs-graphql-vs-ords?edition=297993&utm_source=Daily%20Digest&utm_medium=email&utm_campaign=dd%202017-05-05)_

Learn how API management supports better integration in [Achieving Enterprise Agility with Microservices and API Management](https://dzone.com/go?i=126027&u=http%3A%2F%2Fpages.3scale.net%2Fmicroservices-api-management-dzinteg.html), brought to you in partnership with [3scale](https://dzone.com/go?i=126027&u=https%3A%2F%2Fwww.3scale.net%2F%3Futm_campaign%3Ddzintegration%26utm_source%3Ddzoneint%26utm_content%3Dbumper)

Jeff Leinbach, senior software engineer at Progress, and Saikrishna Teja Bobba, developer evangelist at Progress, conducted this research to help you decide which standard API to consider adopting in your application or analytics/data management tool. We contrasted the differences between OData, GraphQL and ORDS, which are standard APIs and services for querying and updating data over the Internet. The focus is on achieving interoperability across APIs for analytics, integration and data management.

We've been tracking these topics based on numerous discussions at industry events such as AWS re:Invent, Oracle OpenWorld, Dreamforce, API World and more. Progress also has a rich heritage in developing and contributing to data access standards, including ODBC, JDBC, ADO.NET and now OData (REST), and was the first member to join the OData Technical Committee.

## What is REST?

REST (representational state transfer) or RESTful web services are one way of providing interoperability between computer systems on the internet. REST-compliant web services allow requesting systems to access and manipulate textual representations of web resources using a uniform and predefined set of stateless operations. RESTful implementations make use of standards such as HTTP, URI, JSON, and XML.

It's important to note that REST is an architectural style, not a standard.

## Standard APIs to Query Data over the Internet

### OData

Originally developed by Microsoft in 2007, [OData](http://www.odata.org/) is an OASIS standard REST API and is established among companies such as Microsoft, SAP, CA, IBM, and Salesforce. It allows the creation and consumption of queryable and interoperable RESTful APIs in a simple and standard way. OData gives you a rich set of querying capabilities and is quickly gaining ground for its open source approach, as well as its exceptional scalability.

### GraphQL

Developed internally at Facebook in 2012, before public release in 2015, [GraphQL](http://graphql.org/) is a data query language deployed at companies such as Facebook, Shopify and Intuit. GraphQL provides a complete and understandable description of the data in your API, gives clients the power to ask for exactly what they need, makes it easier to evolve APIs over time and enables powerful developer tools.

### ORDS

[ORDS](http://www.oracle.com/technetwork/developer-tools/rest-data-services/overview/index.html) (Oracle REST Data Services) is the Oracle REST service which delivers similar standardization for Oracle-centric applications. It enables developers with SQL and other database skills to build enterprise-class data access APIs to Oracle Database that today's modern, state-of-the-art application developers want to use, and indeed increasingly demand to use, to build applications. Sixty groups at Oracle use ORDS, including Oracle Database, Times Ten, and NoSQL.

## Contrasting the Standard APIs

### Figure 1

![OData vs GraphQL vs ORDS](https://d117h1jjiq768j.cloudfront.net/images/default-source/default-album/table-1---capabilities.jpg?sfvrsn=1)

> _Contrasting the REST APIs_

The criteria for contrasting the standard APIs in Figure 1 are based on achieving interoperability with multiple data sources. One thing to note about this comparison is the maturity of the specification. While GraphQL is growing in popularity, questions remain around maturity for widespread adoption, best practices, and tooling.

Under API versioning/maintenance, you would think a "no" is bad, but it's actually good. It's one of the advantages of GraphQL, which I'll go into later.

### Figure 2

![OData vs GraphQL](https://d117h1jjiq768j.cloudfront.net/images/default-source/default-album/table-2---capabilities.jpg?sfvrsn=1)

> _Constrast the REST APIs - Table 2_

In Figure 2, we completed the initial analysis on additional criteria to consider and will expand on these areas in a future article.

## Standard Query Capabilities

### Figure 3

![Query Capabilities - OData vs GraphQL vs ORDS](https://d117h1jjiq768j.cloudfront.net/images/default-source/default-album/table-3---query-capabilities.jpg?sfvrsn=1)

> _Standard Query Capabilities_

Figure 3 highlights common criteria for accessing data through open standard interfaces. OData has the full range of support for all these query capabilities. You can do some of these operations with GraphQL and ORDS, but they're not standardized or documented in a way to achieve interoperability.

GraphQL is much like REST in that it defines the way to interact with a web service, but it doesn't tell you what the service does. So you can do filtering, ordering, and joins, etc. by creating functions that can call, but the application developer has to understand how those work semantically to be able to know what their behaviors are.

With ORDS, you can do aggregation and joining, but it's accomplished through creating custom functions that you can invoke. But the application has to know what those functions do in order to understand how to interpret the results. There's no metadata or standard behavior definition that can tell the application what to expect.

## Surfacing Metadata

### Figure 4

![Surfacing Metadata - OData vs GraphQL vs ORDS](https://d117h1jjiq768j.cloudfront.net/images/default-source/default-album/table-5---surfacing-metadata.jpg?sfvrsn=1)

> _Surfacing Metadata - OData vs GraphQL vs ORDS_

Figure 4 compares surfacing metadata, which is core to analytics and data management applications that need to programmatically reverse-engineer schemas in an interoperable way.

Each of these APIs is advancing to solve this, however, GraphQL and ORDS don't tell you scale and precision of data, whereas OData does. GraphQL also doesn't tell you about primary keys and ORDS doesn't tell you about nullability. This information is important for an application to be able to know what it can and can't do with each particular field.

## API Versioning and Maintenance

One major headache is handling updates to applications when the API changes while maintaining older versions as well. The biggest problem leading to this headache with REST APIs is that all of the fields are returned when you query an endpoint. API developers have no window into whether or not clients are relying on information in specific fields. Client developers must process all of the fields returned even if they do not need the information.

GraphQL has addressed the problem of API versioning and maintenance by forcing clients to specify exactly which fields they require. API developers can proactively reach out to known consumers of fields to migrate off of deprecated fields. The response includes information about which fields are deprecated.

OData provides similar functionality by providing a select list to limit the number of fields returned to those needed by an application. This reduces response size and processing in an application. However, it does not provide a mechanism to indicate that fields are deprecated.

OData is more flexible in that queries can be easily written to return all fields. And OData is adding schema versioning to the specification to deal with this problem.

## Examples

To visually illustrate the differences in working with these APIs, the following two code examples show how to do an "Order By" in GraphQL and OData.

![GraphQL - Order By Example](https://d117h1jjiq768j.cloudfront.net/images/default-source/default-album/graphql---order-by.jpg?sfvrsn=1)

> _GraphQL - Order By Example_

In the GraphQL example of an All Opportunities function call, it's somewhat obvious by the name what it does. However, there's nothing in GraphQL that tells you what you can pass in for these arguments and how the values specified as arguments causes the function to behave. And this behavior can be different on an implementation by implementation basis.

![OData - Order By Code Example](https://d117h1jjiq768j.cloudfront.net/images/default-source/default-album/odata---order-by.jpg?sfvrsn=1)

> _OData - Order By Code Example_

By contrast, OData tells you exactly how it's going to behave when you use the orderBy query parameter because its behavior is defined as part of the specification.

## Recommendations

![Recommendations - OData vs GraphQL vs ORDS](https://d117h1jjiq768j.cloudfront.net/images/default-source/default-album/table-6---recommendations.jpg?sfvrsn=1)

> _Recommendations - OData vs GraphQL vs ORDS_

GraphQL is almost like a programming language, which makes it very flexible. It's powerful, but using it means your application is tightly coupled to how that particular GraphQL service is implemented. There's no way to generically describe how it works.

GraphQL can also be a bit awkward for people who are used to dealing with web services because, in order to query data, you don't do a GET operation, which is how you would get results from a normal REST web service. You do a POST, defining exactly which fields and functions that you want to be included in the response.

So while GraphQL gives you the ability to determine from the metadata what fields and functions are available, you still don't know what they mean semantically.

## Removing Barriers to Entry

This article is primarily focused on the API consumers, but GraphQL has a much lower barrier to entry to develop an API. If you're doing a quick project, GraphQL is probably the way to go. But you still have the issue of your application being tightly coupled to your implementation.

OData is really powerful, but there's a lot of heavy lifting that goes with it because you have to adhere to all the behaviors of the standard. There's a minimum level of behaviors that you must have to be OData compliant. That creates a larger barrier to entry for service developers.

However, you can leverage our [hybrid technology](https://www.progress.com/cloud-and-hybrid-data-integration) to produce a standard REST API (OData). We do all the heavy lifting [leverage our ](http://twitter.com/share?text=leverage%20our%20hybrid%20technology%C2%A0to%20produce%20a%20standard%20REST%20API%20\(OData\).%20We%20do%20all%20the%20heavy%20lifting)[hybrid technology](https://www.progress.com/cloud-and-hybrid-data-integration) to produce a standard REST API (OData). We do all the heavy lifting with OData, so you don't have to worry about adhering to the standard. We've reduced the barrier to entry for you.

Also, there are a lot of OData clients that can help you get up and running with the OData service quickly and easily. There's a laundry list of applications that are already OData-capable, as well as OData client libraries that can help you if you're developing a new application.

If you'd like to learn how to embed our hybrid technology to [expose data over REST using OData](https://www.progress.com/cloud-and-hybrid-data-integration), talk to one of our data connectivity experts today.

Unleash the power of your APIs with future-proof API management - [Create your account](https://dzone.com/go?i=126028&u=http%3A%2F%2Fpages.3scale.net%2Ffuture-proof-api-management-dzinteg.html) and start your free trial today, brought to you in partnership with [3scale](https://dzone.com/go?i=126028&u=https%3A%2F%2Fwww.3scale.net%2F%3Futm_campaign%3Ddzintegration%26utm_source%3Ddzoneint%26utm_content%3Dbumper).
