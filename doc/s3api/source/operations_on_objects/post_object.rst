:original_name: en-us_topic_0125560263.html

.. _en-us_topic_0125560263:

POST Object
===========

You can use this operation to upload an object to an existing bucket.

Uploading an object indicates that an object is added to a bucket. This operation requires the write permission.

.. note::

   The objects that are uploaded by users are stored in buckets. Only the users who have the write permission can upload objects to buckets. The names of objects in the same bucket must be unique.

If objects whose object keys are the same exist in a specified bucket, the new objects that are uploaded by a user will overwrite the original objects. To prevent data from being damaged during the transfer process, users can add **Content-MD5** to request headers. After OBS receives the objects that are uploaded, it executes MD5 verification and will return an error if inconsistency is detected.

Users can specify the **x-amz-acl** parameter and set a permission control policy when uploading objects.

After creating a bucket in OBS, you can send a **PUT Object** request to upload an object to the bucket.

Versioning
----------

If a bucket has versioning enabled, the system automatically generates a unique version ID for the requested object in this bucket and returns the version ID in response header **x-amz-version-id**. If a bucket has versioning suspended, the version ID of the requested object in this bucket is **null**. For details about bucket versioning, see section :ref:`PUT Bucket versioning <en-us_topic_0125560444>`.

Request Syntax
--------------

.. code-block:: text

   POST / HTTP/1.1
    Host: bucketname.obs.example.com
    User-Agent: browser_data
    Accept: file_types
    Accept-Language: Regions
    Accept-Encoding: encoding
    Accept-Charset: character_set
    Keep-Alive: 300
    Connection: keep-alive
    Content-Type: multipart/form-data; boundary=-9431149156168
    Content-Length: length


    --9431149156168
    Content-Disposition: form-data; name="key"
    acl
    --9431149156168
    Content-Disposition: form-data; name="success_action_redirect"
    success_redirect
    --9431149156168
    Content-Disposition: form-data; name="content-Type"
    content_type
    --9431149156168
    Content-Disposition: form-data; name="x-amz-meta-uuid"
    uuid
    --9431149156168
    Content-Disposition: form-data; name="x-amz-meta-tag"
    metadata
    --9431149156168
    Content-Disposition: form-data; name="AWSAccessKeyId"
    access-key-id
    --9431149156168
    Content-Disposition: form-data; name="policy"
    encoded_policy
    --9431149156168
    Content-Disposition: form-data; name="signature"
    signature=
    --9431149156168
    Content-Disposition: form-data; name="file"; filename="MyFilename"
    Content-Type: image/jpeg
    file_content
    --9431149156168
    Content-Disposition: form-data; name="submit"
    Upload to OBS
    --9431149156168--

Request Parameters
------------------

This request involves no parameters.

Request Headers
---------------

This request uses common headers. For details about common request headers, see section :ref:`Common Request Headers <en-us_topic_0125560462>`. If you want to obtain CORS configuration information, you must use the headers in :ref:`Table 1 <en-us_topic_0125560263__table48637933>`.

.. _en-us_topic_0125560263__table48637933:

.. table:: **Table 1** Request headers of CORS configuration

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

This request uses form fields. :ref:`Table 2 <en-us_topic_0125560263__table13225554>` describes the form fields.

.. _en-us_topic_0125560263__table13225554:

