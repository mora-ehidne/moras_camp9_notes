# REST (REpresentational State Transfer)

REST is a software architectural style for HTTP-based APIs.
An API that is based on this architectural style is called RESTful.

It is defined in year 2000.

REST has six architectural constraints:
1. **Use of a uniform interface (UI)**
    Resources should be uniquely identifiable through a single URL, and only by using the underlying methods of the network protocol, such as DELETE, PUT and GET with HTTP, should it be possible to manipulate a resource.
    >
2. **Client-server based**.
   There should be a clear delineation between the client and server. UI and request-gathering concerns are the client's domain. Data access, workload management and security are the server's domain. This loose coupling of the client and server enables each to be developed and enhanced independent of the other.
   >
3. **Stateless operations**.
   All client-server operations should be stateless, and any state management that is required should take place on the client, not the server.
   >
4. **RESTful resource** caching.
   All resources should allow caching unless explicitly indicated that caching is not possible.
   >
5. **Layered system**. 
   REST allows for an architecture composed of multiple layers of servers.
   >
6. **Code on demand**. 
   Most of the time, a server will send back static representations of resources in the form of XML or JSON. However, when necessary, servers can send executable code to the client.
