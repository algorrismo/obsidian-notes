An **HTTP status code** is a 3-digit number returned by a web server to indicate the result of an HTTP request.

### Common HTTP Status Code Categories

|Range|Meaning|
|---|---|
|**1xx**|Informational (request received)|
|**2xx**|Success|
|**3xx**|Redirection|
|**4xx**|Client error|
|**5xx**|Server error|

### Frequently Used Status Codes

#### Success (2xx)

- **200 OK** — Request succeeded.
    
- **201 Created** — Resource was successfully created.
    
- **204 No Content** — Request succeeded, but no content is returned.
    

#### Redirection (3xx)

- **301 Moved Permanently** — Resource has a new permanent URL.
    
- **302 Found** — Temporary redirect.
    
- **304 Not Modified** — Cached version is still valid.
    

#### Client Errors (4xx)

- **400 Bad Request** — Invalid request syntax.
    
- **401 Unauthorized** — Authentication required.
    
- **403 Forbidden** — Access denied.
    
- **404 Not Found** — Resource does not exist.
    
- **405 Method Not Allowed** — HTTP method not supported.
    
- **429 Too Many Requests** — Rate limit exceeded.
    

#### Server Errors (5xx)

- **500 Internal Server Error** — Generic server-side error.
    
- **502 Bad Gateway** — Invalid response from upstream server.
    
- **503 Service Unavailable** — Server temporarily unavailable.
    
- **504 Gateway Timeout** — Upstream server took too long to respond.
    

### Example

Request:

```http
GET /users/123 HTTP/1.1
Host: example.com
```

Response:

```http
HTTP/1.1 404 Not Found
Content-Type: application/json

{
  "error": "User not found"
}
```

Here, **404 Not Found** is the HTTP status code indicating that the requested resource could not be found.