.. table:: **Table 2** Form fields

   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Form Field                                                         | Description                                                                                                                                                                                                                                                                                 | Remarks               |
   +====================================================================+=============================================================================================================================================================================================================================================================================================+=======================+
   | file                                                               | Indicates the content of the object to be uploaded.                                                                                                                                                                                                                                         | Mandatory             |
   |                                                                    |                                                                                                                                                                                                                                                                                             |                       |
   |                                                                    | Type: Binary or text content                                                                                                                                                                                                                                                                |                       |
   |                                                                    |                                                                                                                                                                                                                                                                                             |                       |
   |                                                                    | Constraints: This field must be the last one in a form. Each request can contain only one **file** field. All excessive **file** fields are discarded.                                                                                                                                      |                       |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | key                                                                | Indicates the name of the object to be uploaded.                                                                                                                                                                                                                                            | Mandatory             |
   |                                                                    |                                                                                                                                                                                                                                                                                             |                       |
   |                                                                    | Type: String                                                                                                                                                                                                                                                                                |                       |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | AWSAccessKeyId                                                     | Indicates the AK of the requester.                                                                                                                                                                                                                                                          | Optional              |
   |                                                                    |                                                                                                                                                                                                                                                                                             |                       |
   |                                                                    | Type: String                                                                                                                                                                                                                                                                                |                       |
   |                                                                    |                                                                                                                                                                                                                                                                                             |                       |
   |                                                                    | Constraints: Required if the **policy** field is included in the request.                                                                                                                                                                                                                   |                       |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | policy                                                             | Indicates the security policy of the request.                                                                                                                                                                                                                                               | Optional              |
   |                                                                    |                                                                                                                                                                                                                                                                                             |                       |
   |                                                                    | Type: String                                                                                                                                                                                                                                                                                |                       |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | expires                                                            | Indicates the date and time at which an object is no longer cacheable. The time is expressed in milliseconds in RFC 2616 format. If this field is specified, it will be returned in response headers after you send a **GET Object** or **HEAD Object** request.                            | Optional              |
   |                                                                    |                                                                                                                                                                                                                                                                                             |                       |
   |                                                                    | Type: String                                                                                                                                                                                                                                                                                |                       |
   |                                                                    |                                                                                                                                                                                                                                                                                             |                       |
   |                                                                    | Example:                                                                                                                                                                                                                                                                                    |                       |
   |                                                                    |                                                                                                                                                                                                                                                                                             |                       |
   |                                                                    | Policy: {" expires ": "1000" }                                                                                                                                                                                                                                                              |                       |
   |                                                                    |                                                                                                                                                                                                                                                                                             |                       |
   |                                                                    | HTML: <input type="text" name=" expires " value="1000" />                                                                                                                                                                                                                                   |                       |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | x-amz-acl                                                          | Indicates the ACL applied to the object to be uploaded. Possible values are **private**, **public-read**, **public-read-write**, **authenticated-read**, **bucket-owner-read**, and **bucket-owner-full-control**. For details, see :ref:`Table 4 <en-us_topic_0125560406__table40200743>`. | Optional              |
   |                                                                    |                                                                                                                                                                                                                                                                                             |                       |
   |                                                                    | Type: String                                                                                                                                                                                                                                                                                |                       |
   |                                                                    |                                                                                                                                                                                                                                                                                             |                       |
   |                                                                    | Example:                                                                                                                                                                                                                                                                                    |                       |
   |                                                                    |                                                                                                                                                                                                                                                                                             |                       |
   |                                                                    | Policy: {"acl": "public-read" }                                                                                                                                                                                                                                                             |                       |
   |                                                                    |                                                                                                                                                                                                                                                                                             |                       |
   |                                                                    | HTML:<input type="text" name="acl" value="public-read" />                                                                                                                                                                                                                                   |                       |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Cache-Control, Content-Type, Content-Disposition, Content-Encoding | Indicate standard HTTP headers. If these fields are specified, they are returned in response headers after you send a **GET Object** or **HEAD Object** request.                                                                                                                            | Optional              |
   |                                                                    |                                                                                                                                                                                                                                                                                             |                       |
   |                                                                    | Type: String                                                                                                                                                                                                                                                                                |                       |
   |                                                                    |                                                                                                                                                                                                                                                                                             |                       |
   |                                                                    | Example:                                                                                                                                                                                                                                                                                    |                       |
   |                                                                    |                                                                                                                                                                                                                                                                                             |                       |
   |                                                                    | Policy: ["starts-with", "$Content-Type", "text/"]                                                                                                                                                                                                                                           |                       |
   |                                                                    |                                                                                                                                                                                                                                                                                             |                       |
   |                                                                    | HTML: <input type="text" name="content-type" value="text/plain" />                                                                                                                                                                                                                          |                       |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | success_action_redirect                                            | Indicates the URL to which the client is redirected after the request is successfully responded to.                                                                                                                                                                                         | Optional              |
   |                                                                    |                                                                                                                                                                                                                                                                                             |                       |
   |                                                                    | -  If the value is valid and the request is successful, OBS returns status code 303. **Location** contains success_action_redirect, bucket name, object name, and object ETag.                                                                                                              |                       |
   |                                                                    | -  If the value is invalid, OBS ignores this field and returns status code 204. **Location** contains the object address.                                                                                                                                                                   |                       |
   |                                                                    |                                                                                                                                                                                                                                                                                             |                       |
   |                                                                    | Type: String                                                                                                                                                                                                                                                                                |                       |
   |                                                                    |                                                                                                                                                                                                                                                                                             |                       |
   |                                                                    | Example:                                                                                                                                                                                                                                                                                    |                       |
   |                                                                    |                                                                                                                                                                                                                                                                                             |                       |
   |                                                                    | Policy: {"success_action_redirect": "http://123458.com"}                                                                                                                                                                                                                                    |                       |
   |                                                                    |                                                                                                                                                                                                                                                                                             |                       |
   |                                                                    | HTML: <input type="text" name="success_action_redirect" value="http://123458.com" />                                                                                                                                                                                                        |                       |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | x-amz-meta-\*                                                      | This prefix is used to construct a field in a **POST** request for returning self-defined metadata. If this prefix is specified, user-defined metadata is returned in one or more response headers prefixed with **x-amz-meta-**.                                                           | Optional              |
   |                                                                    |                                                                                                                                                                                                                                                                                             |                       |
   |                                                                    | Note: The format of the user-defined metadata header is x-amz-meta-key:value. The total size of the key and value of all user-defined metadata in the request cannot exceed 2 KB.                                                                                                           |                       |
   |                                                                    |                                                                                                                                                                                                                                                                                             |                       |
   |                                                                    | Type: String                                                                                                                                                                                                                                                                                |                       |
   |                                                                    |                                                                                                                                                                                                                                                                                             |                       |
   |                                                                    | Example:                                                                                                                                                                                                                                                                                    |                       |
   |                                                                    |                                                                                                                                                                                                                                                                                             |                       |
   |                                                                    | Policy: {" x-amz-meta-test ": " test metadata " }                                                                                                                                                                                                                                           |                       |
   |                                                                    |                                                                                                                                                                                                                                                                                             |                       |
   |                                                                    | HTML: <input type="text" name=" x-amz-meta-test " value=" test metadata " />                                                                                                                                                                                                                |                       |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | success_action_status                                              | Indicates the status code returned after a **POST Object** request is successfully received. Possible values are **200**, **201**, and **204**.                                                                                                                                             | Optional              |
   |                                                                    |                                                                                                                                                                                                                                                                                             |                       |
   |                                                                    | -  If the value is set to **200** or **204**, OBS returns an empty response body.                                                                                                                                                                                                           |                       |
   |                                                                    | -  If the value is set to **201**, OBS returns a response containing an XML file recording request details.                                                                                                                                                                                 |                       |
   |                                                                    | -  If the value is not set or is invalid, OBS returns status code 204.                                                                                                                                                                                                                      |                       |
   |                                                                    |                                                                                                                                                                                                                                                                                             |                       |
   |                                                                    | Type: String                                                                                                                                                                                                                                                                                |                       |
   |                                                                    |                                                                                                                                                                                                                                                                                             |                       |
   |                                                                    | Example:                                                                                                                                                                                                                                                                                    |                       |
   |                                                                    |                                                                                                                                                                                                                                                                                             |                       |
   |                                                                    | Policy: ["starts-with", "$success_action_status", ""]                                                                                                                                                                                                                                       |                       |
   |                                                                    |                                                                                                                                                                                                                                                                                             |                       |
   |                                                                    | HTML: <input type="text" name="success_action_status" value="200" />                                                                                                                                                                                                                        |                       |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | x-amz-website-redirect-location                                    | If a bucket is configured as a website, redirects requests for this object to another object in the same bucket or to an external URL. OBS stores the value of this header in the object metadata.                                                                                          | Optional              |
   |                                                                    |                                                                                                                                                                                                                                                                                             |                       |
   |                                                                    | Default: None                                                                                                                                                                                                                                                                               |                       |
   |                                                                    |                                                                                                                                                                                                                                                                                             |                       |
   |                                                                    | Constraint: The value must be prefixed by a slash (/), **http://**, or **https://**. The length of the value cannot exceed 2 K.                                                                                                                                                             |                       |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

