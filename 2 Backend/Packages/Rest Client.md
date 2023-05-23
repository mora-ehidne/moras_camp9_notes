# REST Client

The REST Client VSCode extension is used to send [[HTTP Messages - Requests and Responses#HTTP Request Structure|HTTP requests]] and receive [[HTTP Messages - Requests and Responses#HTTP Response Structure|HTTP responses]] to those requests.

The requests can be written in any file with an `.http` extension, from which they can be sent via the REST Client.

The requests must be separated with three hash symbols (`###`).

Example of a .http file that can be used with the REST Client:
```http

### 
GET http://localhost:8000/api/1.0/user/bookmarks HTTP/1.1
Cookie: token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOiIyYTQyMzNiYy02Yzg1LTRmN2UtYjQyZS1kODkyYjUxYTY2ZWQiLCJpYXQiOjE2ODQxMzgxNTEsImV4cCI6MTY4NDE0MTc1MX0.5AMXpfWc8Ul95vpgOmu-6mr1BgztEesU3WS8L5WnJ5c;

### 
POST http://localhost:8000/api/1.0/user/login HTTP/1.1
content-type: application/json

{
    "email": "echo@goo.com",
    "password": "echogoo"
}
```