title: RESTful Web Services : The basics
---

Representational State Transfer(REST)  
[Abstract from IBM developerWorks - A good article for understanding the RESTful](http://www.ibm.com/developerworks/library/ws-restful/) 
## The basics

a concrete implementation of a REST Web service follows four basic design principles :

+ Use HTTP methods explicitly.
+ Be stateless.
+ Expose directory structure-like URIs.
+ Transfer XML, JSON ,or both.

### Use HTTP methods explicitly

REST asks developers to use HTTP methods explicitly and in a way that's consistent with the protocol definition. This basic REST design principle establishes a one-to-one mapping between create,read,update,and delete(CRUD) operations and HTTP methods. According to this mapping :
+ To create a resource on the server , use POST.
+ To retrieve a resource , use GET.
+ To change the state of a resource or to update it , use PUT.
+ To remove or delete a resource , use DELETE.

As a general design principle , it helps to follow REST guidelines for using HTTP methods explicitly by using nouns in URIs instead of verbs. In a RESTful Web service , the verbs - POST, GET, PUT , and DELETE - are already defined by the protocol. 
And ideally, to keep the interface generalized and to allow clients to be explicit about the operations they invoke , the Web service should not define more verbs or remote procedures, such as `/addUser` or `/updateUser` . This general design principle also applies to the body of an HTTP request , which is intended to be used to transfer resource state, not to carry the name of a remote method or remote procedure to be invoked.

### Be stateless

REST Web services need to scale to meet increasingly high performance demands.

#### Server

+ **Generates responses that include links to other resources to allow applications to navigate between related resources.** This type of response embed links . Similarly , if the request is for a parent or container resource, then a typical RESTful response might also include links to the parent's children or subordinate resources so that these remain connected.
+ **Generates responses that indicate whether they are cache-able or not to improve performance by reducing the number of requests for duplicate resources and by eliminating some requests entirely.** The server does this by including a Cache-Control and Last-Modified (a data value) HTTP response header.

#### Client Application

+ **Uses the Cache-Control response header to determine whether to cache the resource (make a local copy of it) or not.** The client also reads the Last-Modified response header and sends back the date value in an If-Modified-Since header to ask the server if the resource has changed. This is called Conditional GET , and the two headers go hand in hand in that the server's response is a standard 304 code (Not Modified) and omits the actual resource requested if it has not changed since that time. _A 304 HTTP response code means the client can safely use a cached, local copy of the resource representation as the most up-to-date, in effect bypassing subsequent GET requests until the resource changes._
+ **Sends complete requests that can be serviced independently of other requests.** This requires the client to make full use of HTTP headers as specified by the Web service interface and to send complete representations of resources in the request body. The client sends requests that make very few assumptions about prior requests, the existence of a session on the server, the server's ability to add context to a request, or about application state that is kept in between requests.

#### Summary

This collaboration between client application and service is essential to being stateless in a RESTful Web service. It improves performances by saving bandwidth and minimizing server-side application state.

### Expose directory structure-like URIs

From the standpoint of client applications addressing resources, the URIs determine how intuitive the REST Web service is going to be and whether the service is going to be used in ways that the designers can anticipate. A third RESTful Web service characteristic is all about the URIs.

+ REST Web service URIs should be intuitive to the point where they are easy to guess. To this end , the structure of a URI should be straightforward, predictable , and easily understood.
+ One way to achieve this level of usability is to define directory structure-like URIs. This type of URI is hierarchical, rooted at a single path, and branching from it are sub-paths that expose the service's main areas. 
    + According to this definition, a URI is not merely a slash-delimited string, but rather a tree with subordinate and superordinate branches connected at nodes. 
    + In some cases, the path to a resource lends itself especially well to a directory-like structure. Take resources organized by date, for instance, which are a very good match for using a hierarchical syntax.
+ Some additional guidelines to make note of while thinking about URI structure for a RESTful Web service :
    + Hide the server-side scripting technology file extensions (.jsp, .php, .asp), if any, so you can port to something else without changing the URIs.
    + Keep everything lowercase.
    + Substitute spaces with hyphens or underscores (one or the other ).
    + Avoid query strings as much as you can.
    + Instead of using the 404 NOT Found code if the request URI is for a partial path, always provide a default page for resource as a response.


URIs should also be static so that when the resource changes or the implementation of the service changes, the link stays the same. This allows bookmarking. It's also important that the relationship between resources that's encoded in the URIs remains independent of the way the relationships are represented where they are stored.

### Transfer XML, JSON , or both

_To give client applications the ability to request a specific content type that's best suited for them._  

construct your service so that it makes use of the built-in HTTP Accept header, where the value of the header is a MIME type. Some common MIME types used by RESTful services are shown in Table 1.  

_Table 1. Common MIME types used by RESTful services_
MIME-Type  |  Content-Type
JSON  |  application/json 
XML  |  application/xml
XHTML  |  application/xhtml+xml 

This allows the service to be used by a variety of clients written in different languages running on different platforms and devices. Using MIME types and the HTTP Accept header is a mechanism known as content negotiation, which lets clients choose which data format is right for them and minimizes data coupling between the service and the applications that use it.

### Conclusion

    REST is not always the right choice. It has caught on as a way to design Web services with less dependence on proprietary middle-ware (for example, an application server) than the SOAP- and WSDL-based kind. And in a sense, REST is a return to the Web the way it was before the age of the big application server, through its emphasis on the early Internet standards, URI and HTTP. As you've examined in the so-called principles of RESTful interface design, XML over HTTP is a powerful interface that allows internal applications, such as Asynchronous JavaScript + XML (Ajax)-based custom user interfaces, to easily connect, address, and consume resources. In fact, the great fit between Ajax and REST has increased the amount of attention REST is getting these days.
    Exposing a system's resources through a RESTful API is a flexible way to provide different kinds of applications with data formatted in a standard way. It helps to meet integration requirements that are critical to building systems where data can be easily combined (mashups) and to extend or build on a set of base, RESTful services into something much bigger. This article touches on just the basics here but hopefully in a way that has enticed you to continue exploring the subject.

