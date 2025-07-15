:original_name: en-us_topic_0125560336.html

.. _en-us_topic_0125560336:

GET Object
==========

You can use this operation to obtain the content and metadata of an object, as long as you have **READ** permission for the object.

Versioning
----------

By default, the content of the object with the latest version ID is obtained. If the version ID of the object is a deletion mark, **404** is returned. You can specify **versionId** to obtain the content of an object of the desired version.

Cold Objects
------------

For Cold objects, the response varies with the restoration status of the objects. If the objects have been restored, then the **x-amz-restore** header is returned indicating the expiry date of the objects when they are successfully downloaded. If you request to download Cold objects that are not restored or are being restored, a **403 Forbidden** error is returned.

Request Syntax
--------------

.. code-block:: text

   GET /ObjectName HTTP/1.1
    User-Agent: agent
    Host: bucketname.obs.example.com
    Accept: */*
    Date: date
    Authorization: authorization
    Range:bytes=byte_range
    <Optional Additional Header>

.. note::

   In this request, header **Range** is optional. If this header is not specified, all data of an object is returned.

Request Parameters
------------------

In a **GET** request, you can override values for a set of response headers using the request parameters listed in :ref:`Table 1 <en-us_topic_0125560336__table63181911>`. Response headers that you can override are **Content-Type**, **Content-Language**, **Expires**, **Cache-Control**, **Content-Disposition**, and **Content-Encoding**.

.. _en-us_topic_0125560336__table63181911:

.. table:: **Table 1** Request parameters

   +------------------------------+-------------------------------------------------------------------+-----------------------+
   | Parameter                    | Description                                                       | Remarks               |
   +==============================+===================================================================+=======================+
   | response-content-type        | Overrides the **Content-Type** header in the response.            | Optional              |
   |                              |                                                                   |                       |
   |                              | Type: String                                                      |                       |
   +------------------------------+-------------------------------------------------------------------+-----------------------+
   | response-content-language    | Overrides the **Content-Language** header in the response.        | Optional              |
   |                              |                                                                   |                       |
   |                              | Type: String                                                      |                       |
   +------------------------------+-------------------------------------------------------------------+-----------------------+
   | response-expires             | Overrides the **Expires** header in the response.                 | Optional              |
   |                              |                                                                   |                       |
   |                              | Type: String                                                      |                       |
   +------------------------------+-------------------------------------------------------------------+-----------------------+
   | response-cache-control       | Overrides the **Cache-Control** header in the response.           | Optional              |
   |                              |                                                                   |                       |
   |                              | Type: String                                                      |                       |
   +------------------------------+-------------------------------------------------------------------+-----------------------+
   | response-content-disposition | Overrides the **Content-Disposition** header in the response.     | Optional              |
   |                              |                                                                   |                       |
   |                              | Type: String                                                      |                       |
   +------------------------------+-------------------------------------------------------------------+-----------------------+
   | response-content-encoding    | Overrides the **Content-Encoding** header in the response.        | Optional              |
   |                              |                                                                   |                       |
   |                              | Type: String                                                      |                       |
   +------------------------------+-------------------------------------------------------------------+-----------------------+
   | versionId                    | Specifies the version ID of the object whose content is obtained. | Optional              |
   |                              |                                                                   |                       |
   |                              | Type: String                                                      |                       |
   +------------------------------+-------------------------------------------------------------------+-----------------------+

Request Headers
---------------

This request uses common headers. For details about common request headers, see section :ref:`Common Request Headers <en-us_topic_0125560462>`. In addition, you can add optional headers to this request. :ref:`Table 2 <en-us_topic_0125560336__table54982876>` describes the optional headers.

.. _en-us_topic_0125560336__table54982876:

.. table:: **Table 2** Optional request headers

   +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | Header                         | Description                                                                                                                                                                                                                                         | Remarks                                                                          |
   +================================+=====================================================================================================================================================================================================================================================+==================================================================================+
   | Range                          | Obtains the specified range bytes of an object. The value is a range starting from 0 to maximum object length minus one. If the range is invalid, all object data is returned.                                                                      | Optional                                                                         |
   |                                |                                                                                                                                                                                                                                                     |                                                                                  |
   |                                | Type: String                                                                                                                                                                                                                                        |                                                                                  |
   |                                |                                                                                                                                                                                                                                                     |                                                                                  |
   |                                | Note:                                                                                                                                                                                                                                               |                                                                                  |
   |                                |                                                                                                                                                                                                                                                     |                                                                                  |
   |                                | The header format for a single range is *bytes=byte_range*, for example, **bytes=0-4** or **bytes=512-1024**. The header format for multiple ranges is, for example, **bytes=10-20,30-40**. If there are multiple ranges, the output is as follows: |                                                                                  |
   |                                |                                                                                                                                                                                                                                                     |                                                                                  |
   |                                | --5926640d-5ca3-4e56-a9e9-5493dab2da66                                                                                                                                                                                                              |                                                                                  |
   |                                |                                                                                                                                                                                                                                                     |                                                                                  |
   |                                | Content-type: binary/octet-stream                                                                                                                                                                                                                   |                                                                                  |
   |                                |                                                                                                                                                                                                                                                     |                                                                                  |
   |                                | Content-range: bytes 10-20/7279                                                                                                                                                                                                                     |                                                                                  |
   |                                |                                                                                                                                                                                                                                                     |                                                                                  |
   |                                | xxxx                                                                                                                                                                                                                                                |                                                                                  |
   |                                |                                                                                                                                                                                                                                                     |                                                                                  |
   |                                | --5926640d-5ca3-4e56-a9e9-5493dab2da66                                                                                                                                                                                                              |                                                                                  |
   |                                |                                                                                                                                                                                                                                                     |                                                                                  |
   |                                | Content-type: binary/octet-stream                                                                                                                                                                                                                   |                                                                                  |
   |                                |                                                                                                                                                                                                                                                     |                                                                                  |
   |                                | Content-range: bytes 30-40/7279                                                                                                                                                                                                                     |                                                                                  |
   |                                |                                                                                                                                                                                                                                                     |                                                                                  |
   |                                | yyyy                                                                                                                                                                                                                                                |                                                                                  |
   |                                |                                                                                                                                                                                                                                                     |                                                                                  |
   |                                | .. note::                                                                                                                                                                                                                                           |                                                                                  |
   |                                |                                                                                                                                                                                                                                                     |                                                                                  |
   |                                |    **--5926640d-5ca3-4e56-a9e9-5493dab2da66--** is a randomly generated character string and functions as a separator.                                                                                                                              |                                                                                  |
   |                                |                                                                                                                                                                                                                                                     |                                                                                  |
   |                                |    **Content-type** indicates the type of the range data.                                                                                                                                                                                           |                                                                                  |
   |                                |                                                                                                                                                                                                                                                     |                                                                                  |
   |                                |    **Content-range** indicates the data range or the total object size.                                                                                                                                                                             |                                                                                  |
   +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | If-Modified-Since              | Returns the object only if it has been modified since the time specified by this header, otherwise **304 Not Modified** is returned.                                                                                                                | Optional                                                                         |
   |                                |                                                                                                                                                                                                                                                     |                                                                                  |
   |                                | Type: HTTP time string complying with the format specified in http://www.ietf.org/rfc/rfc2616.txt.                                                                                                                                                  |                                                                                  |
   +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | If-Unmodified-Since            | Returns the object only if it has not been modified since the time specified by this header, otherwise **412 Precondition Failed** is returned.                                                                                                     | Optional                                                                         |
   |                                |                                                                                                                                                                                                                                                     |                                                                                  |
   |                                | Type: HTTP time string complying with the format specified in http://www.ietf.org/rfc/rfc2616.txt.                                                                                                                                                  |                                                                                  |
   +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | If-Match                       | Returns the object only if its ETag is the same as the one specified by this header, otherwise **412 Precondition Failed** is returned.                                                                                                             | Optional                                                                         |
   |                                |                                                                                                                                                                                                                                                     |                                                                                  |
   |                                | Type: String                                                                                                                                                                                                                                        |                                                                                  |
   |                                |                                                                                                                                                                                                                                                     |                                                                                  |
   |                                | Note:                                                                                                                                                                                                                                               |                                                                                  |
   |                                |                                                                                                                                                                                                                                                     |                                                                                  |
   |                                | An example ETag value is **0f64741bf7cb1089e988e4585d0d3434**.                                                                                                                                                                                      |                                                                                  |
   +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | If-None-Match                  | Returns the object only if its ETag is different from the one specified by this header, otherwise **304 Not Modified** is returned.                                                                                                                 | Optional                                                                         |
   |                                |                                                                                                                                                                                                                                                     |                                                                                  |
   |                                | Type: String                                                                                                                                                                                                                                        |                                                                                  |
   |                                |                                                                                                                                                                                                                                                     |                                                                                  |
   |                                | Note:                                                                                                                                                                                                                                               |                                                                                  |
   |                                |                                                                                                                                                                                                                                                     |                                                                                  |
   |                                | An example ETag value is **0f64741bf7cb1089e988e4585d0d3434**.                                                                                                                                                                                      |                                                                                  |
   +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | Origin                         | Indicates an origin specified by a pre-request. Generally, it is a domain name.                                                                                                                                                                     | Optional. If you want to obtain the CORs configuration, this item is mandatory.  |
   |                                |                                                                                                                                                                                                                                                     |                                                                                  |
   |                                | Type: String                                                                                                                                                                                                                                        |                                                                                  |
   +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | Access-Control-Request-Headers | Indicates the HTTP headers of a request. The request can use multiple HTTP headers.                                                                                                                                                                 | Optional                                                                         |
   |                                |                                                                                                                                                                                                                                                     |                                                                                  |
   |                                | Type: String                                                                                                                                                                                                                                        |                                                                                  |
   +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | x-amz-security-token           | Header field used to identify the request of a federated user. When the federal authentication function is enabled, users sending such requests are identified as federated users.                                                                  | Optional. This parameter must be carried in the request sent by federated users. |
   |                                |                                                                                                                                                                                                                                                     |                                                                                  |
   |                                | Type: string                                                                                                                                                                                                                                        |                                                                                  |
   +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+

Request Elements
----------------

This request involves no elements.

Response Syntax
---------------

.. code-block::

   HTTP/1.1 status_code
    Server: OBS
    x-amz-request-id: request id
    x-amz-id-2: id
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Content-Type: type
    Date: date
    Content-Length: length
    Etag: etag
    Last-Modified: time
    <Object Content>

Response Headers
----------------

This response uses common headers. For details about common response headers, see section :ref:`Common Response Headers <en-us_topic_0125560484>`.

This response can also include optional headers. :ref:`Table 3 <en-us_topic_0125560336__table29723549>` describes these headers.

.. _en-us_topic_0125560336__table29723549:

.. table:: **Table 3** Optional response headers

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
   | x-amz-delete-marker               | Indicates whether an object is marked as deleted. If an object is not marked as deleted, the header is not returned.                                                                                                                |
   |                                   |                                                                                                                                                                                                                                     |
   |                                   | Type: Boolean                                                                                                                                                                                                                       |
   |                                   |                                                                                                                                                                                                                                     |
   |                                   | Valid values: true|false                                                                                                                                                                                                            |
   |                                   |                                                                                                                                                                                                                                     |
   |                                   | Default: false                                                                                                                                                                                                                      |
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
   | x-amz-storage-class               | This header is returned when the storage class of an object is not Standard.                                                                                                                                                        |
   |                                   |                                                                                                                                                                                                                                     |
   |                                   | Type: String                                                                                                                                                                                                                        |
   |                                   |                                                                                                                                                                                                                                     |
   |                                   | Valid values: **STANDARD_IA** and **GLACIER**                                                                                                                                                                                       |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | x-amz-restore                     | This header is returned when the storage class of an object is OBS Cold and the object has been restored.                                                                                                                           |
   |                                   |                                                                                                                                                                                                                                     |
   |                                   | Example:                                                                                                                                                                                                                            |
   |                                   |                                                                                                                                                                                                                                     |
   |                                   | x-amz-restore:ongoing-request="false", expiry-date="Wed, 07 Nov 2012 00:00:00 GMT"                                                                                                                                                  |
   |                                   |                                                                                                                                                                                                                                     |
   |                                   | -  **ongoing-request="false"**\ indicates that the object has been restored.                                                                                                                                                        |
   |                                   | -  In **expiry-date="Wed, 07 Nov 2012 00:00:00 GMT"**, **expiry-date** indicates the expiry date of the restored object.                                                                                                            |
   |                                   |                                                                                                                                                                                                                                     |
   |                                   | Type: String                                                                                                                                                                                                                        |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Response Elements
-----------------

This response involves no elements.

Error Responses
---------------

No special error responses are returned. For details about error responses, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`.

Sample Request for Not Overriding Response Headers
--------------------------------------------------

.. code-block:: text

   GET /test HTTP/1.1
    User-Agent: Jakarta Commons-HttpClient/3.1
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Sat, 03 Dec 2011 08:28:02 +0000
    Authorization: AWS BF6C09F302931425E9A7:tQ+A280jUgPCAdSTuUis35T9gWI=

Sample Response for Not Overriding Response Headers
---------------------------------------------------

.. code-block::

   HTTP/1.1 200 OK
    Server: OBS
    x-amz-request-id: 001B21A61C6C0000013403098535528C
    x-amz-id-2: MDAxQjIxQTYxQzZDMDAwMDAxMzQwMzA5ODUzNTUyOENBQUFBQUFBQWJiYmJiYmJi
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    ETag: "507e3fff69b69bf57d303e807448560b"
    Last-Modified: Sat, 03 Dec 2011 08:25:46 GMT
    Accept-Ranges: bytes
    Content-Length: 30
    Content-Type: binary/octet-stream
    Date: Sat, 03 Dec 2011 08:28:02 GMT

Sample Request for Overriding Headers
-------------------------------------

.. code-block:: text

   GET /test?response-cache-control=No-cache&response-content-disposition=attachment%3B%20filename%3Dtesting.txt&response-content-encoding=x-gzip&response-content-language=mi%2C%20en&response-expires=Thu%2C%2001%20Dec%201994%2016:00:00%20GMT HTTP/1.1
    User-Agent: Jakarta Commons-HttpClient/3.1
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Sat, 03 Dec 2011 08:28:02 +0000
    Authorization: AWS BF6C09F302931425E9A7: aaStE6nKnw8ihhiIdReoXYlMamW=

Sample Response for Overriding Headers
--------------------------------------

.. code-block::

   HTTP/1.1 200 OK
    Server: OBS
    x-amz-request-id: 001B21A61C6C0000013403098535528C
    x-amz-id-2: MDAxQjIxQTYxQzZDMDAwMDAxMzQwMzA5ODUzNTUyOENBQUFBQUFBQWJiYmJiYmJi
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    ETag: "507e3fff69b69bf57d303e807448560b"
    Last-Modified: Sat, 03 Dec 2011 08:25:46 GMT
    Accept-Ranges: bytes
    Content-Length: 30
    Cache-Control: No-cache
    Content-Language: mi, en
    Expires: Thu, 01 Dec 1994 16:00:00 GMT
    Content-Disposition: attachment; filename=testing.txt
    Content-Encoding: x-gzip
    Content-Type: binary/octet-stream
    Date: Sat, 03 Dec 2011 08:28:02 GMT

Sample Request for Getting an Object with Version ID Specified
--------------------------------------------------------------

.. code-block:: text

   GET /object?versionId=AAABQ47OMnbc0vycq3gAAAANVURTRkha HTTP/1.1
    User-Agent: Jakarta Commons-HttpClient/3.1
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Tue, 14 Jan 2014 06:11:49 +0000
    Authorization: AWS C9590CEB8EC051BDEC9D:kpuA5lb+IoEOglV5824R4Yb18RE=

Sample Response for Getting an Object with Version ID Specified
---------------------------------------------------------------

.. code-block::

   HTTP/1.1 200 OK
    Server: OBS
    x-amz-request-id: DCD2FC9CAB78000001438F609AD59896
    x-amz-id-2: nz0bi6ru2wS4OvhkCS1OQ2FwyxjvYwuGv1EI5JVeDpuGwX6weBoX7MRxJwhuXJu9
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Accept-Ranges: bytes
    ETag: "ba1f2511fc30423bdbb183fe33f3dd0f"
    Last-Modified: Tue, 14 Jan 2014 03:31:54 GMT
    Content-Length: 4
    x-amz-version-id: AAABQ47OMnbc0vycq3gAAAANVURTRkha
    Content-Type: binary/octet-stream
    Date: Tue, 14 Jan 2014 06:11:49 GMT

    [4 bytes of object data]

Sample Request for Getting an Object Whose Latest Version ID Is a Deletion Mark
-------------------------------------------------------------------------------

.. code-block:: text

   GET /object HTTP/1.1
    User-Agent: Jakarta Commons-HttpClient/3.1
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Tue, 14 Jan 2014 06:17:59 +0000
    Authorization: AWS C9590CEB8EC051BDEC9D:MsZcBz1QOULDOhPP1gx1+4hbh4A=

Sample Response for Getting an Object Whose Latest Version ID Is a Deletion Mark
--------------------------------------------------------------------------------

.. code-block::

   HTTP/1.1 404 Not Found
    Server: OBS
    x-amz-request-id: DCD2FC9CAB78000001438F6640529BA9
    x-amz-id-2: /BdlSJIqa5Gkl3yEoEgmJKUUak0xjtgCTn9LhbsyJwqG5OVqrkfiateRxF8Gg4AU
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Content-Type: application/xml
    x-amz-version-id: AAABQ49lNT_c0vycq3gAAAAOVURTRkha
    x-amz-delete-marker: true
    Date: Tue, 14 Jan 2014 06:17:59 GMT
    Content-Length: 297

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <Error>
    <Code>NoSuchKey</Code>
    <Message>The specified key does not exist.</Message>
    <RequestId>DCD2FC9CAB78000001438F6640529BA9</RequestId>
    <HostId>nkbX5Pw7vRd26kP6gRwQQ4AxiN446dN608LMf4/9h/NMdhrWsc17Vnlva6VS23dq</HostId>
    <Key>object</Key>
    </Error>

Sample Request for Getting an Object and CORS Configuration when CORS is properly configured
--------------------------------------------------------------------------------------------

.. code-block:: text

   GET /object HTTP/1.1
   User-Agent: curl/7.19.0 (x86_64-suse-linux-gnu) libcurl/7.19.0 OpenSSL/0.9.8{ zlib/1.2.3 libidn/1.10
   Host: bucketname.obs.example.com
   Accept: */*
   Date: Tue, 28 Apr 2015 13:36:06 +0000
   Authorization: AWS D13E0C94E722DD69423C:9PzAsaQnzJfMb2pcUNzaYpxgtSE=
   Origin:www.example.com
   Access-Control-Request-Headers:acc_header_1

Sample Response for Getting an Object and CORS Configuration when CORS is properly configured
---------------------------------------------------------------------------------------------

.. code-block::

   HTTP/1.1 200 OK
   x-amz-request-id: 0B2B8A2B224F067CB15E4203ABF583F4
   x-amz-id-2: PI5ZL3VEM6LnENYPchIQLKDfMlHanhkCz+CgmqCmyN0AniJZMGKBij9bj7fm4sve
   x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
   Access-Control-Allow-Origin: www.example.com
   Access-Control-Allow-Methods: POST,GET,HEAD,PUT
   Access-Control-Allow-Headers: acc_header_01
   Access-Control-Max-Age: 100
   Access-Control-Expose-Headers: exp_header_01
   Accept-Ranges: bytes
   ETag: "6bcb16084a88ae550811429c0c1e8bc7"
   Last-Modified: Tue, 28 Apr 2015 13:38:05 GMT
   Content-Length: 264
   Content-Type: binary/octet-stream
   Date: Tue, 28 Apr 2015 13:38:17 GMTa
