:original_name: en-us_topic_0125560464.html

.. _en-us_topic_0125560464:

OPTIONS Bucket
==============

**OPTIONS** refers to pre-requests that are sent to servers by clients. Generally, you can use these requests to check whether clients have permission to perform operations on servers. Only after a pre-request is returned successfully, clients start to execute the follow-up requests.

OBS allows buckets to store static web resources. The buckets of OBS can serve as website resources if the buckets are properly used. In this scenario, buckets in OBS serve as servers to process **OPTIONS** pre-requests from clients.

OBS can process **OPTIONS** pre-requests only after CORS is configured for buckets in OBS. For details about CORS, see section :ref:`PUT Bucket CORS <en-us_topic_0125560238>`.

Request Syntax
--------------

.. code-block::

   OPTIONS / HTTP/1.1
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

:ref:`Table 1 <en-us_topic_0125560464__table57465365>` lists the request headers.

.. _en-us_topic_0125560464__table57465365:

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
    x-amz-request-id: request id
    x-amz-id-2: id
    Access-Control-Allow-Origin: origin
    Access-Control-Allow-Methods: method
    Access-Control-Allow-Header: header
    Access-Control-Max-Age: seconds
    Access-Control-Expose-Headers: header
    Date: date
    Content-Length: length

Response Headers
----------------

:ref:`Table 2 <en-us_topic_0125560464__table7221243>` lists the response headers.

.. _en-us_topic_0125560464__table7221243:

.. table:: **Table 2** CORS response headers

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

For details about other errors, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`. In addition, this response also may contain special errors, as described in :ref:`Table 3 <en-us_topic_0125560464__table64991193>`.

.. _en-us_topic_0125560464__table64991193:

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

Sample Request
--------------

.. code-block::

   OPTIONS / HTTP/1.1
    User-Agent: curl/7.19.0 (x86_64-suse-linux-gnu) libcurl/7.19.0 OpenSSL/0.9.8{ zlib/1.2.3 libidn/1.10
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Tue, 28 Apr 2015 12:43:15 +0000
    Authorization: AWS D13E0C94E722DD69423C:02VOjl2Z5B7mUd+G6zr0Dql5CW8=
    Origin:www.example.com
    Access-Control-Request-Method:HEAD
    Access-Control-Request-Headers:acc_header_1
    Access-Control-Request-Headers:acc_header_2

Sample Response
---------------

.. code-block::

   HTTP/1.1 200 OK
    x-amz-request-id: 0350FC4D73DDA0D3A6FC2CBE01A7943A
    x-amz-id-2: ANHl/5gbYTwbfQat5+QZpWdnuE5DV83RXCyGZgBrbDVzVtdtGkqb9ZOepAX3Yr/z
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Access-Control-Allow-Origin: www.example.com
    Access-Control-Allow-Methods: POST,GET,HEAD,PUT
    Access-Control-Allow-Headers: acc_header_1,acc_header_2
    Access-Control-Max-Age: 100
    Access-Control-Expose-Headers: exp_header_1
    Date: Tue, 28 Apr 2015 12:45:34 GMT
    Content-Length: 0
