:original_name: en-us_topic_0125560348.html

.. _en-us_topic_0125560348:

PUT Object - Copy
=================

You can use this operation to create a copy of an existing object in OBS.

By default, a **PUT Object - Copy** operation copies object metadata together with the object. If you want to update the metadata, provide new metadata in the **PUT Object - Copy** request. The object ACL is not copied together with the object and the ACL of a copy object is set to **private** by default. You can send a **PUT Object acl** request to modify the object ACL.

The **PUT Object - Copy** request must contain authentication information and cannot contain a request body.

Versioning
----------

By default, **x-amz-copy-source** specifies the latest version of the source object. If the latest version of the source object is a deletion mark, the object is considered to be deleted. You can add **versionId** to request header **x-amz-copy-source** to copy an object with the specified version ID.

If a bucket has versioning enabled, the system automatically generates a unique version ID for the requested object in this bucket and returns the version ID in response header **x-amz-version-id**. If a bucket has versioning suspended, the version ID of the requested object in this bucket is **null**.

.. important::

   If multi-version is not enabled for a bucket, you can replace source object **objecta** with target object **objectb** by replication. If **objectb** already exists before you perform replication, the new **objectb** will overwrite the old **objectb** after you perform replication.

   After replication is performed successfully, only new **objectb** can be downloaded. The old **objectb** will be deleted. Before using the copy interface, ensure that the target object does not exist or is useless to avoid incorrect data deletion. During the replication, the source object **objecta** is not changed.

   You cannot determine whether a request is executed successfully only using **status_code** in the header returned by HTTP. If 200 in **status_code** is returned, the server has received the request and starts to process the request. The body in the response shows whether the replication operation succeeds. The replication operation succeeds only when the body has ETags. Otherwise, the replication operation fails.

Request Syntax
--------------

