# HTTP APIs

The most common HTTP API is the XMLHttpRequest API (XHR), and the Fetch API is a modern counterpart to it. In order to do HTTP requests through JavaScript, these APIs can be used directly, or through an HTTP client such as [[Axios - Promise based HTTP client|Axios]] (which uses XHR).

# HTTP Request Structure

HTTP Requests are sent from the client to the server.

All HTTP Requests follow this structure:
1. Request Message Header / Head
	1. Request Line / Start-Line (mandatory, most important information for the request)
		1. The HTTP Method - GET, POST, PATCH etc.
		2. The path of the resource - typically a URL such as `https://www.google.com`
		3. The version of the HTTP protocol - eg. `HTTP/1.1` 
	2. Request Headers (optional) - additional data for the request, the syntax is a case-insensitive string followed by a colon and the header
2. Request Message Body / Payload (optional, separated from the Header by a blank line) - the data that is sent to the server, eg. in a POST, PATCH or PUT request

![[HTTP_RequestMessageExample.png]]

# HTTP Response Structure

All responses from the server to a HTTP request from a client are in the form of an HTTP response.

All HTTP responses follow this structure:
1. Reponse Message Header / Head
	1. Status Line / Start-Line (mandatory)
		1. The version of the HTTP protocol - eg. `HTTP/1.1` 
		2. A status code - indicates success or failure, eg. 200, 201, 404 etc.
		3. A status message - a short description of the status code, eg. OK, CREATED etc.
	2. Response Headers (optional) - additional data for the response, the syntax is a case-insensitive string followed by a colon and the header value
2. Response Message Body / Payload (optional, separated from the Header by a blank line) - resource being fetched

![[HTTP_ResponseMessageExample.png]]

# HTTP request methods
## GET

The `GET` HTTP request method fetches data from a server. It is the most common HTTP request method.

It typically has no body.

It is a _safe_ method (it is read-only, does not change state in the server).

A successful GET request typically gets a response with a `200 OK` status code and .
A failed GET request typically gets a response with a `404 Not Found` status code.

Example of a GET request:

```HTTP
GET https://developer.mozilla.org/ HTTP/1.1
Accept-Language: en

```

>[!TIP] Entering a URL in the address bar of a browser performs a GET request.

## POST

The POST method sends a data to the server in order to create a new entry in a database.
It can be used to eg. create a new user profile, post a new message on a blog, submit data from a form etc.

It has a body.
It must include a header defining the content type of the body.

It is not a _safe_ method (it changes state in the server).

A successful POST request typically gets a response with a `201 Created` status code and the newly created resource as the response body.

```http
POST  http://localhost:8000 HTTP/1.1
content-type: application/json

    {
        "name": "John",
        "age": 30
    }
```

## PATCH

The PATCH method updates one or more fields of a data entity.

## DELETE

## HEAD

The HEAD method is similiar to the GET method, but a response to it does not include the payload. It is used to simply check the information about the payload without actually downloading it, because of eg. potential large filesize of the payload, which can be read out from the response headers.