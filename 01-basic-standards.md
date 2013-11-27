# 1. Basic standards

All the Visipedia API is accessed over HTTPS. The Visipedia system consists of multiple *internal* applications. Each application takes care of it's part of the API and the calls are made to `<app-name>.visipedia.org/api`.

> TODO: This is still subject to discuss whether it is better to use `<app-name>.visipedia.org/api` or `api.visipedia.org/<app-name>`.

## 1.1 Requests
Request and responses are standard HTTP messages.

### Requests without body (GET)
The `GET` requests don't have any body with data. The simplest `GET` request may look as follows:

```http
GET / HTTP/1.1
Host: api.visipedia.org
```

Usually we need to pass some parameters with the `GET` request. Some parameters are passed in the path - `GET /vibe/param`, additional parameters are passed in the query string - `GET /vibe/param?additional=true`.


### Request with body (POST, PATCH, PUT, DELETE)
All the data in the request body is JSON endoded. The simplest request with body may look as follows:

```http
POST / HTTP/1.1
Host: api.visipedia.org
Content-Length: 2

{}
```

### Requests with files
The only requests that don't have purely-JSON body are request transferring files. Such request must go with content type `multipart/form-data` and must contain at least one file part. No file part can be named `data`.

Any additional data is JSON encoded and stored in a `data` field. The `data` field is not mandatory.

A request with file may look as follows:

```http
POST / HTTP/1.1
Host: api.visipedia.org
Content-Type: multipart/form-data; boundary=<boundary>
Content-Length: <length>

--<boundary>
Content-Disposition: form-data; name="file"; filename="image.jpg"
Content-Type: image/jpeg

<image-data>
--<boundary>
Content-Disposition: form-data; name="data"

{}
--<boundary>--
```

## 1.2 Responses
Response uses the HTTP status code to inform about the state of the action.

### Successful responses
A successful response goes with `200 OK` status code and always contains a JSON object as a body. The smallest possible response is...

### Client errors
Visipedia API returns three types of errors:

1. Invalid body format (when the body is not JSON):

```http
HTTP/1.1 400 Bad Request
Content-Length: 35

{"message":"Problems parsing JSON"}
```

2. Invalid types in JSON values:

```http
HTTP/1.1 400 Bad Request
Content-Length: 40

{"message":"Body should be a JSON Hash"}
```

3. Invalid fields in JSON:

## 1.3 Versioning
All the API request must specify the API version. This is done by including the `X-Visipedia-Version` header. For the `alpha1` an example of a `GET` request should look as follows:

```http
GET / HTTP/1.1
Host: api.visipedia.org
X-Visipedia-Version: alpha1
```

It the version header is not specified in the request an error response will be returned:

## 1.4 Authentication:
Requests to the parts of the API that require authentication and authorization must include the `Authorization` header containing an Oauth2 access token according to the [RFC 6750](http://tools.ietf.org/html/rfc6750). An example of a `GET` request with acces token may look as follows:

```http
GET / HTTP/1.1
Host: api.visipedia.org
Authorization: Bearer <access-token>
```

To read more on how to obtain the OAuth2 access token see section...
