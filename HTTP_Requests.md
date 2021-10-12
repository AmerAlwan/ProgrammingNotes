# HTTP Requests

## What are HTTP Requests?

The internet boasts various resources hosted on different servers. These resources can be accessed when a browser sends requests to their servers. HTTP (Hypertext Transfer Protocol) is the format used to structure requests and responses for effective communication between a client and a server. 

The message that is sent by a client to a server is known as an HTTP request

### HTTP Request Methods

The assets that indicate the specific desired action to be performed on a given resource. 

An HTTP request is an action to be performed on a resource identified by a given request-URL. 

## How do HTTP Requests Work?

HTTP requests work as the intermediary transportation method between a client/application and a server.

The client submits an HTTP request to the server, and after internalizing the message, the server sends back a response, which contains status information about the request

## Types of HTTP Request Methods

### GET

Used to retrieve and request data from a specified resource in a server. Essentially, it is used to retrieve whatever information is identified by the Request-URL.

### POST

In web communication, POST requests are utilized to send data to a server to create or update a resource.

Is often used to send user-generated data to a server (Ex: When a user uploads a profile photo).

### PUT

Similar to POST as it is used to send data to the server to create or update a resource.

The difference is that PUT requests are idempotent, meaning that if you call the same PUT requests multiple times, the results will always be the same

## PUT vs POST 

Both are used to facilitate data transmission between a client and a server

| **PUT**                                                      | **POST**                                                     |
| :----------------------------------------------------------- | ------------------------------------------------------------ |
| Is idempotent, meaning that putting a resource twice will have no effect | Not idempotent, and thus calling a POT request repeatedly is discouraged |
| Identity is selected by the client                           | Identity is returned by the server                           |
| Operates as specific                                         | Operates as abstract                                         |

## GET vs POST

| **GET**                                                      | **POST**                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Parameters in this method are saved in the browser's history | Parameters are not archived in the browser history or other web server logs |
| Can be bookmarked                                            | Cannot be bookmarked                                         |
| Features a restriction on data length. This is because the GET method adds data to the URL for it to be sent, and we know the maximum URL length is 2048 characters | No restrictions on data length                               |
| There is no impact when you hit the reload/back button       | If reload/back buttons are pressed, sent data will be resubmitted |
| Has restrictions on data type as the only allowed data type is ASCII characters | No restrictions on data type, and binary data is also allowed |
| Information is visible to everyone in the URL                | Information is not displayed in the URL and thus is not visible to everyone |
| Can be cached                                                | Can't be cached                                              |

