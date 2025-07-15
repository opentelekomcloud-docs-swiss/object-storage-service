:original_name: en-us_topic_0125560237.html

.. _en-us_topic_0125560237:

GET Bucket (List Objects)
=========================

After being granted the **READ** permission for a bucket, you can use this operation to obtain the list of objects in this bucket.

If you specify only the bucket name in the **GET Bucket** request, OBS returns descriptions for some or all objects (a maximum of 1000 objects) in the bucket.

If you also specify one or more parameters among **prefix**, **marker**, **max-keys**, and **delimiter** in the request, OBS returns a list of objects as specified. :ref:`Table 1 <en-us_topic_0125560237__table14681180>` describes the parameters in this request.

When the number of listed objects exceeds the default upper limit 1000 or the specified **max-keys** value, the **NextMarker** field is displayed in the response message, indicating the last object to be listed in the request. For subsequent requests, you can set the **marker** to the value of **NextMarker** returned last time, and list subsequent objects.

Request Syntax
--------------

.. code-block:: text

   GET /?prefix=p&delimiter=d HTTP/1.1
    User-Agent: agent
    Host: bucketname.obs.example.com
    Accept: */*
    Date: date
    Authorization: authorization

Request Parameters
------------------

You can specify parameters in this request to list desired objects in a bucket. :ref:`Table 1 <en-us_topic_0125560237__table14681180>` describes the parameters.

.. _en-us_topic_0125560237__table14681180:

.. table:: **Table 1** Request parameters

   +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Parameter             | Description                                                                                                                                                                                          | Remarks               |
   +=======================+======================================================================================================================================================================================================+=======================+
   | prefix                | Limits the response to object keys that begin with the specified prefix.                                                                                                                             | Optional              |
   |                       |                                                                                                                                                                                                      |                       |
   |                       | Type: String                                                                                                                                                                                         |                       |
   +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | marker                | Indicates the object key to start with when listing objects in a bucket. All objects are listed in the dictionary order.                                                                             | Optional              |
   |                       |                                                                                                                                                                                                      |                       |
   |                       | Type: String                                                                                                                                                                                         |                       |
   +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | max-keys              | Sets the maximum number of object keys returned in the response body. The value ranges from 1 to 1000. If the value is not in this range, 1000 is returned by default.                               | Optional              |
   |                       |                                                                                                                                                                                                      |                       |
   |                       | Type: Integer                                                                                                                                                                                        |                       |
   +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | delimiter             | Indicates a character or a sequence of characters used to group object keys.                                                                                                                         | Optional              |
   |                       |                                                                                                                                                                                                      |                       |
   |                       | All object keys that contain the same string between the prefix, if specified, and the first occurrence of delimiter after the prefix are grouped under a single result element, **CommonPrefixes**. |                       |
   |                       |                                                                                                                                                                                                      |                       |
   |                       | Type: String                                                                                                                                                                                         |                       |
   +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

Request Headers
---------------

This request uses common headers. For details about common request headers, see section :ref:`Common Request Headers <en-us_topic_0125560462>`.

If you want to obtain CORS configuration information, you must use the headers in :ref:`Table 2 <en-us_topic_0125560237__table26112624>`.

.. _en-us_topic_0125560237__table26112624:

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
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    x-amz-bucket-region: region name
    x-amz-id-2: id
    Content-Type: type
    Date: date
    Content-Length: length

   <Response Body>

Response Headers
----------------

This response uses common headers. For details about common response headers, see section :ref:`Common Response Headers <en-us_topic_0125560484>`.

In addition to common headers, when CORS is configured for buckets, you can use the response headers in :ref:`Table 3 <en-us_topic_0125560237__table881688>`.

.. _en-us_topic_0125560237__table881688:

.. table:: **Table 3** Appended response headers

   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | Header                            | Description                                                                                                                                       |
   +===================================+===================================================================================================================================================+
   | Access-Control-Allow-Origin       | If **Origin** in the request meets the CORS configuration requirements, **Origin** is included in the response.                                   |
   |                                   |                                                                                                                                                   |
   |                                   | Type: String                                                                                                                                      |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access-Control-Allow-Headers      | CORS is configured for buckets. If **headers** in the request meet the CORS configuration requirements, **headers** are included in the response. |
   |                                   |                                                                                                                                                   |
   |                                   | Type: String                                                                                                                                      |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access-Control-Max-Age            | Indicates **MaxAgeSeconds** in the CORS configuration of a server.                                                                                |
   |                                   |                                                                                                                                                   |
   |                                   | Type: Integer                                                                                                                                     |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access-Control-Allow-Methods      | If **Access-Control-Request-Method** in the request meets the CORS configuration requirements, methods in the rule are included in the response.  |
   |                                   |                                                                                                                                                   |
   |                                   | Type: String                                                                                                                                      |
   |                                   |                                                                                                                                                   |
   |                                   | Valid values: **GET**, **PUT**, **HEAD**, **POST**, and **DELETE**                                                                                |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access-Control-Expose-Headers     | Indicates **ExposeHeader** in the CORS configuration of a server.                                                                                 |
   |                                   |                                                                                                                                                   |
   |                                   | Type: String                                                                                                                                      |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | x-amz-bucket-region               | Indicates the region of the bucket.                                                                                                               |
   |                                   |                                                                                                                                                   |
   |                                   | Type: String                                                                                                                                      |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+

Response Elements
-----------------

This response contains the XML list of the objects in a bucket. :ref:`Table 4 <en-us_topic_0125560237__table51351348142023>` describes the elements in the XML list.

.. _en-us_topic_0125560237__table51351348142023:

.. table:: **Table 4** Response elements

   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Element                           | Description                                                                                                                                                                                              |
   +===================================+==========================================================================================================================================================================================================+
   | ListBucketResult                  | A list of objects in a bucket                                                                                                                                                                            |
   |                                   |                                                                                                                                                                                                          |
   |                                   | Type: XML                                                                                                                                                                                                |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Contents                          | Metadata of the objects                                                                                                                                                                                  |
   |                                   |                                                                                                                                                                                                          |
   |                                   | Type: XML                                                                                                                                                                                                |
   |                                   |                                                                                                                                                                                                          |
   |                                   | Parent node: ListBucketResult                                                                                                                                                                            |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | CommonPrefixes                    | Grouping information. If you specify a delimiter in the request, the response contains grouping information in **CommonPrefixes**.                                                                       |
   |                                   |                                                                                                                                                                                                          |
   |                                   | Type: XML                                                                                                                                                                                                |
   |                                   |                                                                                                                                                                                                          |
   |                                   | Parent node: ListBucketResult                                                                                                                                                                            |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Delimiter                         | The **delimiter** parameter specified in a request                                                                                                                                                       |
   |                                   |                                                                                                                                                                                                          |
   |                                   | Type: String                                                                                                                                                                                             |
   |                                   |                                                                                                                                                                                                          |
   |                                   | Parent node: ListBucketResult                                                                                                                                                                            |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | DisplayName                       | Name of an object owner                                                                                                                                                                                  |
   |                                   |                                                                                                                                                                                                          |
   |                                   | Type: String                                                                                                                                                                                             |
   |                                   |                                                                                                                                                                                                          |
   |                                   | Parent node: ListBucketResult.Contents.Owner                                                                                                                                                             |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ETag                              | The MD5 value of an object.                                                                                                                                                                              |
   |                                   |                                                                                                                                                                                                          |
   |                                   | Type: String                                                                                                                                                                                             |
   |                                   |                                                                                                                                                                                                          |
   |                                   | Parent node: ListBucketResult.Contents                                                                                                                                                                   |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ID                                | DomainId of an object owner                                                                                                                                                                              |
   |                                   |                                                                                                                                                                                                          |
   |                                   | Type: String                                                                                                                                                                                             |
   |                                   |                                                                                                                                                                                                          |
   |                                   | Parent node: ListBucketResult.Contents.Owner                                                                                                                                                             |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | IsTruncated                       | Determines whether the returned list is truncated. **true** indicates that the result is incomplete while **false** indicates that the result is complete.                                               |
   |                                   |                                                                                                                                                                                                          |
   |                                   | Type: Boolean                                                                                                                                                                                            |
   |                                   |                                                                                                                                                                                                          |
   |                                   | Parent node: ListBucketResult                                                                                                                                                                            |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Key                               | Name of an object                                                                                                                                                                                        |
   |                                   |                                                                                                                                                                                                          |
   |                                   | Type: String                                                                                                                                                                                             |
   |                                   |                                                                                                                                                                                                          |
   |                                   | Parent node: ListBucketResult.Contents                                                                                                                                                                   |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | LastModified                      | Date and time when the last modification was made to an object                                                                                                                                           |
   |                                   |                                                                                                                                                                                                          |
   |                                   | Type: Date                                                                                                                                                                                               |
   |                                   |                                                                                                                                                                                                          |
   |                                   | Parent node: ListBucketResult.Contents                                                                                                                                                                   |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Marker                            | Start point for listing objects                                                                                                                                                                          |
   |                                   |                                                                                                                                                                                                          |
   |                                   | Type: String                                                                                                                                                                                             |
   |                                   |                                                                                                                                                                                                          |
   |                                   | Parent node: ListBucketResult                                                                                                                                                                            |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | NextMarker                        | A marker for the last returned object in the list. **NextMarker** is returned when not all the objects are listed. You can set the **Marker** value to list the remaining objects in follow-up requests. |
   |                                   |                                                                                                                                                                                                          |
   |                                   | Type: String                                                                                                                                                                                             |
   |                                   |                                                                                                                                                                                                          |
   |                                   | Parent node: ListBucketResult                                                                                                                                                                            |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | MaxKeys                           | The maximum objects returned.                                                                                                                                                                            |
   |                                   |                                                                                                                                                                                                          |
   |                                   | Type: String                                                                                                                                                                                             |
   |                                   |                                                                                                                                                                                                          |
   |                                   | Parent node: ListBucketResult                                                                                                                                                                            |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Name                              | Name of the requested bucket                                                                                                                                                                             |
   |                                   |                                                                                                                                                                                                          |
   |                                   | Type: String                                                                                                                                                                                             |
   |                                   |                                                                                                                                                                                                          |
   |                                   | Parent node: ListBucketResult                                                                                                                                                                            |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Owner                             | User information, including the DomainId and name                                                                                                                                                        |
   |                                   |                                                                                                                                                                                                          |
   |                                   | Type: XML                                                                                                                                                                                                |
   |                                   |                                                                                                                                                                                                          |
   |                                   | Parent node: ListBucketResult.Contents                                                                                                                                                                   |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Prefix                            | Prefix of an object key. Only objects whose keys have this prefix are listed.                                                                                                                            |
   |                                   |                                                                                                                                                                                                          |
   |                                   | Type: String                                                                                                                                                                                             |
   |                                   |                                                                                                                                                                                                          |
   |                                   | Parent node: ListBucketResult                                                                                                                                                                            |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Size                              | Number of bytes of an object                                                                                                                                                                             |
   |                                   |                                                                                                                                                                                                          |
   |                                   | Type: String                                                                                                                                                                                             |
   |                                   |                                                                                                                                                                                                          |
   |                                   | Parent node: ListBucketResult.Contents                                                                                                                                                                   |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | StorageClass                      | Storage class of an object                                                                                                                                                                               |
   |                                   |                                                                                                                                                                                                          |
   |                                   | Type: String                                                                                                                                                                                             |
   |                                   |                                                                                                                                                                                                          |
   |                                   | Values: STANDARD \| STANDARD_IA \|GLACIER                                                                                                                                                                |
   |                                   |                                                                                                                                                                                                          |
   |                                   | Parent node: ListBucketResult.Contents                                                                                                                                                                   |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Error Responses
---------------

No special error responses are returned. For details about error responses, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`.

Sample Request
--------------

.. code-block:: text

   GET / HTTP/1.1
    User-Agent: Jakarta Commons-HttpClient/3.1
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Sun, 26 Sep 2010 09:16:00 GMT
    Authorization: AWS 04RZT432N80TGDF2Y2G2:QaTwEcRs5E4p/uahBMYHB+dY00k=

Sample Response
---------------

.. code-block::

   HTTP/1.1 200 OK
    Server: OBS
    x-amz-request-id: 367CB63A2F283044981285492719060
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    x-amz-bucket-region: R1
    x-amz-id-2: MzY3Q0I2M0EyRjI4MzA0NDk4MTI4NTQ5MjcxOTA2MEFBQUFBQUFBYmJiYmJiYmJD
    Content-Type: application/xml
    Date: Sun, 26 Sep 2010 09:18:36 GMT
    Content-Length: 560

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <ListBucketResult xmlns="http://obs.example.com/doc/2015-06-30/">
    <Name>example</Name>
    <Prefix></Prefix>
    <Marker></Marker>
    <MaxKeys>1000</MaxKeys>
    <IsTruncated>false</IsTruncated>
    <Contents>
    <Key>test</Key>
    <LastModified>2013-01-15T05:52:15.920Z</LastModified>
    <ETag>0f64741bf7cb1089e988e4585d0d3434</ETag>
    <Size>11</Size>
    <Owner>
    <ID>bcaf1ffd86f41caff1a493dc2ad8c2c281e37522a640e161ca5fb16fd081034f</ID>
    <DisplayName>apple</DisplayName>
    </Owner>
    <StorageClass>STANDARD</StorageClass>
    </Contents>
    </ListBucketResult>

Sample Request (Example of listing objects in a bucket by specifying prefix)
----------------------------------------------------------------------------

.. code-block:: text

   GET /?prefix=photos/2006/&delimiter=/ HTTP/1.1
    User-Agent: Jakarta Commons-HttpClient/3.1
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Sun, 26 Sep 2010 09:18:36 GMT
    Authorization: AWS 04RZT432N80TGDF2Y2G2:QaTwEcRs5E4p/uahBMYHB+dY00k=

Sample Response (Example of listing objects in a bucket by specifying prefix)
-----------------------------------------------------------------------------

.. code-block::

   HTTP/1.1 200 OK
    Server: OBS
    x-amz-request-id: 367CB63A2F283044981285492719060
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    x-amz-bucket-region: R1
    x-amz-id-2: MzY3Q0I2M0EyRjI4MzA0NDk4MTI4NTQ5MjcxOTA2MEFBQUFBQUFBYmJiYmJiYmJD
    Content-Type: application/xml
    Date: Sun, 26 Sep 2010 09:18:36 GMT
    Content-Length: 560

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <ListBucketResult xmlns="http://obs.example.com/doc/2015-06-30/">
    <Name>example</Name>
    <Prefix>photos/2006/</Prefix>
    <Marker></Marker>
    <MaxKeys>1000</MaxKeys>
    <Delimiter>/</Delimiter>
    <IsTruncated>false</IsTruncated>
    <Contents>
    <Key>photos/2006/index.html</Key>
    <LastModified>2009-01-01T12:00:00.000Z</LastModified>
    <ETag>ce1acdafcc879d7eee54cf4e97334078</ETag>
    <Size>1234</Size>
    <Owner>
    <ID>214153b66967d86f031c7487b4566cb1b</ID>
    <DisplayName>John Smith</DisplayName>
    </Owner>
    <StorageClass>STANDARD</StorageClass>
    </Contents>
    <CommonPrefixes>
    <Prefix>photos/2006/January/</Prefix>
    </CommonPrefixes>
    </ListBucketResult>

Sample Request (list of objects in a bucket and the CORS configuration being obtained with CORS configured for the bucket)
--------------------------------------------------------------------------------------------------------------------------

.. code-block:: text

   GET / HTTP/1.1
   User-Agent: curl/7.19.0 (x86_64-suse-linux-gnu) libcurl/7.19.0 OpenSSL/0.9.8{ zlib/1.2.3 libidn/1.10
   Host: bucketname.obs.example.com
   Accept: */*
   Date: Tue, 28 Apr 2015 13:52:29 +0000
   Authorization: AWS D13E0C94E722DD69423C:m/jxIj4ZYv4mjpk4xqlMTQKe7aQ=
   Origin:www.example.com
   Access-Control-Request-Headers:AllowedHeader_1

Sample Response (list of objects in a bucket and the CORS configuration being obtained with CORS configured for the bucket)
---------------------------------------------------------------------------------------------------------------------------

.. code-block::

   HTTP/1.1 200 OK
   Server: OBS
   x-amz-request-id: B50AD92B37C934BAD314B5EB0BB5BEF2
   x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
   Access-Control-Allow-Origin: www.example.com
   Access-Control-Allow-Methods: POST,GET,HEAD,PUT,DELETE
   Access-Control-Allow-Headers: AllowedHeader_1
   Access-Control-Max-Age: 100
   Access-Control-Expose-Headers: ExposeHeader_1
   x-amz-id-2: 1jSuajz0BqBC0sly+aYIIpbK4ETxBVeCYtBq3Lvc7H7zuCefvq9Kowtp0o3cmQ3X
   Content-Type: application/xml
   Date: Tue, 28 Apr 2015 13:52:29 GMT
   Content-Length: 559