.. code-block::

    PUT /destinationObjectName HTTP/1.1
    User-Agent: agent
    Host: bucketname.obs.example.com
    Accept: */*
    x-amz-copy-source: /sourceBucket/sourceObject
    x-amz-metadata-directive: COPY
    x-amz-copy-source-if-match: etag
    x-amz-copy-source-if-none-match: etag
    x-amz-copy-source-if-unmodified-since: time_stamp
    x-amz-copy-source-if-modified-since: time_stamp
    Authorization: signatureValue
    Date: date

Request Parameters
------------------

This request involves no parameters.

Request Headers
---------------

This request uses common headers. For details about common request headers, see section :ref:`Common Request Headers <en-us_topic_0125560462>`. In addition, you can add optional headers to specify the object to be copied. :ref:`Table 1 <en-us_topic_0125560348__table59683248>` describes the optional headers.

.. _en-us_topic_0125560348__table59683248:

.. table:: **Table 1** Optional request headers

   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | Header                                | Description                                                                                                                                                                                              | Remarks                                                                          |
   +=======================================+==========================================================================================================================================================================================================+==================================================================================+
   | x-amz-acl                             | Indicates the ACL applied to the copy object. Possible values are **private**, **public-read**, **public-read-write**, **authenticated-read**, **bucket-owner-read**, and **bucket-owner-full-control**. | Optional                                                                         |
   |                                       |                                                                                                                                                                                                          |                                                                                  |
   |                                       | Type: String                                                                                                                                                                                             |                                                                                  |
   |                                       |                                                                                                                                                                                                          |                                                                                  |
   |                                       | Example:                                                                                                                                                                                                 |                                                                                  |
   |                                       |                                                                                                                                                                                                          |                                                                                  |
   |                                       | x-amz-acl: acl                                                                                                                                                                                           |                                                                                  |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | x-amz-copy-source                     | Indicates the name of the source bucket and the key of the source object. If the source object has multiple version IDs, **versionId** is used to specify the required version ID.                       | Mandatory                                                                        |
   |                                       |                                                                                                                                                                                                          |                                                                                  |
   |                                       | Type: String                                                                                                                                                                                             |                                                                                  |
   |                                       |                                                                                                                                                                                                          |                                                                                  |
   |                                       | Example: x-amz-copy-source: /source_bucket/sourceObject                                                                                                                                                  |                                                                                  |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | x-amz-metadata-directive              | Indicates whether the metadata is copied from the source object or replaced with the metadata provided in the request.                                                                                   | Optional                                                                         |
   |                                       |                                                                                                                                                                                                          |                                                                                  |
   |                                       | Type: String                                                                                                                                                                                             |                                                                                  |
   |                                       |                                                                                                                                                                                                          |                                                                                  |
   |                                       | Valid values: **COPY** or **REPLACE**                                                                                                                                                                    |                                                                                  |
   |                                       |                                                                                                                                                                                                          |                                                                                  |
   |                                       | Default: **COPY**                                                                                                                                                                                        |                                                                                  |
   |                                       |                                                                                                                                                                                                          |                                                                                  |
   |                                       | Example: x-amz-metadata-directive: **COPY**                                                                                                                                                              |                                                                                  |
   |                                       |                                                                                                                                                                                                          |                                                                                  |
   |                                       | Constraints:                                                                                                                                                                                             |                                                                                  |
   |                                       |                                                                                                                                                                                                          |                                                                                  |
   |                                       | -  If the value is neither **COPY** nor **REPLACE**, OBS returns status code **400**.                                                                                                                    |                                                                                  |
   |                                       | -  If you want to copy an object to itself, set the value to **REPLACE**. Otherwise, OBS considers the request invalid and returns status code **400**.                                                  |                                                                                  |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | x-amz-copy-source-if-match            | Copies the source object only if its ETag matches the one specified by this header, otherwise a 412 HTTP status code error (failed precondition) is returned.                                            | Optional                                                                         |
   |                                       |                                                                                                                                                                                                          |                                                                                  |
   |                                       | Type: String                                                                                                                                                                                             |                                                                                  |
   |                                       |                                                                                                                                                                                                          |                                                                                  |
   |                                       | Example: x-amz-copy-source-if-match: etag                                                                                                                                                                |                                                                                  |
   |                                       |                                                                                                                                                                                                          |                                                                                  |
   |                                       | Constraints: This header can be used with **x-amz-copy-source-if-unmodified-since** but cannot be used with other conditional copy headers.                                                              |                                                                                  |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | x-amz-copy-source-if-none-match       | Copies the source object only if its ETag is different from the one specified by this header, otherwise a 412 HTTP status code error (failed precondition) is returned.                                  | Optional                                                                         |
   |                                       |                                                                                                                                                                                                          |                                                                                  |
   |                                       | Type: String                                                                                                                                                                                             |                                                                                  |
   |                                       |                                                                                                                                                                                                          |                                                                                  |
   |                                       | Example: x-amz-copy-source-if-none-match: etag                                                                                                                                                           |                                                                                  |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | x-amz-copy-source-if-unmodified-since | Copies the source object only if it has not been modified since the time specified by this header, otherwise a 412 HTTP status code error (failed precondition) is returned.                             | Optional                                                                         |
   |                                       |                                                                                                                                                                                                          |                                                                                  |
   |                                       | Type: HTTP time string complying with the format specified in http://www.ietf.org/rfc/rfc2616.txt.                                                                                                       |                                                                                  |
   |                                       |                                                                                                                                                                                                          |                                                                                  |
   |                                       | Example: x-amz-copy-source-if-unmodified-since: time-stamp                                                                                                                                               |                                                                                  |
   |                                       |                                                                                                                                                                                                          |                                                                                  |
   |                                       | Constraints: This header can be used with **x-amz-copy-source-if-match** but cannot be used with other conditional copy headers.                                                                         |                                                                                  |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | x-amz-copy-source-if-modified-since   | Copies the source object only if it has not been modified since the time specified by this header, otherwise a 412 HTTP status code error (failed precondition) is returned.                             | Optional                                                                         |
   |                                       |                                                                                                                                                                                                          |                                                                                  |
   |                                       | Type: HTTP time string complying with the format specified in http://www.ietf.org/rfc/rfc2616.txt.                                                                                                       |                                                                                  |
   |                                       |                                                                                                                                                                                                          |                                                                                  |
   |                                       | Example: x-amz-copy-source-if-modified-since: time-stamp                                                                                                                                                 |                                                                                  |
   |                                       |                                                                                                                                                                                                          |                                                                                  |
   |                                       | Constraints: This header can be used with **x-amz-copy-source-if-none-match** but cannot be used with other conditional copy headers.                                                                    |                                                                                  |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | x-amz-website-redirect-location       | If a bucket is configured as a website, redirects requests for this object to another object in the same bucket or to an external URL. OBS stores the value of this header in the object metadata.       | Optional                                                                         |
   |                                       |                                                                                                                                                                                                          |                                                                                  |
   |                                       | Type: String                                                                                                                                                                                             |                                                                                  |
   |                                       |                                                                                                                                                                                                          |                                                                                  |
   |                                       | Default: None                                                                                                                                                                                            |                                                                                  |
   |                                       |                                                                                                                                                                                                          |                                                                                  |
   |                                       | Constraint: The value must be prefixed by a slash (/), **http://**, or **https://**. The length of the value cannot exceed 2 K.                                                                          |                                                                                  |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | x-amz-security-token                  | Header field used to identify the request of a federated user. When the federal authentication function is enabled, users sending such requests are identified as federated users.                       | Optional. This parameter must be carried in the request sent by federated users. |
   |                                       |                                                                                                                                                                                                          |                                                                                  |
   |                                       | Type: string                                                                                                                                                                                             |                                                                                  |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+

For details about other headers, see section :ref:`Common Request Headers <en-us_topic_0125560462>`.

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
    Content-Type: type
    Date: date
    Content-Length: length

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <CopyObjectResult xmlns="http://obs.example.com/doc/2015-06-30/">
    <LastModified>modifiedDate</LastModified>
    <ETag>etagValue</ETag>
    </CopyObjectResult>

Response Headers
----------------

This response uses common headers. For details about common response headers, see section :ref:`Common Response Headers <en-us_topic_0125560484>`.

This response also uses optional headers, as described in :ref:`Table 2 <en-us_topic_0125560348__table44830087>`.

.. _en-us_topic_0125560348__table44830087:

.. table:: **Table 2** Optional response header

   +-----------------------------------+------------------------------------------------+
   | Header                            | Description                                    |
   +===================================+================================================+
   | x-amz-copy-source-version-id      | Indicates the version ID of the source object. |
   |                                   |                                                |
   |                                   | Type: String                                   |
   +-----------------------------------+------------------------------------------------+
   | x-amz-version-id                  | Indicates the version ID of the target object. |
   |                                   |                                                |
   |                                   | Type: String                                   |
   +-----------------------------------+------------------------------------------------+

Response Elements
-----------------

This response contains elements to indicate the copy results. :ref:`Table 3 <en-us_topic_0125560348__table5815269>` describes the elements.

.. _en-us_topic_0125560348__table5815269:

.. table:: **Table 3** Response elements

   +-----------------------------------+-------------------------------------------------------+
   | Element                           | Description                                           |
   +===================================+=======================================================+
   | CopyObjectResult                  | Indicates the container for copy results.             |
   |                                   |                                                       |
   |                                   | Type: XML                                             |
   +-----------------------------------+-------------------------------------------------------+
   | LastModified                      | Indicates the date when the object was last modified. |
   |                                   |                                                       |
   |                                   | Type: String                                          |
   +-----------------------------------+-------------------------------------------------------+
   | ETag                              | Indicates the ETag of the new object.                 |
   |                                   |                                                       |
   |                                   | Type: String                                          |
   +-----------------------------------+-------------------------------------------------------+

Error Responses
---------------

No special error responses are returned. For details about error responses, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`.

Sample Request
--------------

.. code-block:: text

   PUT /destobject HTTP/1.1
    User-Agent: Jakarta Commons-HttpClient/3.1
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Sat, 03 Dec 2011 08:48:07 +0000
    Authorization: AWS BF6C09F302931425E9A7:2rZR+iaH8xUewvUKuicLhLHpNoU=
    x-amz-copy-source: /bucket/srcobject

Sample Response
---------------

.. code-block::

   HTTP/1.1 200 OK
    Server: OBS
    x-amz-request-id: 001B21A61C6C00000134031BE8005293
    x-amz-id-2: MDAxQjIxQTYxQzZDMDAwMDAxMzQwMzFCRTgwMDUyOTNBQUFBQUFBQWJiYmJiYmJi
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Content-Type: application/xml
    Date: Sat, 03 Dec 2011 08:48:07 GMT
    Content-Length: 254

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <CopyObjectResult xmlns="http://obs.example.com/doc/2015-06-30/">
    <LastModified>2011-12-03T08:48:07.706Z</LastModified>
    <ETag>"507e3fff69b69bf57d303e807448560b"</ETag>
    </CopyObjectResult>

Sample Request (Copying an Object with Version ID Specified to a Bucket with Versioning Enabled)
------------------------------------------------------------------------------------------------

.. code-block:: text

   PUT /destobject HTTP/1.1
    User-Agent: Jakarta Commons-HttpClient/3.1
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Mon, 13 Jan 2014 12:19:13 +0000
    Authorization: AWS C5780CDE717D50F4CDAA:4BLYv+1UxfRSHBMvrhVLDszxvcY=
    x-amz-copy-source: versionbucket/srcobject?versionId=AAABQ4uBLdLc0vycq3gAAAAEVURTRkha

Sample Response (Copying an Object with Version ID Specified to a Bucket with Versioning Enabled)
-------------------------------------------------------------------------------------------------

.. code-block::

   HTTP/1.1 200 OK
    Server: OBS
    x-amz-request-id: DCD2FC9CAB78000001438B8A9C898B79
    x-amz-id-2: DB/qBZmbN6AIoX9mrrSNYdLxwvbO0tLR/l6/XKTT4NmZspzhWrwp5Z74ybAYVOgr
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Content-Type: application/xml
    x-amz-version-id: AAABQ4uKnOrc0vycq3gAAAAFVURTRkha
    x-amz-copy-source-version-id: AAABQ4uBLdLc0vycq3gAAAAEVURTRkha
    Date: Mon, 13 Jan 2014 12:19:14 GMT
    Transfer-Encoding: chunked
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <CopyObjectResult xmlns="http://obs.example.com/doc/2015-06-30/">
    <LastModified>2014-01-13T12:19:13.770Z</LastModified>
    <ETag>"ba1f2511fc30423bdbb183fe33f3dd0f"</ETag>
    </CopyObjectResult>

Sample Request (Copying an Object with Version ID Specified to a Bucket with Versioning Suspended)
--------------------------------------------------------------------------------------------------

.. code-block:: text

   PUT /object03 HTTP/1.1
    User-Agent: Jakarta Commons-HttpClient/3.1
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Mon, 13 Jan 2014 12:30:11 +0000
    Authorization: AWS C5780CDE717D50F4CDAA:TzFaMXTynxWqPdhhRy9l/8Litb8=
    x-amz-copy-source: versionbucket/srcobject?versionId=AAABQ4uBLdLc0vycq3gAAAAEVURTRkha

Sample Response (Copying an Object with Version ID Specified to a Bucket with Versioning Suspended)
---------------------------------------------------------------------------------------------------

.. code-block::

   HTTP/1.1 200 OK
    Server: OBS
    x-amz-request-id: DCD2FC9CAB78000001438B94A6CE90D3
    x-amz-id-2: ITdGwAvGXezuPzC6m87LVpk2F0i6P5W8GxhBOhmwdf03VjrcL/OXSeOlTpnTLnJy
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Content-Type: application/xml
    x-amz-version-id: null
    Date: Mon, 13 Jan 2014 12:30:11 GMT
    Transfer-Encoding: chunked
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <CopyObjectResult xmlns="http://obs.example.com/doc/2015-06-30/">
    <LastModified>2014-01-13T12:30:11.690Z</LastModified>
    <ETag>"ba1f2511fc30423bdbb183fe33f3dd0f"</ETag>
    </CopyObjectResult>
