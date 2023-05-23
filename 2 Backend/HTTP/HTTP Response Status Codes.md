# HTTP response status codes

reference: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status

Types of responses with some examples:
1.  Info responses 100-199
2. Success responses 200-299
	- __200 OK__ - successful request
	- __201 Created__ - successful POST/PUT request, new resource created
	- __202 Accepted__ - successful request, but not yet fulfilled. Occurs when a request is being fulfilled asynchronously and is yet to be fulfiled.
	- __204 No Content__ -  successful DELETE request
3. Redirection messages 300-399
	- **307 Temporary Redirect** - redirects to another URL, link equity is NOT passed along
	- **308 Permanent Redirect** - redirects to another URL, all link equity is passed along
4. Client error responses 400-499
	- __400 Bad Request__ - client error, the request should not be repeated without changes
	- __401 Unauthorized__ - user authentication needed
	- __403 Forbidden__ - the server has understood the request, but refused to fulfill it. The server should provide the reason for not fulfilling the request.
	- __404 Not Found__ - URL not found, server cannot find the resource (either permanently or temporarily)
	- __405 Method Not Allowed__ - the server does not allow the requested HTTP method on the given URL. The response must include an Allow header with allowed methods.
	- __410 Gone__ - the page is permanently unavailable, no redirect set up, dead resource
	- **422 Unprocessable Content** - eg. when a non-unique email address is POSTed
	- __429 Too Many Requests__ - occurs when requests are rate limited, happens when an API is accessed to often in a set span of time (eg. TMBD API limits requests to 50 per second)
1. Server error responses 500-599
	- __500 Internal Server Error__ - generic server error status
	- __501 Not Implemented__ - the server is unable to recognize the request, it does not support the functionality to fulfill the request.
	- __503 Sever Unavailable__ - the user/crawlbot is asked to come back later, the server is temporarily unavailable due to maintenance or overload