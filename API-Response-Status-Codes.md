
# API Response codes

HTTP defines these standard status codes that can be  
used to convey the results of a client’s request. The status codes are divided into five categories.

* **1xx: Informational** – Communicates transfer protocol-level information.
* **2xx: Success** – Indicates that the client’s request was accepted successfully.
* **3xx: Redirection** – Indicates that the client must take some additional action in order to complete their request.
* **4xx: Client Error** – This category of error status codes points the finger at clients.
* **5xx: Server Error** – The server takes responsibility for these error status codes.




## Status Code Reference

### 2xx Status Codes [Success]

| Status Code | API Message | Description | Details |
| :-------- | :-------- | :------------------------- | :------------------------- |
| **`200`** | **`OK`** | Indicates that the request has succeeded. | Unlike the 204 status code, a 200 response should include a response body. The information returned with the response is dependent on the method used in the request |
| **`201`** | **`Created`** | Indicates that the request has succeeded and a new resource has been created as a result. | A REST API responds with the 201 status code whenever a resource is created inside a collection. There may also be times when a new resource is created as a result of some controller action, in which case 201 would also be an appropriate response. |
| **`204`** | **`No Content`** | Indicates that the request has succeeded. | The 204 status code is usually sent out in response to a PUT, POST, or DELETE request when the REST API declines to send back any status message or representation in the response message’s body. The 204 response MUST NOT include a message-body and thus is always terminated by the first empty line after the header fields. |

### 3xx Status Codes [Redirection]

| Status Code | API Message | Description | Details |
| :-------- | :-------- | :------------------------- | :------------------------- |
| **`302`** | **`Found`** | The URL of the requested resource has been changed temporarily. The new URL is given by the Location field in the response. This response is only cacheable if indicated by a Cache-Control or Expires header field. |
| **`304`** | **`Not Modified`** | Indicates the client that the response has not been modified, so the client can continue to use the same cached version of the response. | This status code is similar to 204 (“No Content”) in that the response body must be empty. The critical distinction is that 204 is used when there is nothing to send in the body, whereas 304 is used when the resource has not been modified since the version specified by the request headers If-Modified-Since or If-None-Match. |

### 4xx Status Codes (Client Error)

| Status Code | API Message | Description | Details |
| :-------- | :-------- | :------------------------- | :------------------------- |
| **`400`** | **`Bad Request`** | The request could not be understood by the server due to incorrect syntax. The client SHOULD NOT repeat the request without modifications. | 400 is the generic client-side error status, used when no other 4xx error code is appropriate. Errors can be like malformed request syntax, invalid request message parameters, or deceptive request routing etc. |
| **`401`** | **`Unauthorized`** | Indicates that the request requires user authentication information. The client MAY repeat the request with a suitable Authorization header field | A 401 error response indicates that the client tried to operate on a protected resource without providing the proper authorization. It may have provided the wrong credentials or none at all. The response must include a WWW-Authenticate header field containing a challenge applicable to the requested resource. |
| **`403`** | **`Forbidden`** | Unauthorized request. The client does not have access rights to the content. Unlike 401, the client’s identity is known to the server. | A 403 error response indicates that the client’s request is formed correctly, but the REST API refuses to honor it, i.e., the user does not have the necessary permissions for the resource. A 403 response is not a case of insufficient client credentials; that would be 401 (“Unauthorized”).Authentication will not help, and the request SHOULD NOT be repeated. Unlike a 401 Unauthorized response, authenticating will make no difference. | 
| **`404`** | **`No Content`** | The server can not find the requested resource. | The 404 error status code indicates that the REST API can’t map the client’s URI to a resource but may be available in the future. Subsequent requests by the client are permissible. This status code is commonly used when the server does not wish to reveal exactly why the request has been refused, or when no other response is applicable.|
| **`406`** | **`Not Acceptable`** | The server doesn’t find any content that conforms to the criteria given by the user agent in the Accept header sent in the request. | The 406 error response indicates that the API is not able to generate any of the client’s preferred media types, as indicated by the Accept request header. For example, a client request for data formatted as application/xml will receive a 406 response if the API is only willing to format data as application/json. If the response could be unacceptable, a user agent SHOULD temporarily stop receipt of more data and query the user for a decision on further actions. |

