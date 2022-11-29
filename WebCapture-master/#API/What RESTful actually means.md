# What RESTful actually means

_Captured: 2015-12-25 at 00:27 from [codewords.recurse.com](https://codewords.recurse.com/issues/five/what-restful-actually-means)_

If you do web development, you've probably heard of REST. But if you're like me, you usually just pretend to know what it is, and nod politely when someone asks you if what you're making is RESTful. _I use HTTP, err, that means it's RESTful right?_ Recently, I decided to take the plunge and actually find out what this peaceful-sounding buzzword means.

## What is REST?

REST stands for Representational State Transfer. It is a set of design principles for making network communication more scalable and flexible. These principles answer a number of questions. What are the components of the system? How should they communicate with each other? How do we ensure we can swap out different parts of the system at any time? How can the system be scaled up to serve billions of users?

Roy T. Fielding first coined the term REST in 2000, in his PhD dissertation _[Architectural Styles and the Design of Network-based Software Architectures_](https://www.ics.uci.edu/~fielding/pubs/dissertation/top.htm). At the time of the dissertation's publication, the World Wide Web (or "the Web" for short) was already very popular. Fielding essentially took a step back and analyzed the traits that made the Web more successful than competing Internet protocols. He then envisioned a design framework for making network communication "web-like." So REST is a generic set of principles not specific to the Web. It can be applied to other kinds of networks such as embedded systems. REST is also not a protocol since it does not prescribe implementation details.

## The Fielding Constraints

Fielding's dissertation outlines a number of architectural constraints that a system must satisfy to be considered RESTful. Below, I'll give a brief overview of each of these constraints and discuss how the Web satisfies them using its core technologies: HTTP, HTML, and URIs.[1](https://codewords.recurse.com/issues/five/what-restful-actually-means)(If you're unfamiliar with URI, just think "URL". There is a distinction, but it is not important to our discussion.) Let's take a look at the Fielding Constraints one by one.

### Client-server

The first Fielding Constraint specifies that the network must be made up of clients and servers. A server is a computer that has resources of interest, and a client is a computer that wants to interact with the resources stored on the server. When you browse the Internet, your computer is acting as a client and sends HTTP requests to a server in order to access and manipulate information. A RESTful system has to operate in the client-server model, even if a component sometimes acts like a client and sometimes acts like a server.

A non-RESTful alternative to client-server architecture is event-based integration architecture. In this model, each component continuously broadcasts events while listening for pertinent events from other components. There's no one-to-one communication, only broadcasting and eavesdropping. REST requires one-to-one communication, so event-based integration architecture would not be RESTful.

### Stateless

Stateless does not mean that servers and clients do not have state, it simply means that they do not need to keep track of each other's state. When a client is not interacting with the server, the server has no idea of its existence. The server also does not keep a record of past requests. Each request is treated as a standalone.

### Uniform interface

The "uniform interface" constraint ensures that there is a common language between servers and clients that allows each part to be swapped out or modified without breaking the entire system. This is achieved through 4 sub-constraints: identification of resources, manipulation of resources through representations, self-descriptive messages, and hypermedia.

#### **Interface constraint 1: identification of resources**

The first sub-constraint of "uniform interface" affects the way that resources are identified. In REST terminology, a resource could be anything - an HTML document, an image, information about a particular user, etc. Each resource must be uniquely identified by a stable identifier. A "stable" identifier means that it does not change across interactions, and it does not change even when the state of the resource changes. If a resource does get moved to another identifier, the server should give the client a response indicating that the request was bad, and give it a link to the new location of the resource.

The Web uses URI to identify resources, and HTTP as its communication standard. To get a resource stored on a server, a client makes a HTTP GET request to the URI that identifies that resource. Every time you type an address into your browser, your browser makes a GET request to that URI. If it receives a 200 OK response and an HTML document back, then it renders the page in the window so that you can view it.

#### **Interface constraint 2: manipulation of resources through representations**

The second sub-constraint of "uniform interface" says that the client manipulates resources through sending representations to the server-usually a JSON object containing the content that it would like to add, delete, or modify. In REST, the server has full control of the resources, and is responsible for making any changes. When a client wishes to make changes to resources, it sends the server a representation of what it would like the resulting resource to look like. The server takes the request as a suggestion, but still has ultimate control.

Let's think about the case of a blog on the Web. When a user makes a new blog post, their computer wants to tell the server that a new blog post needs to be added. To do this, it sends an HTTP POST or PUT request with the content for the new blog post. The server sends back a response indicating whether the post was created, or if there was a problem. In a non-REST world, the client may literally be sending instructions for operations such as _add a new line_ and _make the title of the blog "What RESTful Actually Means"_, instead of simply sending a representation of what it would like the final product to look like.

#### **Interface constraint 3: self-descriptive messages**

Self-descriptive messages are another constraint that ensures a uniform interface between clients and servers. A self-descriptive message is one that contains all the information that the recipient needs to understand it. There should not be additional information in a separate documentation or in another message.

To understand how this applies to the Web, let's analyze a set of HTTP requests and responses.

When a user types _http://www.example.com_ in the address bar of their web browser, the browser sends the following HTTP request:
    
    
    GET / HTTP/1.1
    Host: www.example.com
    

This message is self-descriptive because it told the server what HTTP method was used, and the protocol that was used (HTTP 1.1).

The server may send back a response like this:
    
    
    HTTP/1.1 200 OK
    Content-Type: text/html
    
    <!DOCTYPE html>
    <html>
      <head>
        <title>Home Page</title>
      </head>
      </body>
        <div>Hello World!</div>
        <a href= “http://www.recurse.com”> Check out the Recurse Center! </a>
        <img src="awesome-pic.jpg">
      </body>
    </html>
    

This message is self-descriptive because it told the client how it needs to interpret the message body, by indicating that `Content-type` was `text/html`. The client has everything it needs in this single message to handle it appropriately.

Imagine an alternative method of communication where the server sent binary code in one response, and then sent a seperate response telling the client how to interpret the binary code-whether it is an image or a code snippet. If the two responses had somehow arrived out of order, or if a third response was inserted between them, then the client may be confused about how to interpret the responses properly.

#### **Interface constraint 4: hypermedia**

The last interface constraint is the hypermedia constraint. Hypermedia is a fancy word for data sent from the server to the client that contains information about what the client can do next-in other words, what further requests it can make. In REST, servers should be sending only hypermedia to clients.

HTML is a type of hypermedia. To understand this better, let's look again at the server response above. * `<a href= "http://www.recurse.com"> Check out the Recurse Center! </a>` tells the client that it should make a GET request to _http://www.recurse.com_ if the user clicks on the link. * `<img src="awesome-pic.jpg">` tells the client to immediately make a GET request to _http://www.example.com/awesome-pic.jpg_ so it can display the image to the user.

When a system has identifiers for each resource, manipulates them through sending representations from the client to the server, and has messages that are self-descriptive and composed of hypermedia, it is said to have a uniform interface. This is perhaps the most important attribute of a RESTful system, as it allows for clients to intelligently adapt to changes. A server can change the underlying implementation without breaking all the clients that interacted with it, because each interaction is self-contained, identifiers do not change when the underlying state or implementation changes, and hypermedia gives clients instructions for state transitions that it can do next. The server does not need to remember anything about the client or do anything special to cater to it, and vice versa.

### Other Fielding Constraints: caching, layered system, and code on demand

There are three more Fielding Constraints, which we'll explore briefly here.

**Caching** refers to the constraint that server responses should be labelled as either cacheable or non-cacheable. Caching occurs when the client stores previous responses it received from the server, so that when that data is needed again, it can save a round trip over the network by using the cached data. The ability to cache is made possible by the interface constraint of "self-descriptive messages", since the client knows that all the relevant data about a single resource is being sent in one response. It doesn't have to worry about accidentally only caching part of the information it needs, and missing other parts.

**Layered system** refers to the fact that there can be more components than just servers and clients. This means there can be more than one layer in the system. However, each component is constrained to only see and interact with the very next layer. A proxy is an additional component, and it relays HTTP requests to servers or other proxies. Proxies can be useful for load balancing and security checks. A proxy acts like a server to the initial client that sends the request, and then acts like a client when it relays that request. A gateway is another additional component and it translates an HTTP request into another protocol, propagates that request, and then translates the response it receives back into HTTP. A client can simply treat a gateway as a regular server. An example use case for gateways is a system that needs to download a file from an FTP server.

**Code on demand** is the only optional constraint and refers to the ability for a server to send executable code to the client. This is what happens in HTML's `<script>` tag. When the HTML document is loaded, the browser automatically fetches the JavaScript from the server and executes it locally.

In summary, a RESTful system is any network that fulfills the Fielding Constraints. A RESTful system is meant to be flexible for different use cases, scalable to accommodate a large number of users and components, and adaptable over time. We explored how the World Wide Web is RESTful when it comes to interactions involving browsers and human users. Designing RESTful Web APIs for machine-to-machine interactions is a much more complex topic; see the resources listed below for more information. Remember that REST is a theoretical design, and the Web we have today still falls short in some cases.

Next time, you no longer have to pretend to know what RESTful actually means.

## Further reading
