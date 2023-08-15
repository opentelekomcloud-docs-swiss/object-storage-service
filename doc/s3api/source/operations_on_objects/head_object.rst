:original_name: en-us_topic_0125560379.html

.. _en-us_topic_0125560379:

HEAD Object
===========

You can use this operation to view an object's metadata, as long as you have **READ** permission for the object.

Versioning
----------

By default, the metadata of the object of the latest version is obtained. If the version ID of the object is a deletion mark, **404** is returned. You can specify **versionId** to obtain the metadata of an object of the desired version.

Request Syntax
--------------

.. code-block::

   HEAD /ObjectName HTTP/1.1
    User-Agent: agent
    Host: bucketname.obs.example.com
    Accept: */*
    Date: date
    Authorization: authorization

Request Parameters
------------------

:ref:`Table 1 <en-us_topic_0125560379__table59191946>` describes the request parameter.

.. _en-us_topic_0125560379__table59191946:

.. table:: **Table 1** Request parameter

   +-----------------------+----------------------------------------+-----------------------+
   | Parameter             | Description                            | Remarks               |
   +=======================+========================================+=======================+
   | versionId             | Indicates the version ID of an object. | Optional              |
   |                       |                                        |                       |
   |                       | Type: String                           |                       |
   +-----------------------+----------------------------------------+-----------------------+

Request Headers
---------------

This request uses common headers. For details about common request headers, see section :ref:`Common Request Headers <en-us_topic_0125560462>`.

If you want to obtain CORS configuration information, you must use the headers in :ref:`Table 2 <en-us_topic_0125560379__table62965470>`.

.. _en-us_topic_0125560379__table62965470:

.. table:: **Table 2** Request headers of CORS configuration

   +--------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | Header                         | Description                                                                                                                                                                        | Remarks                                                                          |
   +================================+====================================================================================================================================================================================+==================================================================================+
   | Origin                         | Indicates an origin specified by a pre-request. Generally, it is a domain name.                                                                                                    | Mandatory                                                                        |
   |                                |                                                                                                                                                                                    |                                                                                  |
   |                                | Type: String                                                                                                                                                                       |                                                                                  |
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
    Server: Server Name
    x-amz-request-id: request id
    x-amz-id-2: id
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Accept-Ranges: bytes
    Content-Type: type
    Date: date
    Content-Length: length
    Etag: etag
    Last-Modified: time

Response Headers
----------------

This response uses common headers. For details about common response headers, see section :ref:`Common Response Headers <en-us_topic_0125560484>`.

This response can also include an optional header. :ref:`Table 3 <en-us_topic_0125560379__table53033363>` describes the header.

.. _en-us_topic_0125560379__table53033363:

.. table:: **Table 3** Optional response header

   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Header                            | Description                                                                                                                                                                                                                         |
   +===================================+=====================================================================================================================================================================================================================================+
   | x-amz-expiration                  | This header is included in the response if the object expiration is configured. This header includes **expiry-date** and **rule-id** key value pairs to provide object expiration information.                                      |
   |                                   |                                                                                                                                                                                                                                     |
   |                                   | Type: String                                                                                                                                                                                                                        |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | x-amz-website-redirect-location   | When a bucket is configured as a website, you can set this metadata for the object so that the website endpoint will evaluate the request for the object as a 301 redirect to another object in the same bucket or an external URL. |
   |                                   |                                                                                                                                                                                                                                     |
   |                                   | Type: String                                                                                                                                                                                                                        |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | x-amz-version-id                  | Indicates the version ID of an object. If an object has no version ID specified, this header is not returned.                                                                                                                       |
   |                                   |                                                                                                                                                                                                                                     |
   |                                   | Valid values: String                                                                                                                                                                                                                |
   |                                   |                                                                                                                                                                                                                                     |
   |                                   | Default: None                                                                                                                                                                                                                       |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access-Control-Allow-Origin       | CORS is configured for buckets. If **Origin** in the request meets the CORS configuration requirements, **Origin** is included in the response.                                                                                     |
   |                                   |                                                                                                                                                                                                                                     |
   |                                   | Type: String                                                                                                                                                                                                                        |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access-Control-Allow-Headers      | CORS is configured for buckets. If **headers** in the request meet the CORS configuration requirements, **headers** are included in the response.                                                                                   |
   |                                   |                                                                                                                                                                                                                                     |
   |                                   | Type: String                                                                                                                                                                                                                        |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access-Control-Max-Age            | Indicates **MaxAgeSeconds** in the CORS configuration of a server when CORS is configured for buckets.                                                                                                                              |
   |                                   |                                                                                                                                                                                                                                     |
   |                                   | Type: Integer                                                                                                                                                                                                                       |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access-Control-Allow-Methods      | CORS is configured for buckets. If **Access-Control-Request-Method** in the request meets the CORS configuration requirements, methods in the rule are included in the response.                                                    |
   |                                   |                                                                                                                                                                                                                                     |
   |                                   | Type: String                                                                                                                                                                                                                        |
   |                                   |                                                                                                                                                                                                                                     |
   |                                   | Valid values: **GET**, **PUT**, **HEAD**, **POST**, and **DELETE**                                                                                                                                                                  |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access-Control-Expose-Headers     | Indicates **ExposeHeader** in the CORS configuration of a server when CORS is configured for buckets.                                                                                                                               |
   |                                   |                                                                                                                                                                                                                                     |
   |                                   | Type: String                                                                                                                                                                                                                        |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Response elements
-----------------

This response involves no elements.

Error Responses
---------------

No special error responses are returned. For details about error responses, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`.

Sample Request
--------------

.. code-block::

   HEAD /test HTTP/1.1
    User-Agent: Jakarta Commons-HttpClient/3.1
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Sat, 03 Dec 2011 09:17:57 +0000
    Authorization: AWS BF6C09F302931425E9A7:++6NkzwVhw4qccNfIqf4G2vMggg=

Sample Response
---------------

.. code-block::

   HTTP/1.1 200 OK
    Server: OBS
    x-amz-request-id: 001B21A61C6C0000013403373811529D
    x-amz-id-2: MDAxQjIxQTYxQzZDMDAwMDAxMzQwMzM3MzgxMTUyOURBQUFBQUFBQWJiYmJiYmJi
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Accept-Ranges: bytes
    ETag: "507e3fff69b69bf57d303e807448560b"
    Last-Modified: Sat, 03 Dec 2011 08:47:50 GMT
    Content-Length: 30
    Content-Type: binary/octet-stream
    Date: Sat, 03 Dec 2011 09:17:57 GMT

Sample Request (Getting the Metadata of an Object with Version ID Specified)
----------------------------------------------------------------------------

.. code-block::

   HEAD /object?versionId=AAABQ4-glIvc0vycq3gAAAAVVURTRkha HTTP/1.1
    User-Agent: Jakarta Commons-HttpClient/3.1
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Tue, 14 Jan 2014 07:22:17 +0000
    Authorization: AWS C9590CEB8EC051BDEC9D:CTunmEJMuOBqUa4zfJNz6zxkjBE=

Sample Response (Getting the Metadata of an Object with Version ID Specified)
-----------------------------------------------------------------------------

.. code-block::

   HTTP/1.1 200 OK
    Server: OBS
    x-amz-request-id: DCD2FC9CAB78000001438FA11E6CBB07
    x-amz-id-2: SSfKQyh2Gr6ygerqHhJLZ6rxPiv+ucjWabr48RssNJMWmGyKh9gDdXC0jvo1JmFs
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Accept-Ranges: bytes
    ETag: "ba1f2511fc30423bdbb183fe33f3dd0f"
    Last-Modified: Tue, 14 Jan 2014 07:21:42 GMT
    Content-Length: 4
    x-amz-version-id: AAABQ4-glIvc0vycq3gAAAAVVURTRkha
    Content-Type: binary/octet-stream
    Date: Tue, 14 Jan 2014 07:22:17 GMT

Sample Request (Getting Object Metadata and CORS Configuration when CORS is properly configured)
------------------------------------------------------------------------------------------------

.. code-block::

   HEAD /object HTTP/1.1
   User-Agent: curl/7.19.0 (x86_64-suse-linux-gnu) libcurl/7.19.0 OpenSSL/0.9.8{ zlib/1.2.3 libidn/1.10
   Host: bucketname.obs.example.com
   Accept: */*
   Date: Tue, 28 Apr 2015 14:03:45 +0000
   Authorization: AWS D13E0C94E722DD69423C:YcuaA/lJkmWn8AqjfWvIodNJ/yM=
   Origin:www.example.com
   Access-Control-Request-Headers:AllowedHeader_1

Sample Response (Getting Object Metadata and CORS Configuration when CORS is properly configured)
-------------------------------------------------------------------------------------------------

.. code-block::

   HTTP/1.1 200 OK
   x-amz-request-id: D168613B12D6EE5744A69C524D3AA876
   x-amz-id-2: 35Sas+J9yUY4xz3PrL0O938UKDg+Dc8EfSw0m9LtfoqB7s0wiMc44TOGguSLNyOv
   x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
   Access-Control-Allow-Origin: www.example.com
   Access-Control-Allow-Methods: POST,GET,HEAD,PUT,DELETE
   Access-Control-Allow-Headers: AllowedHeader_1
   Access-Control-Max-Age: 100
   Access-Control-Expose-Headers: ExposeHeader_1
   Accept-Ranges: bytes
   ETag: "6bcb16084a88ae550811429c0c1e8bc7"
   Last-Modified: Tue, 28 Apr 2015 13:38:05 GMT
   Content-Length: 264
   Content-Type: binary/octet-stream
   Date: Tue, 28 Apr 2015 14:03:45 GMT
