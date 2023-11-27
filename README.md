
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

| Status Code | API Message | Description                |
| :-------- | :-------- | :------------------------- |
| **`200`** | **`OK`** | Indicates that the request has succeeded. |
| **`201`** | **`Created`** | Indicates that the request has succeeded and a new resource has been created as a result. |
| **`204`** | **`No Content`** | Indicates that the request has succeeded. |

### 3xx Status Codes [Redirection]

| Status Code | API Message | Description                |
| :-------- | :-------- | :------------------------- |
| **`300`** | **`Multiple Choices`** | The request has more than one possible response. The user-agent  or user should choose one of them. |
| **`302`** | **`Found`** | The URL of the requested resource has been changed temporarily. The new URL is given by the Location field in the response. This response is only cacheable if indicated by a Cache-Control or Expires header field. |
| **`304`** | **`Not Modified`** | Indicates the client that the response has not been modified, so the client can continue to use the same cached version of the response. |

### 4xx Status Codes (Client Error)

| Status Code | API Message | Description | Details |
| :-------- | :-------- | :------------------------- | :------------------------- |
| **`400`** | **`Bad Request`** | The request could not be understood by the server due to incorrect syntax. The client SHOULD NOT repeat the request without modifications. | 400 is the generic client-side error status, used when no other 4xx error code is appropriate. Errors can be like malformed request syntax, invalid request message parameters, or deceptive request routing etc. |
| **`401`** | **`Unauthorized`** | Indicates that the request requires user authentication information. The client MAY repeat the request with a suitable Authorization header field |
| **`403`** | **`Forbidden`** | Unauthorized request. The client does not have access rights to the content. Unlike 401, the client’s identity is known to the server. |
| **`404`** | **`No Content`** | The server can not find the requested resource. |
| **`406`** | **`Not Acceptable`** | The server doesn’t find any content that conforms to the criteria given by the user agent in the Accept header sent in the request. |

### 5xx Status Codes (Server Error)

| Status Code | API Message | Description                |
| :-------- | :-------- | :-------------------------- |
| **`500`** | **`Internal Server Error`** | The server encountered an unexpected condition that prevented it from fulfilling the request. |
| **`501`** | **`Not Implemented`** | The HTTP method is not supported by the server and cannot be handled. |
| **`503`** | **`Service Unavailable`** | The server is not ready to handle the request. |



