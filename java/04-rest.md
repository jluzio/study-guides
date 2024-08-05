What is RESTful API?
--------------------

RESTful API is an interface that two computer systems use to exchange information securely over the internet. Most business applications have to communicate with other internal and third-party applications to perform various tasks. For example, to generate monthly payslips, your internal accounts system has to share data with your customer's banking system to automate invoicing and communicate with an internal timesheet application. RESTful APIs support this information exchange because they follow secure, reliable, and efficient software communication standards.

What is an API?
---------------

An application programming interface (API) defines the rules that you must follow to communicate with other software systems. Developers expose or create APIs so that other applications can communicate with their applications programmatically. For example, the timesheet application exposes an API that asks for an employee's full name and a range of dates. When it receives this information, it internally processes the employee's timesheet and returns the number of hours worked in that date range.

You can think of a web API as a gateway between clients and resources on the web.

### Clients

Clients are users who want to access information from the web. The client can be a person or a software system that uses the API. For example, developers can write programs that access weather data from a weather system. Or you can access the same data from your browser when you visit the weather website directly.

### Resources

Resources are the information that different applications provide to their clients. Resources can be images, videos, text, numbers, or any type of data. The machine that gives the resource to the client is also called the server. Organizations use APIs to share resources and provide web services while maintaining security, control, and authentication. In addition, APIs help them to determine which clients get access to specific internal resources.

What is REST?
-------------

Representational State Transfer (REST) is a software architecture that imposes conditions on how an API should work. REST was initially created as a guideline to manage communication on a complex network like the internet. You can use REST-based architecture to support high-performing and reliable communication at scale. You can easily implement and modify it, bringing visibility and cross-platform portability to any API system.

API developers can design APIs using several different architectures. APIs that follow the REST architectural style are called REST APIs. Web services that implement REST architecture are called RESTful web services. The term RESTful API generally refers to RESTful web APIs. However, you can use the terms REST API and RESTful API interchangeably.

The following are some of the principles of the REST architectural style:

### Uniform interface

By applying the principle of generality to the components interface, we can simplify the overall system architecture and improve the visibility of interactions. Multiple architectural constraints help in obtaining a uniform interface and guiding the behavior of components.

The following four constraints can achieve a uniform REST interface:

*   **Identification of resources** – The interface must uniquely identify each resource involved in the interaction between the client and the server.
*   **Manipulation of resources through representations** – The resources should have uniform representations in the server response. API consumers should use these representations to modify the resource state in the server.
*   **Self-descriptive messages** – Each resource representation should carry enough information to describe how to process the message. It should also provide information of the additional actions that the client can perform on the resource.
*   **Hypermedia as the engine of application state** – The client should have only the initial URI of the application. The client application should dynamically drive all other resources and interactions with the use of hyperlinks.

In simpler words, REST defines a consistent and uniform interface for interactions between clients and servers. For example, the HTTP-based REST APIs make use of the standard HTTP methods (GET, POST, PUT, DELETE, etc.) and the URIs (Uniform Resource Identifiers) to identify resources.

### Client/Server
The client-server design pattern enforces the separation of concerns, which helps the client and the server components evolve independently.

By separating the user interface concerns (client) from the data storage concerns (server), we improve the portability of the user interface across multiple platforms and improve scalability by simplifying the server components.

While the client and the server evolve, we have to make sure that the interface/contract between the client and the server does not break.

### Statelessness

In REST architecture, statelessness refers to a communication method in which the server completes every client request independently of all previous requests. Clients can request resources in any order, and every request is stateless or isolated from other requests. This REST API design constraint implies that the server can completely understand and fulfill the request every time. 

### Layered system

In a layered system architecture, the client can connect to other authorized intermediaries between the client and server, and it will still receive responses from the server. Servers can also pass on requests to other servers. You can design your RESTful web service to run on several servers with multiple layers such as security, application, and business logic, working together to fulfill client requests. These layers remain invisible to the client.

### Cacheability

RESTful web services support caching, which is the process of storing some responses on the client or on an intermediary to improve server response time. For example, suppose that you visit a website that has common header and footer images on every page. Every time you visit a new website page, the server must resend the same images. To avoid this, the client caches or stores these images after the first response and then uses the images directly from the cache. RESTful web services control caching by using API responses that define themselves as cacheable or noncacheable.

### Code on demand

In REST architectural style, servers can temporarily extend or customize client functionality by transferring software programming code to the client. For example, when you fill a registration form on any website, your browser immediately highlights any mistakes you make, such as incorrect phone numbers. It can do this because of the code sent by the server.

What are the benefits of RESTful APIs?
--------------------------------------

RESTful APIs include the following benefits:

### Scalability

