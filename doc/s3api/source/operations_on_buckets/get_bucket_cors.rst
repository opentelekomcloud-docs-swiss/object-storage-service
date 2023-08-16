:original_name: en-us_topic_0125560258.html

.. _en-us_topic_0125560258:

GET Bucket CORS
===============

You can use this operation to obtain CORS configuration information about a specified bucket.

Only users granted the **s3:GetBucketCORS** permission can perform this operation. By default, only the bucket owner can perform this operation. The bucket owner can allow other users to perform this operation by granting them the permission.

Request Syntax
--------------

.. code-block::

    GET /?cors HTTP/1.1
    User-Agent: agent
    Host: bucketname.obs.example.com
    Accept: */*
    Date: date
    Authorization: authorization

Request Parameters
------------------

This request involves no parameters.

Request Headers
---------------

This request uses common headers. For details about common request headers, see section :ref:`Common Request Headers <en-us_topic_0125560462>`.

Request Elements
----------------

This request involves no elements.

Response Syntax
---------------

.. code-block::

   HTTP/1.1 status_code
    Server: Server Name
    x-amz-request-id: id
    x-amz-id-2: id
    x-reserved: reserved info
    Content-Type: type
    Date: date
    Content-Length: lenth

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <CORSConfiguration xmlns="http://obs.example.com/doc/2015-06-30/">
      <CORSRule>
        ...
      </CORSRule>
    </CORSConfiguration>

Response Headers
----------------

This response uses common headers. For details about common response headers, see section :ref:`Common Response Headers <en-us_topic_0125560484>`.

Response Elements
-----------------

This response contains elements to detail the CORS configuration. :ref:`Table 1 <en-us_topic_0125560258__table34893051>` describes the elements.

.. _en-us_topic_0125560258__table34893051:

.. table:: **Table 1** CORS configuration elements

   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Element                           | Description                                                                                                                                                                                                                                                                                                           |
   +===================================+=======================================================================================================================================================================================================================================================================================================================+
   | CORSConfiguration                 | Indicates the **CORSRules** root node. The maximum size is 64 KB.                                                                                                                                                                                                                                                     |
   |                                   |                                                                                                                                                                                                                                                                                                                       |
   |                                   | Type: Container                                                                                                                                                                                                                                                                                                       |
   |                                   |                                                                                                                                                                                                                                                                                                                       |
   |                                   | Ancestor: None                                                                                                                                                                                                                                                                                                        |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | CORSRule                          | Indicates a CORS rule. **CORSConfiguration** can contain a maximum of 100 rules.                                                                                                                                                                                                                                      |
   |                                   |                                                                                                                                                                                                                                                                                                                       |
   |                                   | Type: Container                                                                                                                                                                                                                                                                                                       |
   |                                   |                                                                                                                                                                                                                                                                                                                       |
   |                                   | Ancestor: **CORSConfiguration**                                                                                                                                                                                                                                                                                       |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ID                                | Indicates the unique identifier of a rule. The value can contain a maximum of 255 characters.                                                                                                                                                                                                                         |
   |                                   |                                                                                                                                                                                                                                                                                                                       |
   |                                   | Type: String                                                                                                                                                                                                                                                                                                          |
   |                                   |                                                                                                                                                                                                                                                                                                                       |
   |                                   | Ancestor: Rule                                                                                                                                                                                                                                                                                                        |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | AllowedMethod                     | Indicates a method that is allowed by a CORS rule.                                                                                                                                                                                                                                                                    |
   |                                   |                                                                                                                                                                                                                                                                                                                       |
   |                                   | Type: String                                                                                                                                                                                                                                                                                                          |
   |                                   |                                                                                                                                                                                                                                                                                                                       |
   |                                   | Valid values: **GET**, **PUT**, **HEAD**, **POST**, and **DELETE**                                                                                                                                                                                                                                                    |
   |                                   |                                                                                                                                                                                                                                                                                                                       |
   |                                   | Ancestor: Rule                                                                                                                                                                                                                                                                                                        |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | AllowedOrigin                     | Indicates an origin that is allowed by a CORS rule. It is a character string and can contain a wildcard (``*``). Each **AllowedOrigin** can only contain one wildcard (``*``).                                                                                                                                        |
   |                                   |                                                                                                                                                                                                                                                                                                                       |
   |                                   | Type: String                                                                                                                                                                                                                                                                                                          |
   |                                   |                                                                                                                                                                                                                                                                                                                       |
   |                                   | Ancestor: Rule                                                                                                                                                                                                                                                                                                        |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | AllowedHeader                     | Indicates an allowed header (**Access-Control-Request-Headers**) in a CORS request. If a request contains **Access-Control-Request-Headers**, only a CORS request that matches the configuration of **AllowedHeader** is considered as a valid request. Each **AllowedHeader** can only contain one wildcard (``*``). |
   |                                   |                                                                                                                                                                                                                                                                                                                       |
   |                                   | Type: String                                                                                                                                                                                                                                                                                                          |
   |                                   |                                                                                                                                                                                                                                                                                                                       |
   |                                   | Ancestor: Rule                                                                                                                                                                                                                                                                                                        |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | MaxAgeSeconds                     | Indicates the response time of the CORS that can be cached by a server. It is expressed in seconds.                                                                                                                                                                                                                   |
   |                                   |                                                                                                                                                                                                                                                                                                                       |
   |                                   | Each **CORSRule** can contain only one **MaxAgeSeconds**. It can be set to a negative value.                                                                                                                                                                                                                          |
   |                                   |                                                                                                                                                                                                                                                                                                                       |
   |                                   | Type: Integer                                                                                                                                                                                                                                                                                                         |
   |                                   |                                                                                                                                                                                                                                                                                                                       |
   |                                   | Ancestor: Rule                                                                                                                                                                                                                                                                                                        |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ExposeHeader                      | Indicates a supplemented header in CORS responses. The header provides additional information for servers. It cannot contain spaces.                                                                                                                                                                                  |
   |                                   |                                                                                                                                                                                                                                                                                                                       |
   |                                   | Type: String                                                                                                                                                                                                                                                                                                          |
   |                                   |                                                                                                                                                                                                                                                                                                                       |
   |                                   | Ancestor: Rule                                                                                                                                                                                                                                                                                                        |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Error Responses
---------------

For details about other error responses, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`. In addition, this response contains one special error, as described in :ref:`Table 2 <en-us_topic_0125560258__table45602007>`.

.. _en-us_topic_0125560258__table45602007:

.. table:: **Table 2** Special error

   +-------------------------+------------------------------------------------------------------+------------------+
   | Error Code              | Description                                                      | HTTP Status Code |
   +=========================+==================================================================+==================+
   | NoSuchCORSConfiguration | Indicates that the CORS configuration of buckets does not exist. | 404 Not Found    |
   +-------------------------+------------------------------------------------------------------+------------------+

Sample Request
--------------

.. code-block:: text

   GET /?cors HTTP/1.1
    User-Agent: curl/7.19.0 (x86_64-suse-linux-gnu) libcurl/7.19.0 OpenSSL/0.9.8{ zlib/1.2.3 libidn/1.10
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Tue, 28 Apr 2015 09:11:35 +0000
    Authorization: AWS D13E0C94E722DD69423C:FJt2xJ1gEnozLSdpRNTJUoy6344=

Sample Response
---------------

.. code-block::

   HTTP/1.1 200 OK
    Server: OBS
    x-amz-request-id: C2D7CDD617B33354C3AA227BF2077071
    x-amz-id-2: xO3n8Q4eiJKCeAtG6U4nCSnDzhbBbMhgln8fcrOFYVGRJMc8KK/puQyr5bbSdjBU
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Content-Type: application/xml
    Date: Tue, 28 Apr 2015 09:11:35 GMT
    Content-Length: 556

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <CORSConfiguration xmlns="http://obs.example.com/doc/2015-06-30/">
        <CORSRule>
            <AllowedMethod>POST</AllowedMethod>
            <AllowedMethod>GET</AllowedMethod>
            <AllowedMethod>HEAD</AllowedMethod>
            <AllowedMethod>PUT</AllowedMethod>
            <AllowedMethod>DELETE</AllowedMethod>
            <AllowedOrigin>obs.example.com</AllowedOrigin>
            <AllowedOrigin>www.example.com</AllowedOrigin>
            <AllowedHeader>AllowedHeader_1</AllowedHeader>
            <AllowedHeader>AllowedHeader_2</AllowedHeader>
            <MaxAgeSeconds>100</MaxAgeSeconds>
            <ExposeHeader>ExposeHeader_1</ExposeHeader>
            <ExposeHeader>ExposeHeader_2</ExposeHeader>
        </CORSRule>
    </CORSConfiguration>