Response Syntax
---------------

.. code-block::

   HTTP/1.1 status_code
    Server: Server Name
    x-amz-request-id: request id
    x-amz-id-2: id
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Content-Type: type
    Location: location
    Date: date
    ETag: etag

Response Headers
----------------

This response uses common headers. For details about common response headers, see section :ref:`Common Response Headers <en-us_topic_0125560484>`. This response also uses one optional header, as described in :ref:`Table 3 <en-us_topic_0125560263__table15828906>`.

.. _en-us_topic_0125560263__table15828906:

.. table:: **Table 3** Optional response header

   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Header                            | Description                                                                                                                                                                                                                                  |
   +===================================+==============================================================================================================================================================================================================================================+
   | x-amz-version-id                  | Indicates the version ID of an object. The version ID of an object will be returned if the bucket housing the object has versioning enabled. A string "**null**" will be returned if the bucket housing the object has versioning suspended. |
   |                                   |                                                                                                                                                                                                                                              |
   |                                   | Type: String                                                                                                                                                                                                                                 |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access-Control-Allow-Origin       | CORS is configured for buckets. If **Origin** in the request meets the CORS configuration requirements, **Origin** is included in the response.                                                                                              |
   |                                   |                                                                                                                                                                                                                                              |
   |                                   | Type: String                                                                                                                                                                                                                                 |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access-Control-Allow-Headers      | CORS is configured for buckets. If **headers** in the request meet the CORS configuration requirements, **headers** are included in the response.                                                                                            |
   |                                   |                                                                                                                                                                                                                                              |
   |                                   | Type: String                                                                                                                                                                                                                                 |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access-Control-Max-Age            | Indicates **MaxAgeSeconds** in the CORS configuration of a server when CORS is configured for buckets.                                                                                                                                       |
   |                                   |                                                                                                                                                                                                                                              |
   |                                   | Type: Integer                                                                                                                                                                                                                                |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access-Control-Allow-Methods      | CORS is configured for buckets. If **Access-Control-Request-Method** in the request meets the CORS configuration requirements, methods in the rule are included in the response.                                                             |
   |                                   |                                                                                                                                                                                                                                              |
   |                                   | Type: String                                                                                                                                                                                                                                 |
   |                                   |                                                                                                                                                                                                                                              |
   |                                   | Valid values: **GET**, **PUT**, **HEAD**, **POST**, and **DELETE**                                                                                                                                                                           |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access-Control-Expose-Headers     | Indicates **ExposeHeader** in the CORS configuration of a server when CORS is configured for buckets.                                                                                                                                        |
   |                                   |                                                                                                                                                                                                                                              |
   |                                   | Type: String                                                                                                                                                                                                                                 |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Response Elements