Systems that implement REST APIs can scale efficiently because REST optimizes client-server interactions. Statelessness removes server load because the server does not have to retain past client request information. Well-managed caching partially or completely eliminates some client-server interactions. All these features support scalability without causing communication bottlenecks that reduce performance.

### Flexibility

RESTful web services support total client-server separation. They simplify and decouple various server components so that each part can evolve independently. Platform or technology changes at the server application do not affect the client application. The ability to layer application functions increases flexibility even further. For example, developers can make changes to the database layer without rewriting the application logic.

### Independence

REST APIs are independent of the technology used. You can write both client and server applications in various programming languages without affecting the API design. You can also change the underlying technology on either side without affecting the communication.

How do RESTful APIs work?
-------------------------

The basic function of a RESTful API is the same as browsing the internet. The client contacts the server by using the API when it requires a resource. API developers explain how the client should use the REST API in the server application API documentation. These are the general steps for any REST API call:

1.  The client sends a request to the server. The client follows the API documentation to format the request in a way that the server understands.
2.  The server authenticates the client and confirms that the client has the right to make that request.
3.  The server receives the request and processes it internally.
4.  The server returns a response to the client. The response contains information that tells the client whether the request was successful. The response also includes any information that the client requested.

The REST API request and response details vary slightly depending on how the API developers design the API.

What does the RESTful API client request contain?
-------------------------------------------------

RESTful APIs require requests to contain the following main components:

### Unique resource identifier

The server identifies each resource with unique resource identifiers. For REST services, the server typically performs resource identification by using a Uniform Resource Locator (URL). The URL specifies the path to the resource. A URL is similar to the website address that you enter into your browser to visit any webpage. The URL is also called the request endpoint and clearly specifies to the server what the client requires.


### Method
Developers often implement RESTful APIs by using the Hypertext Transfer Protocol (HTTP). An HTTP method tells the server what it needs to do to the resource.

### HTTP headers

Request headers are the metadata exchanged between the client and server. For instance, the request header indicates the format of the request and response, provides information about request status, and so on.

_**Data**_

REST API requests might include data for the POST, PUT, and other HTTP methods to work successfully.

_**Parameters**_

RESTful API requests can include parameters that give the server more details about what needs to be done. The following are some different types of parameters:

*   Path parameters that specify URL details.
*   Query parameters that request more information about the resource.
*   Cookie parameters that authenticate clients quickly.


## Semantics of HTTP methods
### GET

Use GET requests to retrieve resource representation/information only – and not modify it in any way. As GET requests do not change the resource’s state, these are said to be safe methods.
Additionally, GET APIs should be idempotent. Making multiple identical requests must produce the same result every time until another API (POST or PUT) has changed the state of the resource on the server.

### POST

Use POST APIs to create new subordinate resources, e.g., a file is subordinate to a directory containing it or a row is subordinate to a database table.
When talking strictly about REST, POST methods are used to create a new resource into the collection of resources.
Responses to this method are not cacheable unless the response includes appropriate Cache-Control or Expires header fields.
Please note that POST is neither safe nor idempotent, and invoking two identical POST requests will result in two different resources containing the same information (except resource ids).

### PUT

Use PUT APIs primarily to update an existing resource (if the resource does not exist, then API may decide to create a new resource or not).
If the request passes through a cache and the Request-URI identifies one or more currently cached entities, those entries SHOULD be treated as stale. 
Responses to PUT method are not cacheable.

### DELETE

As the name applies, DELETE APIs delete the resources (identified by the Request-URI).
DELETE operations are idempotent. If you DELETE a resource, it’s removed from the collection of resources.
Some may argue that it makes the DELETE method non-idempotent. It’s a matter of discussion and personal opinion.
If the request passes through a cache and the Request-URI identifies one or more currently cached entities, those entries SHOULD be treated as stale. 
Responses to this method are not cacheable.

### PATCH

HTTP PATCH requests are to make a partial update on a resource.
If you see PUT requests modify a resource entity too. So to make it more precise – the PATCH method is the correct choice for partially updating an existing resource, and you should only use PUT if you’re replacing a resource in its entirety.
Please note that there are some challenges if you decide to use PATCH APIs in your application:
Support for PATCH in browsers, servers, and web application frameworks is not universal. IE8, PHP, Tomcat, Django, and lots of other software have missing or broken support for it.
Request payload of a PATCH request is not straightforward as it is for a PUT request (e.g. patch spec, etc).


## Best Practices for Designing REST APIs

### Resource Naming Conventions

Designing intuitive and consistent URI structures is crucial for creating user-friendly and maintainable REST APIs. Following best practices in resource naming helps clients understand and interact with your API more effectively.

**Guidelines for Designing URI Structures:**

