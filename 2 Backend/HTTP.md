# HTTP request methods
## GET

The `GET` HTTP request method fetches data from a server.
Entering a URL in the address bar of a browser performs a GET request.

## POST
## PATCH

Updates one or more fields of a data entity.

## DELETE

# HTTP response status codes

reference: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status

Types of responses with some examples:
1.  Info responses 100-199
2. Success responses 200-299
	- __200 OK__ - successful request
	- __201 Created__ - successful POST request, new resource created
	- __204 No Content__ -  successful DELETE request
3. Redirection messages 300-399
4. Client error responses 400-499
	- __400 Bad Request__ - client error
	- __404 Not Found__ - URL not found, server cannot find the resource
	- **422 Unprocessable Content** - eg. when a non-unique email address is POSTed
1. Server error responses 500-599
	- __500 Internal Server Error__ - generic server error status