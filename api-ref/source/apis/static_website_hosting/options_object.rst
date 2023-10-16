:original_name: obs_04_0078.html

.. _obs_04_0078:

OPTIONS Object
==============

Functions
---------

For details, see :ref:`OPTIONS Bucket <obs_04_0077>`.

Differences Between OPTIONS Bucket and OPTIONS Object
-----------------------------------------------------

With the OPTIONS Object, you need to specify an object name in the URL, but an object name is not required with the OPTIONS Bucket, which uses the bucket domain name as the URL. The request lines of the two methods are as follows:

.. code-block::

   OPTIONS /object HTTP/1.1

.. code-block::

   OPTIONS / HTTP/1.1

Request Syntax
--------------

::

   OPTIONS /object HTTP/1.1
   Host: bucketname.obs.region.example.com
   Date: date
   Authorization: authorization
   Origin: origin
   Access-Control-Request-Method: method

Request Parameters
------------------

This request contains no message parameters.

Request Headers
---------------

:ref:`Table 1 <obs_04_0078__table39180475205737>` describes headers used by this request.

.. _obs_04_0078__table39180475205737:

.. table:: **Table 1** OPTIONS request headers

   +--------------------------------+--------------------------------------------------------------------------------------------------------------+-----------------------+
   | Header                         | Description                                                                                                  | Mandatory             |
   +================================+==============================================================================================================+=======================+
   | Origin                         | Origin of the cross-domain request specified by the pre-request. Generally, it is a domain name set in CORS. | Yes                   |
   |                                |                                                                                                              |                       |
   |                                | Type: string                                                                                                 |                       |
   +--------------------------------+--------------------------------------------------------------------------------------------------------------+-----------------------+
   | Access-Control-Request-Method  | Indicates an HTTP method that can be used by a request. The request can use multiple method headers.         | Yes                   |
   |                                |                                                                                                              |                       |
   |                                | Type: string                                                                                                 |                       |
   |                                |                                                                                                              |                       |
   |                                | Value options: **GET**, **PUT**, **HEAD**, **POST**, **DELETE**                                              |                       |
   +--------------------------------+--------------------------------------------------------------------------------------------------------------+-----------------------+
   | Access-Control-Request-Headers | Indicates the HTTP headers of a request. The request can use multiple HTTP headers.                          | No                    |
   |                                |                                                                                                              |                       |
   |                                | Type: string                                                                                                 |                       |
   +--------------------------------+--------------------------------------------------------------------------------------------------------------+-----------------------+

Request Elements
----------------

This request involves no elements.

Response Syntax
---------------

::

   HTTP/1.1 status_code
   Content-Type: type
   Access-Control-Allow-Origin: origin
   Access-Control-Allow-Methods: method
   Access-Control-Allow-Header: header
   Access-Control-Max-Age: time
   Access-Control-Expose-Headers: header
   Date: date
   Content-Length: length

Response Headers
----------------

The request uses the headers described in :ref:`Table 2 <obs_04_0078__table14690348205823>`.

.. _obs_04_0078__table14690348205823:

.. table:: **Table 2** CORS request headers

   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
   | Header                            | Description                                                                                                                                    |
   +===================================+================================================================================================================================================+
   | Access-Control-Allow-Origin       | If the origin of a request meets server CORS configuration requirements, the response contains the origin.                                     |
   |                                   |                                                                                                                                                |
   |                                   | Type: string                                                                                                                                   |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access-Control-Allow-Headers      | If the headers of a request meet server CORS configuration requirements, the response contains the headers.                                    |
   |                                   |                                                                                                                                                |
   |                                   | Type: string                                                                                                                                   |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access-Control-Max-Age            | Value of MaxAgeSeconds in the CORS configuration of a server.                                                                                  |
   |                                   |                                                                                                                                                |
   |                                   | Type: integer                                                                                                                                  |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access-Control-Allow-Methods      | If the Access-Control-Request-Method of a request meets server CORS configuration requirements, the response contains the methods in the rule. |
   |                                   |                                                                                                                                                |
   |                                   | Type: string                                                                                                                                   |
   |                                   |                                                                                                                                                |
   |                                   | Value options: **GET**, **PUT**, **HEAD**, **POST**, **DELETE**                                                                                |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access-Control-Expose-Headers     | Indicates ExposeHeader in the CORS configuration of a server.                                                                                  |
   |                                   |                                                                                                                                                |
   |                                   | Type: string                                                                                                                                   |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+

Response Elements
-----------------

This response contains no elements.

Error Responses
---------------

:ref:`Table 3 <obs_04_0078__table38908138205823>` describes possible special errors in the request.

.. _obs_04_0078__table38908138205823:

.. table:: **Table 3** Special error

   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Error Code            | Description                                                                                                                                                                                                                       | HTTP Status Code      |
   +=======================+===================================================================================================================================================================================================================================+=======================+
   | Bad Request           | Invalid Access-Control-Request-Method: null                                                                                                                                                                                       | 400 BadRequest        |
   |                       |                                                                                                                                                                                                                                   |                       |
   |                       | When CORS and OPTIONS are configured for a bucket, no method header is added.                                                                                                                                                     |                       |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Bad Request           | Insufficient information. Origin request header needed.                                                                                                                                                                           | 400 BadRequest        |
   |                       |                                                                                                                                                                                                                                   |                       |
   |                       | When CORS and OPTIONS are configured for a bucket, no origin header is added.                                                                                                                                                     |                       |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | AccessForbidden       | CORSResponse: This CORS request is not allowed. This is usually because the evaluation of Origin, request method/Access-Control-Request-Method or Access-Control-Request-Headers are not whitelisted by the resource's CORS spec. | 403 Forbidden         |
   |                       |                                                                                                                                                                                                                                   |                       |
   |                       | When CORS and OPTIONS are configured for a bucket, origin, method, and headers do not match any rule.                                                                                                                             |                       |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

For other errors, see :ref:`Table 2 <obs_04_0115__d0e843>`.

Sample Request
--------------

::

   OPTIONS /object_1 HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: WED, 01 Jul 2015 04:02:19 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:bQZG9c2aokAJsHOOkuVBK6cHZZQ=
   Origin: www.example.com
   Access-Control-Request-Method: PUT

Sample Response
---------------

::

   HTTP/1.1 200 OK
   Server: OBS
   x-obs-request-id: BF26000001643632D12EFCE1C1294555
   Access-Control-Allow-Origin: www.example.com
   Access-Control-Allow-Methods: POST,GET,HEAD,PUT,DELETE
   Access-Control-Max-Age: 100
   Access-Control-Expose-Headers: ExposeHeader_1,ExposeHeader_2
   Access-Control-Allow-Credentials: true
   x-obs-id-2: 32AAAQAAEAABAAAQAAEAABAAAQAAEAABCS+DXV4zZetbTqFehhEcuXywTa/mi3T3
   Date: WED, 01 Jul 2015 04:02:19 GMT
   Content-Length: 0