1.  **Use Nouns, Not Verbs:** URIs should represent resources, so use nouns to name endpoints. For example, use `/users` instead of `/getUsers`.
2.  **Hierarchical Structure:** Organize URIs to reflect resource hierarchy. For example, use `/users/{userId}/orders/{orderId}` to indicate that orders belong to users.
3.  **Plural Names for Collections:** Use plural nouns for collections of resources. For example, use `/users` for a collection of user resources.
4.  **Use Hyphens for Readability:** Use hyphens to improve readability of multi-word URIs. For example, use `/user-profiles` instead of `/userProfiles`.
5.  **Consistent Naming Conventions:** Apply a consistent naming convention throughout your API. Stick to a format like snake\_case or camelCase, and use it consistently.

**Examples of Good and Bad Practices:**

*   Good: `/users`, `/users/{userId}`, `/users/{userId}/orders`
*   Bad: `/getUsers`, `/Users/{id}`, `/users/{userId}/getOrders`

#### Versioning Strategies

Versioning APIs is essential for managing changes and ensuring backward compatibility for clients. Here are some common methods for versioning APIs:

**1. URL Versioning:**

*   **Example:** `/v1/users`
*   **Pros:** Easy to understand and implement. Clear separation of versions.
*   **Cons:** Can lead to URI clutter if many versions are maintained.

**2. Header Versioning:**

*   **Example:** `GET /users` with `Accept: application/vnd.example.v1+json`
*   **Pros:** Cleaner URLs. Versioning information is abstracted from the URI.
*   **Cons:** Less visible and harder to test with simple tools like cURL.

**3. Query Parameter Versioning:**

*   **Example:** `/users?version=1`
*   **Pros:** Easy to implement and test.
*   **Cons:** Clutters query parameters and mixes versioning with other query options.

#### Handling Errors and Status Codes

Returning meaningful HTTP status codes and error messages is crucial for API usability and debugging. Here are some best practices:

**1. Use Standard HTTP Status Codes:**

*   **200 OK:** Request succeeded.
*   **201 Created:** Resource created successfully.
*   **400 Bad Request:** Client-side input validation failed.
*   **401 Unauthorized:** Authentication required.
*   **403 Forbidden:** Client authenticated but does not have permission.
*   **404 Not Found:** Resource not found.
*   **500 Internal Server Error:** Server encountered an unexpected condition.

**2. Standardizing Error Responses:**

**Example Format:**

 Copy code
~~~json
{
  "error": {
    "code": 400,
    "message": "Invalid input data",
    "details": [
      {
        "field": "email",
        "issue": "Email format is invalid"
      }
    ]
  }
}
~~~


What are RESTful API authentication methods?
--------------------------------------------

A RESTful web service must authenticate requests before it can send a response. Authentication is the process of verifying an identity. For example, you can prove your identity by showing an ID card or driver's license. Similarly, RESTful service clients must prove their identity to the server to establish trust.

RESTful API has four common authentication methods:

### HTTP authentication

HTTP defines some authentication schemes that you can use directly when you are implementing REST API. The following are two of these schemes:

_**Basic authentication**_

In basic authentication, the client sends the user name and password in the request header. It encodes them with base64, which is an encoding technique that converts the pair into a set of 64 characters for safe transmission.

_**Bearer authentication**_

The term bearer authentication refers to the process of giving access control to the token bearer. The bearer token is typically an encrypted string of characters that the server generates in response to a login request. The client sends the token in the request headers to access resources.

### API keys

API keys are another option for REST API authentication. In this approach, the server assigns a unique generated value to a first-time client. Whenever the client tries to access resources, it uses the unique API key to verify itself. API keys are less secure because the client has to transmit the key, which makes it vulnerable to network theft.

### OAuth

OAuth combines passwords and tokens for highly secure login access to any system. The server first requests a password and then asks for an additional token to complete the authorization process. It can check the token at any time and also over time with a specific scope and longevity.


### Example
```java
// Example JAX-RS
@Path("/notifications")
public class NotificationsResource {
  @GET
  @Path("/ping")
  public Response ping() {
    return Response.ok().entity("Service online").build();
  }

  @GET
  @Path("/get/{id}")
  @Produces(MediaType.APPLICATION_JSON)
  public Response getNotification(@PathParam("id") int id) {
    return Response.ok()
        .entity(new Notification(id, "john", "test notification"))
        .build();
  }

  @POST
  @Path("/post/")
  @Consumes(MediaType.APPLICATION_JSON)
  @Produces(MediaType.APPLICATION_JSON)
  public Response postNotification(Notification notification) {
    return Response.status(201).entity(notification).build();
  }
}
```

```java
// Example Spring
@RestController
public class GreetingController {

  @GetMapping(path = "/webmvc/hello")
  public String hello() {
    return "Hello, WebMvc Spring!";
  }

}
```