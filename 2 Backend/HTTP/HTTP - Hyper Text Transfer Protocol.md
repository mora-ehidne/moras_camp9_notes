# HTTP

HTTP (Hyper Text Transfer Protocol) is a protocol for transmitting hypermedia documents, eg. HTML. It is used primarily to communicate between web browsers and servers. It follows a classical client-server model in which a client (eg. a web browser) makes a **request** to a server and then waits until it recieves a **response**.

HTTP is a stateless protocol - it stores no data between requests. In order to temporarily store some data, HTTP has cookies.

A server cannot send anything to a client without receiving an HTTP Request first, to which it can then send an HTTP Response.

>[!TIP] There are many entities between a client (user-agent) and a server. They are collectively called _proxies_. These include modems, routers etc. They are hidden in the network and transport layers and mostly irrelevant for HTTP.

>[!NOTE] An example of how HTTP works, client-side:
>A web browser establishes connection with a server.
>
>The browser sends a GET request to the URL of `www.google.com`. 
>
>The server in charge of that URL sends back a response with an HTML file. The browser then parses the HTML file, and makes more GET requests for the linked files, such as CSS files, scripts and sub-resources such as images, videos etc. When the files required to start loading the page are downloaded, the browser combines all these resources to display the page.
>
>New requests can be made in later phases to update the page.

HTTP is sent over TCP (Transmission Control Protocol), sometimes encrypted through the TLS (Transport Layer Security, formerly known as SSL - Secure Sockets Layer) protocol.