### 5xx Status Codes (Server Error)

| Status Code | API Message | Description | Details |
| :-------- | :-------- | :------------------------- | :------------------------- |
| **`500`** | **`Internal Server Error`** | The server encountered an unexpected condition that prevented it from fulfilling the request. | 500 is the generic REST API error response. Most web frameworks automatically respond with this response status code whenever they execute some request handler code that raises an exception. A 500 error is never the client’s fault, and therefore, it is reasonable for the client to retry the same request that triggered this response and hope to get a different response. The API response is the generic error message, given when an unexpected condition was encountered and no more specific message is suitable.|
| **`501`** | **`Not Implemented`** | The HTTP method is not supported by the server and cannot be handled. | The server either does not recognize the request method, or it cannot fulfill the request. Usually, this implies future availability (e.g., a new feature of a web-service API). |
| **`503`** | **`Service Unavailable`** | The server is not ready to handle the request. |


## Below are examples of common response structures for both error and success scenarios using JSON format. These examples follow a consistent format for clarity and ease of handling:

### Error Response Body:

```
{
  "error": {
    "code": "not_found",
    "message": "The requested resource could not be found.",
    "details": "Please check the resource ID and try again."
  }
}
```
* **error**: An object containing details about the error.
    * **code**: A machine-readable error code.
    * **message**: A human-readable summary of the error.
    * **details**: Additional details about the error, which may include specific information for debugging.

### Data Response Body:
```
{
  "data": {
    "message": "User successfully retrieved.",
    "user": {
      "id": 123,
      "name": "John Doe",
      "email": "john.doe@example.com"
    }
  }
}
```

* **data**: An object containing the successful response data.
    * **message**: A message indicating the success of the operation.
    * **user**: The requested user's information.

## Handling Both Success and Error in One Response:
#### Sometimes, it's useful to include a success or status field in your response to explicitly indicate success or failure. Here's an example that combines both success and error scenarios:

```
{
  "status": "success / fail",
  "data": {
    "message": "User successfully retrieved.",
    "user": {
      "id": 123,
      "name": "John Doe",
      "email": "john.doe@example.com"
    }
  }
}
```
```
{
  "status": "error",
  "error": {
    "code": "not_found",
    "message": "The requested resource could not be found.",
    "details": "Please check the resource ID and try again."
  }
}
```

#### When an API request is successful, and the expected result is an empty array, you can structure the response to include an empty array in the data field. Here's an example:

```
{
  "status": "success",
  "data": {
    "message": "Operation successful.",
    "result": []
  }
}
```
In this example
* **status**: Indicates the overall status of the response, in this case, "success."
* **data**: An object containing the successful response data.
    * **message**: A message indicating the success of the operation.
    * **result**: This field contains an empty array ([]) to represent the absence of specific data.

By using this approach, you maintain a consistent structure for your API responses, making it clear that the operation was successful even though there is no data in the array. It helps both developers and clients interpret the response consistently.

#### If the API request is successful and there is data, you can include the data in the result field within the data object. Here's an example with some data:
```
{
  "status": "success",
  "data": {
    "message": "Operation successful.",
    "result": [
      {
        "id": 1,
        "name": "Example 1",
        "description": "This is an example item."
      },
      {
        "id": 2,
        "name": "Example 2",
        "description": "Another example item."
      }
      // ... more items if applicable
    ]
  }
}
```
In this example:

* **status**: Indicates the overall status of the response, in this case, "success."
    * **data**: An object containing the successful response data.
    * **message**: A message indicating the success of the operation.
    * **result**: This field contains an array with specific data items.

This structure provides a clear indication of the success of the operation along with the actual data returned. It's a common and consistent way to handle successful responses with or without data.

By maintaining a consistent structure for both success and error responses, you make it easier for developers to handle responses programmatically and for clients to interpret the results. Additionally, including clear and informative messages helps in troubleshooting and understanding issues during development and integration.
