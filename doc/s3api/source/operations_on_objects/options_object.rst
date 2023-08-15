:original_name: en-us_topic_0125560261.html

.. _en-us_topic_0125560261:

OPTIONS Object
==============

For details, see section :ref:`OPTIONS Bucket <en-us_topic_0125560464>`.

Request Syntax
--------------

.. code-block::

   OPTIONS /object HTTP/1.1
    User-Agent: agent
    Host: bucketname.obs.example.com
    Accept: */*
    Date: date
    Authorization: authorization
    Origin: origin
    Access-Control-Request-Method: method

Request Parameters
------------------

This request involves no parameters.

Request Headers
---------------

:ref:`Table 1 <en-us_topic_0125560261__table58188993>` lists the request headers.

.. _en-us_topic_0125560261__table58188993:

.. table:: **Table 1** OPTIONS request headers

   +--------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | Header                         | Description                                                                                                                                                                        | Remarks                                                                          |
   +================================+====================================================================================================================================================================================+==================================================================================+
   | Origin                         | Indicates an origin specified by a pre-request. Generally, it is a domain name.                                                                                                    | Mandatory                                                                        |
   |                                |                                                                                                                                                                                    |                                                                                  |
   |                                | Type: String                                                                                                                                                                       |                                                                                  |
   +--------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | Access-Control-Request-Method  | Indicates an HTTP method that can be used by a request. The request can use multiple method headers.                                                                               | Mandatory                                                                        |
   |                                |                                                                                                                                                                                    |                                                                                  |
   |                                | Type: String                                                                                                                                                                       |                                                                                  |
   |                                |                                                                                                                                                                                    |                                                                                  |
   |                                | Valid values: **GET**, **PUT**, **HEAD**, **POST**, and **DELETE**                                                                                                                 |                                                                                  |
   +--------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | Access-Control-Request-Headers | Indicates the HTTP headers of a request. The request can use multiple HTTP headers.                                                                                                | Optional                                                                         |
   |                                |                                                                                                                                                                                    |                                                                                  |
   |                                | Type: String                                                                                                                                                                       |                                                                                  |
   +--------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | x-amz-security-token           | Header field used to identify the request of a federated user. When the federal authentication function is enabled, users sending such requests are identified as federated users. | Optional. This parameter must be carried in the request sent by federated users. |
   |                                |                                                                                                                                                                                    |                                                                                  |
   |                                | Type: string                                                                                                                                                                       |                                                                                  |
   +--------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+

Request Elements
----------------

This request involves no elements.

Response Syntax
---------------

.. code-block::

   HTTP/1.1 status_code
    Server: server
    x-amz-request-id: request id
    x-amz-id-2: id
    Content-Type: type
    Access-Control-Allow-Origin: origin
    Access-Control-Allow-Methods: method
    Access-Control-Allow-Header: header
    Access-Control-Max-Age: seconds
    Access-Control-Expose-Headers: header
    Date: date
    Content-Length: length

Response Headers
----------------

:ref:`Table 2 <en-us_topic_0125560261__table47822814>` lists the request headers.

.. _en-us_topic_0125560261__table47822814:

.. table:: **Table 2** CORS request headers

   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | Header                            | Description                                                                                                                                        |
   +===================================+====================================================================================================================================================+
   | Access-Control-Allow-Origin       | If the origin of a request meets server CORS configuration requirements, the response contains the origin.                                         |
   |                                   |                                                                                                                                                    |
   |                                   | Type: String                                                                                                                                       |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access-Control-Allow-Headers      | If the headers of a request meet server CORS configuration requirements, the response contains the headers.                                        |
   |                                   |                                                                                                                                                    |
   |                                   | Type: String                                                                                                                                       |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access-Control-Max-Age            | Indicates **MaxAgeSeconds** in the CORS configuration of a server.                                                                                 |
   |                                   |                                                                                                                                                    |
   |                                   | Type: Integer                                                                                                                                      |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access-Control-Allow-Methods      | If the **Access-Control-Request-Method** of a request meets server CORS configuration requirements, the response contains the methods in the rule. |
   |                                   |                                                                                                                                                    |
   |                                   | Type: String                                                                                                                                       |
   |                                   |                                                                                                                                                    |
   |                                   | Valid values: **GET**, **PUT**, **HEAD**, **POST**, and **DELETE**                                                                                 |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access-Control-Expose-Headers     | Indicates **ExposeHeader** in the CORS configuration of a server.                                                                                  |
   |                                   |                                                                                                                                                    |
   |                                   | Type: String                                                                                                                                       |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+

Response Elements
-----------------

This response involves no elements.

Error Responses
---------------

:ref:`Table 3 <en-us_topic_0125560261__table27752149>` describes possible special errors in the request.

.. _en-us_topic_0125560261__table27752149:

.. table:: **Table 3** Special errors

   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Error Code            | Description                                                                                                                                                                                                                         | HTTP Status Code      |
   +=======================+=====================================================================================================================================================================================================================================+=======================+
   | Bad Request           | Invalid Access-Control-Request-Method: null                                                                                                                                                                                         | 400 Bad Request       |
   |                       |                                                                                                                                                                                                                                     |                       |
   |                       | When CORS and OPTIONS are configured for a bucket, no method header is added.                                                                                                                                                       |                       |
   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Bad Request           | Insufficient information. Origin request header needed.                                                                                                                                                                             | 400 Bad Request       |
   |                       |                                                                                                                                                                                                                                     |                       |
   |                       | When CORS and OPTIONS are configured for a bucket, no origin header is added.                                                                                                                                                       |                       |
   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | AccessForbidden       | CORSResponse: This CORS request is not allowed. This is usually because the evaluation of Origin, request method / Access-Control-Request-Method or Access-Control-Request-Headers are not whitelisted by the resource's CORS spec. | 403 Forbidden         |
   |                       |                                                                                                                                                                                                                                     |                       |
   |                       | When CORS and OPTIONS are configured for a bucket, origin, method, and headers do not match any rule.                                                                                                                               |                       |
   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

For details about other errors, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`.

Sample Request
--------------

.. code-block::

   OPTIONS /object HTTP/1.1
    User-Agent: curl/7.19.0 (x86_64-suse-linux-gnu) libcurl/7.19.0 OpenSSL/0.9.8{ zlib/1.2.3 libidn/1.10
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Tue, 28 Apr 2015 12:44:17 +0000
    Authorization: AWS D13E0C94E722DD69423C:9U2ZGZebzPsbjsbxd6Qx1552LCI=
    Origin:www.example.com
    Access-Control-Request-Method:HEAD
    Access-Control-Request-Headers:acc_header_1
    Access-Control-Request-Headers:acc_header_2

Sample Response
---------------

.. code-block::

   HTTP/1.1 200 OK
    Server: OBS
    x-amz-request-id: EB916A17C4CA9863E10CB3875D12D921
    x-amz-id-2: xuXo/62YzJOvNjQ3179xVyqlTSY8cWbI/EBDbKmhEoqdvKw7bU4KwFzeBX9oq212
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Content-Type: text/xml
    Access-Control-Allow-Origin: www.example.com
    Access-Control-Allow-Methods: POST,GET,HEAD,PUT
    Access-Control-Allow-Headers: acc_header_1,acc_header_2
    Access-Control-Max-Age: 100
    Access-Control-Expose-Headers: exp_header_1
    Date: Tue, 28 Apr 2015 12:46:56 GMT
    Content-Length: 0
