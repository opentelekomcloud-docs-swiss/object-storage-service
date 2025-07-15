:original_name: en-us_topic_0125560273.html

.. _en-us_topic_0125560273:

GET Bucket Object versions
==========================

After being granted the **READ** permission for a bucket, you can use this operation to obtain the list of objects in this bucket.

If you specify only the bucket name in the request (**GET /BucketName**), OBS returns descriptions of all objects (a maximum of 1000 objects) in the bucket.

If you specify one or more parameters among **prefix**, **marker**, **max-keys**, **delimiter**, and **version-id-marker**, OBS returns a list of objects in alphabetic order as specified. :ref:`Table 1 <en-us_topic_0125560273__table5679749>` describes the request parameters.

Request Syntax
--------------

.. code-block:: text

   GET /?versions HTTP/1.1
   User-Agent: agent
   Host: bucketname.obs.example.com
   Accept: */*
   Date: date
   Authorization: authorization

Request Parameters
------------------

You can specify parameters in this request to list desired objects (including objects with different version IDs) in a bucket. :ref:`Table 1 <en-us_topic_0125560273__table5679749>` describes the parameters.

.. _en-us_topic_0125560273__table5679749:

.. table:: **Table 1** Request parameters

   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Parameter             | Description                                                                                                                                                                                                                               | Remarks               |
   +=======================+===========================================================================================================================================================================================================================================+=======================+
   | prefix                | Limits the response to object keys that begin with the specified prefix.                                                                                                                                                                  | Optional              |
   |                       |                                                                                                                                                                                                                                           |                       |
   |                       | Type: String                                                                                                                                                                                                                              |                       |
   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | key-marker            | Indicates the object key to start with when listing objects in a bucket. All objects are listed in the dictionary order.                                                                                                                  | Optional              |
   |                       |                                                                                                                                                                                                                                           |                       |
   |                       | Type: String                                                                                                                                                                                                                              |                       |
   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | max-keys              | Sets the maximum number of object keys returned in the response body. All objects are listed in the dictionary order. The value ranges from 1 to 1000. If the value is not in this range, 1000 is returned by default.                    | Optional              |
   |                       |                                                                                                                                                                                                                                           |                       |
   |                       | Type: Integer                                                                                                                                                                                                                             |                       |
   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | delimiter             | Indicates a character used to group object keys. All object keys that contain the same string between the prefix and the first occurrence of the delimiter after the prefix are grouped under a single result element **CommonPrefixes**. | Optional              |
   |                       |                                                                                                                                                                                                                                           |                       |
   |                       | Type: String                                                                                                                                                                                                                              |                       |
   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | version-id-marker     | Indicates the version ID to start with when listing objects in a bucket. All objects are listed in the dictionary order. This parameter is used together with **key-marker**.                                                             | Optional              |
   |                       |                                                                                                                                                                                                                                           |                       |
   |                       | If the value of **version-id-marker** is not a version ID specified by **key-marker**, **version-id-marker** is invalid.                                                                                                                  |                       |
   |                       |                                                                                                                                                                                                                                           |                       |
   |                       | Type: String                                                                                                                                                                                                                              |                       |
   |                       |                                                                                                                                                                                                                                           |                       |
   |                       | Valid Value: object version ID|None                                                                                                                                                                                                       |                       |
   |                       |                                                                                                                                                                                                                                           |                       |
   |                       | Constraint: This parameter cannot be an empty string.                                                                                                                                                                                     |                       |
   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

Request Headers
---------------

This request uses common headers. For details about common request headers, see section :ref:`Common Request Headers <en-us_topic_0125560462>`.

If you want to obtain CORS configuration information, you must use the headers in :ref:`Table 2 <en-us_topic_0125560273__table51117746>`.

.. _en-us_topic_0125560273__table51117746:

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
    Server: OBS
    x-amz-request-id: request id
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    x-amz-id-2: id
    Content-Type: type
    Date: date
    Content-Length: length

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <ListVersionsResult xmlns="http://obs.example.com/doc/2015-06-30/">
    <Name>bucket</Name>
    <Prefix/>
    <KeyMarker/>
    <VersionIdMarker/>
    <NextKeyMarker>nextKeyMarker</NextKeyMarker>
    <NextVersionIdMarker>nextVersionIdMarker</NextVersionIdMarker>
    <MaxKeys>maxKeys</MaxKeys>
    <IsTruncated>boolean</IsTruncated>
    <Version>
    <Key>object</Key>
    <VersionId>versionId</VersionId>
    <IsLatest>boolean</IsLatest>
    <LastModified>date</LastModified>
    <ETag>String</ETag>
    <Size>size</Size>
    <Owner>
    <ID>ownerID</ID>
    <DisplayName>name</DisplayName>
    </Owner>
    <StorageClass>storageClass</StorageClass>
    </Version>
    <DeleteMarker>
    <Key>object</Key>
    <VersionId>versionId</VersionId>
    <IsLatest>boolean</IsLatest>
    <LastModified>date</LastModified>
    <Owner>
    <ID>ownerID</ID>
    <DisplayName>name</DisplayName>
    </Owner>
    </DeleteMarker>
    </ListVersionsResult>

Response Headers
----------------

This response uses common headers. For details about common response headers, see section :ref:`Common Response Headers <en-us_topic_0125560484>`.

In addition to common headers, when CORS is configured for buckets, you can use the response headers in :ref:`Table 3 <en-us_topic_0125560273__table28132937>`.

.. _en-us_topic_0125560273__table28132937:

.. table:: **Table 3** Appended response headers

   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | Header                            | Description                                                                                                                                      |
   +===================================+==================================================================================================================================================+
   | Access-Control-Allow-Origin       | If **Origin** in the request meets the CORS configuration requirements, **Origin** is included in the response.                                  |
   |                                   |                                                                                                                                                  |
   |                                   | Type: String                                                                                                                                     |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access-Control-Allow-Headers      | If **headers** in the request meet the CORS configuration requirements, **headers** are included in the response.                                |
   |                                   |                                                                                                                                                  |
   |                                   | Type: String                                                                                                                                     |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access-Control-Max-Age            | Indicates **MaxAgeSeconds** in the CORS configuration of a server.                                                                               |
   |                                   |                                                                                                                                                  |
   |                                   | Type: Integer                                                                                                                                    |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access-Control-Allow-Methods      | If **Access-Control-Request-Method** in the request meets the CORS configuration requirements, methods in the rule are included in the response. |
   |                                   |                                                                                                                                                  |
   |                                   | Type: String                                                                                                                                     |
   |                                   |                                                                                                                                                  |
   |                                   | Valid values: **GET**, **PUT**, **HEAD**, **POST**, and **DELETE**                                                                               |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access-Control-Expose-Headers     | Indicates **ExposeHeader** in the CORS configuration of a server.                                                                                |
   |                                   |                                                                                                                                                  |
   |                                   | Type: String                                                                                                                                     |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+

Response Elements
-----------------

This response contains elements to specify the objects (including objects with multiple version IDs) in a bucket. :ref:`Table 4 <en-us_topic_0125560273__table51869847>` describes the elements.

.. _en-us_topic_0125560273__table51869847:

.. table:: **Table 4** Response elements

   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Element                           | Description                                                                                                                                                                                                                                       |
   +===================================+===================================================================================================================================================================================================================================================+
   | ListVersionsResult                | Indicates the container for the list of objects (including objects with multiple version IDs).                                                                                                                                                    |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Type: Container                                                                                                                                                                                                                                   |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Name                              | Indicates the bucket name.                                                                                                                                                                                                                        |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Type: String                                                                                                                                                                                                                                      |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Ancestor: ListVersionsResult                                                                                                                                                                                                                      |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Prefix                            | Indicates the prefix of an object key. Only objects whose keys have this prefix are listed.                                                                                                                                                       |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Type: String                                                                                                                                                                                                                                      |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Ancestor: ListVersionsResult                                                                                                                                                                                                                      |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | KeyMarker                         | Indicates the object key to start with when listing objects.                                                                                                                                                                                      |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Type: String                                                                                                                                                                                                                                      |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Ancestor: ListVersionsResult                                                                                                                                                                                                                      |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | VersionIdMarker                   | Indicates the object version ID to start with when listing objects.                                                                                                                                                                               |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Type: String                                                                                                                                                                                                                                      |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Ancestor: ListVersionsResult                                                                                                                                                                                                                      |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | NextKeyMarker                     | Indicates the key marker for the last returned object in the list. **NextKeyMarker** is returned when not all the objects are listed. You can set the **KeyMarker** value to list the remaining objects in follow-up requests.                    |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Type: String                                                                                                                                                                                                                                      |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Ancestor: ListVersionsResult                                                                                                                                                                                                                      |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | NextVersionIdMarker               | Indicates the version ID marker for the last returned object in the list. **NextVersionIdMarker** is returned when not all the objects are listed. You can set the **VersionIdMarker** value to list the remaining objects in follow-up requests. |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Type: String                                                                                                                                                                                                                                      |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Ancestor: ListVersionsResult                                                                                                                                                                                                                      |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | MaxKeys                           | Indicates the maximum objects returned.                                                                                                                                                                                                           |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Type: String                                                                                                                                                                                                                                      |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Ancestor: ListVersionsResult                                                                                                                                                                                                                      |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | IsTruncated                       | Determines whether the returned list of objects is truncated. **true** indicates that the result is incomplete while **false** indicates that the result is complete.                                                                             |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Type: Boolean                                                                                                                                                                                                                                     |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Ancestor: ListVersionsResult                                                                                                                                                                                                                      |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Version                           | Indicates the container for version information.                                                                                                                                                                                                  |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Type: Container                                                                                                                                                                                                                                   |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Ancestor: ListVersionsResult                                                                                                                                                                                                                      |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | DeleteMarker                      | Indicates the container for objects with deletion marks.                                                                                                                                                                                          |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Type: Container                                                                                                                                                                                                                                   |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Ancestor: ListVersionsResult                                                                                                                                                                                                                      |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | key                               | Name of an object                                                                                                                                                                                                                                 |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Type: String                                                                                                                                                                                                                                      |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Ancestor: ListVersionsResult.Version \| ListVersionsResult.DeleteMarker                                                                                                                                                                           |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | VersionId                         | Indicates the object version ID.                                                                                                                                                                                                                  |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Type: String                                                                                                                                                                                                                                      |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Ancestor: ListVersionsResult.Version \| ListVersionsResult.DeleteMarker                                                                                                                                                                           |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | IsLatest                          | Specifies whether the object is or is not of the latest version. If the element is **true**, the object is of the latest version.                                                                                                                 |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Type: Boolean                                                                                                                                                                                                                                     |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Ancestor: ListVersionsResult.Version \| ListVersionsResult.DeleteMarker                                                                                                                                                                           |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | LastModified                      | Indicates the date and time when the last modification was made to an object.                                                                                                                                                                     |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Type: Date                                                                                                                                                                                                                                        |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Ancestor: ListVersionsResult.Version \| ListVersionsResult.DeleteMarker                                                                                                                                                                           |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ETag                              | MD5 value of an object                                                                                                                                                                                                                            |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Type: String                                                                                                                                                                                                                                      |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Ancestor: ListVersionsResult.Version                                                                                                                                                                                                              |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Size                              | Number of bytes of an object                                                                                                                                                                                                                      |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Type: String                                                                                                                                                                                                                                      |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Ancestor: ListVersionsResult.Version                                                                                                                                                                                                              |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Owner                             | User information, including the DomainId and name                                                                                                                                                                                                 |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Type: Container                                                                                                                                                                                                                                   |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Ancestor: ListVersionsResult.Version \| ListVersionsResult.DeleteMarker                                                                                                                                                                           |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ID                                | DomainId of an object owner                                                                                                                                                                                                                       |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Type: String                                                                                                                                                                                                                                      |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Ancestor: ListVersionsResult.Version.Owner \| ListVersionsResult.DeleteMarker.Owner                                                                                                                                                               |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | DisplayName                       | Name of an object owner                                                                                                                                                                                                                           |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Type: String                                                                                                                                                                                                                                      |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Ancestor: ListVersionsResult.Version.Owner \| ListVersionsResult.Version.Owner                                                                                                                                                                    |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | StorageClass                      | Storage type of an object                                                                                                                                                                                                                         |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Type: Enumeration                                                                                                                                                                                                                                 |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Ancestor: ListVersionsResult.Version                                                                                                                                                                                                              |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | CommonPrefixes                    | Grouping information. If you specify a delimiter in the request, the response contains grouping information in **CommonPrefixes**.                                                                                                                |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Type: Container                                                                                                                                                                                                                                   |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Ancestor: ListVersionsResult                                                                                                                                                                                                                      |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Prefix                            | Indicates a different prefix in the grouping information in **CommonPrefixes**.                                                                                                                                                                   |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Type: String                                                                                                                                                                                                                                      |
   |                                   |                                                                                                                                                                                                                                                   |
   |                                   | Ancestor: ListVersionsResult.CommonPrefixes                                                                                                                                                                                                       |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Error Responses
---------------

No special error responses are returned. For details about error responses, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`.

Sample Request
--------------

.. code-block:: text

   GET /?versions HTTP/1.1
    User-Agent: curl/7.19.0
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Thu, 16 Jan 2014 03:31:26 +0000
    Authorization: AWS C9590CEB8EC051BDEC9D:KfF0yCAt+LAE/AE0YTxQS7IzQ8U=

Sample Response
---------------

.. code-block::

   HTTP/1.1 200 OK
    Server: OBS
    x-amz-request-id: DCD2FC9CAB7800000143991A7DEECBF4
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    x-amz-id-2: 00QkPL575tIUmU8kth0zA16DlRzzdDiVDHK4OaGeujayXCfdD7phC21ZZYmVqx3W
    Content-Type: application/xml
    Date: Thu, 16 Jan 2014 03:31:26 GMT
    Content-Length: 1275

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <ListVersionsResult xmlns="http://obs.example.com/doc/2015-06-30/">
   <Name>bucket</Name>
    <Prefix/>
    <KeyMarker/>
    <VersionIdMarker/>
    <MaxKeys>1000</MaxKeys>
    <IsTruncated>false</IsTruncated>
    <DeleteMarker>
    <Key>key0</Key>
    <VersionId>AAABQ5kabBnc0vycq3gAAABCVURTRkha</VersionId>
    <IsLatest>true</IsLatest>
    <LastModified>2014-01-16T03:31:22.265Z</LastModified>
    <Owner>
    <ID>DCD2FC9CAB78000001438EC051BD0002</ID>
    <DisplayName>user</DisplayName>
    </Owner>
    </DeleteMarker>
    <Version>
    <Key>key0</Key>
    <VersionId>AAABQ5kZxWTc0vycq3gAAABBVURTRkha</VersionId>
    <IsLatest>false</IsLatest>
    <LastModified>2014-01-16T03:30:39.575Z</LastModified>
    <ETag>"6b0e1cad9fd2eff22004e28aa8073420"</ETag>
    <Size>80</Size>
    <Owner>
    <ID>DCD2FC9CAB78000001438EC051BD0002</ID>
    <DisplayName>user</DisplayName>
    </Owner>
    <StorageClass>STANDARD</StorageClass>
    </Version>
    <Version>
    <Key>suspend</Key>
    <VersionId>null</VersionId>
    <IsLatest>true</IsLatest>
    <LastModified>2014-01-16T03:25:58.443Z</LastModified>
    <ETag>"a65d3be0857de44e470e0c069e4b04e3"</ETag>
    <Size>80</Size>
    <Owner>
    <ID>DCD2FC9CAB78000001438EC051BD0002</ID>
    <DisplayName>user</DisplayName>
    </Owner>
    <StorageClass>STANDARD</StorageClass>
    </Version>
    </ListVersionsResult>

Sample Request (Example of getting bucket object versions by using key-marker and version-id-marker)
----------------------------------------------------------------------------------------------------

.. code-block:: text

   GET /?versions&key-marker=key0&version-id-marker=AAABQ5kabBnc0vycq3gAAABCVURTRkha HTTP/1.1
    User-Agent: curl/7.19.0
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Thu, 16 Jan 2014 04:48:20 +0000
    Authorization: AWS C9590CEB8EC051BDEC9D:iw+nTJEMO5KLMoE66sqzkRF3ik0=

Sample Response (Example of getting bucket object versions by using key-marker and version-id-marker)
-----------------------------------------------------------------------------------------------------

.. code-block::

   HTTP/1.1 200 OK
    Server: OBS
    x-amz-request-id: DCD2FC9CAB78000001439960E2F3F18A
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    x-amz-id-2: P1j6zAy1GOP9KoRUWgJt3mJGKNLlAU4dn7BfL16VXpeWCX/25cZpshp5mTbu1kyw
    Content-Type: application/xml
    Date: Thu, 16 Jan 2014 04:48:20 GMT
    Content-Length: 1051

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <ListVersionsResult xmlns="http://obs.example.com/doc/2015-06-30/">
    <Name>bucket</Name>
    <Prefix/>
    <KeyMarker>key0</KeyMarker>
    <VersionIdMarker>AAABQ5kabBnc0vycq3gAAABCVURTRkha</VersionIdMarker>
    <MaxKeys>1000</MaxKeys>
    <IsTruncated>false</IsTruncated>
    <Version>
    <Key>key0</Key>
    <VersionId>AAABQ5kZxWTc0vycq3gAAABBVURTRkha</VersionId>
    <IsLatest>false</IsLatest>
    <LastModified>2014-01-16T03:30:39.575Z</LastModified>
    <ETag>"6b0e1cad9fd2eff22004e28aa8073420"</ETag>
    <Size>80</Size>
    <Owner>
    <ID>DCD2FC9CAB78000001438EC051BD0002</ID>
    <DisplayName>user</DisplayName>
    </Owner>
    <StorageClass>STANDARD</StorageClass>
    </Version>
    <Version>
    <Key>suspend</Key>
    <VersionId>null</VersionId>
    <IsLatest>true</IsLatest>
    <LastModified>2014-01-16T03:25:58.443Z</LastModified>
    <ETag>"a65d3be0857de44e470e0c069e4b04e3"</ETag>
    <Size>80</Size>
    <Owner>
    <ID>DCD2FC9CAB78000001438EC051BD0002</ID>
    <DisplayName>user</DisplayName>
    </Owner>
    <StorageClass>STANDARD</StorageClass>
    </Version>
    </ListVersionsResult>
