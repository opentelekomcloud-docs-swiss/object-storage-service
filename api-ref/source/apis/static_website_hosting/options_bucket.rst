:original_name: obs_04_0077.html

.. _obs_04_0077:

OPTIONS Bucket
==============

Functions
---------

OPTIONS refers to pre-requests that are sent to servers by clients. Generally, the requests are used to check whether clients have permissions to perform operations on servers. Only after a pre-request is returned successfully, clients start to execute the follow-up requests.

The OBS allows buckets to store static web resources. OBS buckets can serve as website resources if the buckets are properly used. In this scenario, buckets in the OBS serve as servers to process OPTIONS pre-requests from clients.

OBS can process OPTIONS pre-requests only after CORS is configured for buckets in OBS. For details about CORS, see :ref:`Configuring Bucket CORS <obs_04_0074>`.

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

   OPTIONS / HTTP/1.1
   Host: bucketname.obs.region.example.com
   Date: date
   Authorization: authorization
   Origin: origin
   Access-Control-Request-Method: method

Request Parameters
------------------

This request contains no parameter.

Request Headers
---------------

This request uses the headers described in :ref:`Table 1 <obs_04_0077__table2585568620633>`.

.. _obs_04_0077__table2585568620633:

.. table:: **Table 1** OPTIONS request headers

   +--------------------------------+--------------------------------------------------------------------------------------------------------------+-----------------------+
   | Header                         | Description                                                                                                  | Mandatory             |
   +================================+==============================================================================================================+=======================+
   | Origin                         | Origin of the cross-domain request specified by the pre-request. Generally, it is a domain name set in CORS. | Yes                   |
   |                                |                                                                                                              |                       |
   |                                | Type: string                                                                                                 |                       |
   +--------------------------------+--------------------------------------------------------------------------------------------------------------+-----------------------+
   | Access-Control-Request-Method  | An HTTP method that can be used by a request. The request can use multiple method headers.                   | Yes                   |
   |                                |                                                                                                              |                       |
   |                                | Type: string                                                                                                 |                       |
   |                                |                                                                                                              |                       |
   |                                | Possible values are GET, PUT, HEAD, POST, and DELETE.                                                        |                       |
   +--------------------------------+--------------------------------------------------------------------------------------------------------------+-----------------------+
   | Access-Control-Request-Headers | HTTP headers of a request. The request can use multiple HTTP headers.                                        | No                    |
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
   Content-Type: application/xml
   Access-Control-Allow-Origin: origin
   Access-Control-Allow-Methods: method
   Access-Control-Allow-Header: header
   Access-Control-Max-Age: time
   Access-Control-Expose-Headers: header
   Date: date
   Content-Length: length

Response Headers
----------------

The response uses the following headers as described in :ref:`Table 2 <obs_04_0077__table40550587202855>`.

.. _obs_04_0077__table40550587202855:

.. table:: **Table 2** CORS response headers

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
   | Access-Control-Max-Age            | Value of MaxAgeSeconds in the CORS configuration of a server                                                                                   |
   |                                   |                                                                                                                                                |
   |                                   | Type: integer                                                                                                                                  |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access-Control-Allow-Methods      | If the Access-Control-Request-Method of a request meets server CORS configuration requirements, the response contains the methods in the rule. |
   |                                   |                                                                                                                                                |
   |                                   | Type: string                                                                                                                                   |
   |                                   |                                                                                                                                                |
   |                                   | Possible values are GET, PUT, HEAD, POST, and DELETE.                                                                                          |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access-Control-Expose-Headers     | Value of ExposeHeader in the CORS configuration of a server                                                                                    |
   |                                   |                                                                                                                                                |
   |                                   | Type: string                                                                                                                                   |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+

Response Elements
-----------------

This response involves no elements.

Error Responses
---------------

:ref:`Table 3 <obs_04_0077__table1322139420210>` describes possible special errors in the request.

.. _obs_04_0077__table1322139420210:

.. table:: **Table 3** Special error

   +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Error Code            | Description                                                                                                                                                                                                                                  | HTTP Status Code      |
   +=======================+==============================================================================================================================================================================================================================================+=======================+
   | Bad Request           | Invalid Access-Control-Request-Method: null                                                                                                                                                                                                  | 400 BadRequest        |
   |                       |                                                                                                                                                                                                                                              |                       |
   |                       | When CORS and OPTIONS are configured for a bucket, no method header is added.                                                                                                                                                                |                       |
   +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Bad Request           | Insufficient information. Origin request header needed.                                                                                                                                                                                      | 400 BadRequest        |
   |                       |                                                                                                                                                                                                                                              |                       |
   |                       | When CORS and OPTIONS are configured for a bucket, no origin header is added.                                                                                                                                                                |                       |
   +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | AccessForbidden       | CORSResponse: This CORS request is not allowed. This is usually because the evaluation of Origin, request method / Access-Control-Request-Method or Access-Control-Request-Headers are not whitelisted by the resource's CORS specification. | 403 Forbidden         |
   |                       |                                                                                                                                                                                                                                              |                       |
   |                       | When CORS and OPTIONS are configured for a bucket, origin, method, and headers do not match any rule.                                                                                                                                        |                       |
   +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

For other errors, see :ref:`Table 2 <obs_04_0115__d0e843>`.

Sample Request
--------------

::

   OPTIONS / HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: WED, 01 Jul 2015 04:02:15 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:7RqP1vjemo6U+Adv9/Y6eGzWrzA=
   Origin: www.example.com
   Access-Control-Request-Method: PUT

Sample Response
---------------

::

   HTTP/1.1 200 OK
   Server: OBS
   x-obs-request-id: BF260000016436314E8FF936946DBC9C
   Access-Control-Allow-Origin: www.example.com
   Access-Control-Allow-Methods: POST,GET,HEAD,PUT,DELETE
   Access-Control-Max-Age: 100
   Access-Control-Expose-Headers: ExposeHeader_1,ExposeHeader_2
   Access-Control-Allow-Credentials: true
   x-obs-id-2: 32AAAQAAEAABAAAQAAEAABAAAQAAEAABCTlYimJvOyJncCLNm5y/iz6MAGLNxTuS
   Date: WED, 01 Jul 2015 04:02:15 GMT
   Content-Length: 0