-----------------

This response involves no elements.

Error Responses
---------------

No special error responses are returned. For details about error responses, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`.

Sample Request
--------------

.. code-block:: text

   POST / HTTP/1.1
    Date: Fri, 18 Nov 2011 01:19:49 GMT
    Host: bucketname.obs.example.com
    Content-Type: multipart/form-data; boundary=---------------------------7db143f50da2
    Content-Length: 2424


    -----------------------------7db143f50da2
    Content-Disposition: form-data; name="key"
    object01
    -----------------------------7db143f50da2
    Content-Disposition: form-data; name="acl"
    public-read
    -----------------------------7db143f50da2
    Content-Disposition: form-data; name="content-type"
    text/plain
    -----------------------------7db143f50da2
    Content-Disposition: form-data; name="expires"
    1000
    -----------------------------7db143f50da2
    Content-Disposition: form-data; name="AWSAccessKeyId"
    14RZT432N80TGDF2Y2G2
    -----------------------------7db143f50da2
    Content-Disposition: form-data; name="policy"
    ewogICJleHBpcmF0aW9uIjogIjIwMTItMDEtMDFUMTI6MDA6MDAuMDAwWiIsCiAgImNvbmRpdGlvbnMiOiBbCiAgICB7ImJ1Y2tldCI6ICJ0Yy5wb3N0LmV4cGlyZXMuMDAxIiB9LAogICAgeyJhY2wiOiAicHVibGljLXJlYWQiIH0sCiAgICB7IkV4cGlyZXMiOiAiMTAwMCIgfSwKICAgIFsiZXEiLCAiJGtleSIsICJvYmplY3QwMSJdLAogICAgWyJzdGFydHMtd2l0aCIsICIkQ29udGVudC1UeXBlIiwgInRleHQvIl0sCiAgXQp9Cg==
    -----------------------------7db143f50da2
    Content-Disposition: form-data; name="signature"
    Vk6rwO0Nq09BLhvNSIYwSJTRQ+k=
    -----------------------------7db143f50da2
    Content-Disposition: form-data; name="file"; filename="C:\Testtools\UpLoadFiles\object\1024Bytes.txt"
    Content-Type: text/plain
    01234567890
    -----------------------------7db143f50da2
    Content-Disposition: form-data; name="submit"
    Upload
    -----------------------------7db143f50da2--

Sample Response for Uploading Objects to a Bucket with No Versioning Configured
-------------------------------------------------------------------------------

.. code-block::

   HTTP/1.1 204 No Content
    Server: OBS
    x-amz-request-id: 90E2BA00C26C00000133B442A90063FD
    x-amz-id-2: OTBFMkJBMDBDMjZDMDAwMDAxMzNCNDQyQTkwMDYzRkRBQUFBQUFBQWJiYmJiYmJi
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Content-Type: text/xml
    Location: http://obs.example.com/tc.post.expires.001/object01
    Date: Fri, 18 Nov 2011 01:20:27 GMT
    ETag: "ab7abb0da4bca5323ab6119bb5dcd296"

Sample Response for Uploading Objects to a Bucket with Versioning Enabled
-------------------------------------------------------------------------

.. code-block::

   HTTP/1.1 204 No Content
    Server: OBS
    x-amz-request-id: DCD2FC9CAB780000014394C8D18D7A7F
    x-amz-id-2: ebDwZjh64WVojaUVqPaWaXPqqfqLcp15DNr1KkAkP9EXyWrLsrqQoUs1Xn49VC9h
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Content-Type: text/xml
    Location: http://192.168.69.11/example/testfile.txt
    ETag: "098f6bcd4621d373cade4e832627b4f6"
    x-amz-version-id: AAABQ5TI0anc0vycq3gAAAAyVURTRkha
    Date: Wed, 15 Jan 2014 07:23:45 GMT

Sample Response for Uploading Objects to a Bucket with Versioning Suspended
---------------------------------------------------------------------------

.. code-block::

   HTTP/1.1 204 No Content
    Server: OBS
    x-amz-request-id: DCD2FC9CAB780000014394F041CA8F94
    x-amz-id-2: 8EUVTpv5QBvTslQVlaDrzEauRpDP9fusd4IiJrgjExdPlyz+xleFMCNZD/zK0aZg
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Content-Type: text/xml
    Location: http://192.168.69.11/example/testfile.txt
    ETag: "cc03e747a6afbbcbf8be7668acfebee5"
    x-amz-version-id: null
    Date: Wed, 15 Jan 2014 08:06:50 GMT
