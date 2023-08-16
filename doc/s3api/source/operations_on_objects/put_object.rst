:original_name: en-us_topic_0125560399.html

.. _en-us_topic_0125560399:

PUT Object
==========

After creating a bucket in OBS, you can use this operation to upload an object to the bucket.

Uploading an object adds it to a bucket. This operation requires users to have the write permission.

.. note::

   The objects uploaded by users are stored in buckets. Only the users with the write permission can upload objects to buckets. The names of objects in the same bucket must be unique.

If objects with the same object keys exist in a specified bucket, the new objects uploaded by a user will overwrite the original objects.

To prevent data from being damaged during the transfer process, users can add **Content-MD5** to request headers. After OBS receives the objects that are uploaded, it executes MD5 verification and returns an error if inconsistency is detected.

Users can specify the **x-amz-acl** parameter and set a permission control policy when uploading objects.

After creating a bucket in OBS, you can send a **PUT Object** request to upload an object to the bucket.

Versioning
----------

If a bucket has versioning enabled, the system automatically generates a unique version ID for the requested object in this bucket and returns the version ID in response header **x-amz-version-id**. If a bucket has versioning suspended, the version ID of the requested object in this bucket is **null**. For details about bucket versioning, see section :ref:`PUT Bucket versioning <en-us_topic_0125560444>`.

Request Syntax
--------------

.. code-block:: text

   PUT /ObjectName HTTP/1.1
    User-Agent: agent
    Host: bucketname.obs.example.com
    Accept: */*
    Content-Type: type
    Content-Length: length
    Authorization: authorization
    Date: date
    <Optional Additional Header>

   <object Content>

Request Parameters
------------------

This request involves no parameters.

Request Headers
---------------

You can add optional headers to this request. For details about the optional headers, see :ref:`Table 1 <en-us_topic_0125560399__table21799862>`.

.. _en-us_topic_0125560399__table21799862:

.. table:: **Table 1** Optional request headers

   +---------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | Header                          | Description                                                                                                                                                                                                                                                                 | Remarks                                                                          |
   +=================================+=============================================================================================================================================================================================================================================================================+==================================================================================+
   | Content-MD5                     | The MD5 digest string of the message body is calculated according to the RFC 1864 standard. That is, calculate the 128-bit binary array (the message header data encrypted with MD5) first, and then use Base 64 encoding to convert the binary data to a character string. | Optional                                                                         |
   |                                 |                                                                                                                                                                                                                                                                             |                                                                                  |
   |                                 | Type: String                                                                                                                                                                                                                                                                |                                                                                  |
   |                                 |                                                                                                                                                                                                                                                                             |                                                                                  |
   |                                 | Example: **n58IG6hfM7vqI4K0vnWpog==**                                                                                                                                                                                                                                       |                                                                                  |
   +---------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | x-amz-acl                       | Indicates the ACL applied to an object.                                                                                                                                                                                                                                     | Optional                                                                         |
   |                                 |                                                                                                                                                                                                                                                                             |                                                                                  |
   |                                 | The value of this header is a predefined character string that is not user-configurable.                                                                                                                                                                                    |                                                                                  |
   |                                 |                                                                                                                                                                                                                                                                             |                                                                                  |
   |                                 | Possible values are **private**, **public-read**, **public-read-write**, **authenticated-read**, **bucket-owner-read**, and **bucket-owner-full-control**. For further details, see :ref:`Table 4 <en-us_topic_0125560406__table40200743>`.                                 |                                                                                  |
   |                                 |                                                                                                                                                                                                                                                                             |                                                                                  |
   |                                 | Type: String                                                                                                                                                                                                                                                                |                                                                                  |
   +---------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | x-amz-meta-\*                   | This prefix is used to construct a header in an HTTP request for returning self-defined metadata. If this prefix is specified, user-defined metadata is returned in one or more response headers prefixed with **x-amz-meta-**.                                             | Optional                                                                         |
   |                                 |                                                                                                                                                                                                                                                                             |                                                                                  |
   |                                 | Note: The format of the user-defined metadata header is x-amz-meta-key:value. The total size of the key and value of all user-defined metadata in the request cannot exceed 2 KB.                                                                                           |                                                                                  |
   |                                 |                                                                                                                                                                                                                                                                             |                                                                                  |
   |                                 | Type: String                                                                                                                                                                                                                                                                |                                                                                  |
   |                                 |                                                                                                                                                                                                                                                                             |                                                                                  |
   |                                 | Example:                                                                                                                                                                                                                                                                    |                                                                                  |
   |                                 |                                                                                                                                                                                                                                                                             |                                                                                  |
   |                                 | x-amz-meta-test: test metadata                                                                                                                                                                                                                                              |                                                                                  |
   +---------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | x-amz-website-redirect-location | If a bucket is configured as a website, redirects requests for this object to another object in the same bucket or to an external URL.                                                                                                                                      | Optional                                                                         |
   |                                 |                                                                                                                                                                                                                                                                             |                                                                                  |
   |                                 | OBS stores the value of this header in the object metadata.                                                                                                                                                                                                                 |                                                                                  |
   |                                 |                                                                                                                                                                                                                                                                             |                                                                                  |
   |                                 | In the following example, the request header sets the redirection to an object (anotherPage.html) in the same bucket:                                                                                                                                                       |                                                                                  |
   |                                 |                                                                                                                                                                                                                                                                             |                                                                                  |
   |                                 | x-amz-website-redirect-location:/anotherPage.html                                                                                                                                                                                                                           |                                                                                  |
   |                                 |                                                                                                                                                                                                                                                                             |                                                                                  |
   |                                 | In the following example, the request header sets the object redirection to an external URL:                                                                                                                                                                                |                                                                                  |
   |                                 |                                                                                                                                                                                                                                                                             |                                                                                  |
   |                                 | x-amz-website-redirect-location:http://www.example.com/                                                                                                                                                                                                                     |                                                                                  |
   |                                 |                                                                                                                                                                                                                                                                             |                                                                                  |
   |                                 | Type: String                                                                                                                                                                                                                                                                |                                                                                  |
   |                                 |                                                                                                                                                                                                                                                                             |                                                                                  |
   |                                 | Default: None                                                                                                                                                                                                                                                               |                                                                                  |
   |                                 |                                                                                                                                                                                                                                                                             |                                                                                  |
   |                                 | Constraint: The value must be prefixed by a slash (/), **http://**, or **https://**. The length of the value cannot exceed 2 K.                                                                                                                                             |                                                                                  |
   +---------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | x-amz-security-token            | Header field used to identify the request of a federated user. When the federal authentication function is enabled, users sending such requests are identified as federated users.                                                                                          | Optional. This parameter must be carried in the request sent by federated users. |
   |                                 |                                                                                                                                                                                                                                                                             |                                                                                  |
   |                                 | Type: string                                                                                                                                                                                                                                                                |                                                                                  |
   +---------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+

Request Elements
----------------

This request involves no elements. Its body contains only the content of the requested object.

Response Syntax
---------------

.. code-block::

   HTTP/1.1 status_code
    Server: Server Name
    x-amz-request-id: request id
    x-amz-id-2: id
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    ETag: etag
    Date: date
    Content-Length: length
    Content-Type: type

Response Headers
----------------

This response uses common headers. For details about common response headers, see section :ref:`Common Response Headers <en-us_topic_0125560484>`.

This response also uses optional headers, as described in :ref:`Table 2 <en-us_topic_0125560399__table8944551125949>`.

.. _en-us_topic_0125560399__table8944551125949:

.. table:: **Table 2** Optional response headers

   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------+
   | Header                            | Description                                                                                                                                  |
   +===================================+==============================================================================================================================================+
   | x-amz-version-id                  | Indicates the version ID of an object. The version ID of an object will be returned if the bucket housing the object has versioning enabled. |
   |                                   |                                                                                                                                              |
   |                                   | Type: String                                                                                                                                 |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------+

Response Elements
-----------------

This response involves no elements.

Error Responses
---------------

No special error responses are returned. For details about error responses, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`.

Sample Request
--------------

.. code-block:: text

   PUT /object02 HTTP/1.1
    User-Agent: Jakarta Commons-HttpClient/3.1
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Sat, 03 Dec 2011 07:12:31 +0000
    Authorization: AWS BF6C09F302931425E9A7:KUxrlwKGWYpUOTgwNxIHALsRdT4=
    x-amz-meta-key: value
    Content-Length: 256

    1234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456

Sample Request for Redirecting Object Location
----------------------------------------------

.. code-block:: text

   PUT /object02 HTTP/1.1
   User-Agent: Jakarta Commons-HttpClient/3.1
   Host: bucketname.obs.example.com
   Accept: */*
   Date: Sat, 03 Dec 2011 07:12:31 +0000
   Authorization: AWS BF6C09F302931425E9A7:KUxrlwKGWYpUOTgwNxIHALsRdT4=
   x-amz-meta-key: value
   Content-Length: 256
   x-amz-website-redirect-location: www.example.com
   1234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456

Sample Response for Uploading Objects to a Bucket with No Versioning Configured
-------------------------------------------------------------------------------

.. code-block::

   HTTP/1.1 200 OK
    Server: OBS
    x-amz-request-id: 001B21A61C6C0000013402C4616D5285
    x-amz-id-2: MDAxQjIxQTYxQzZDMDAwMDAxMzQwMkM0NjE2RDUyODVBQUFBQUFBQWJiYmJiYmJi
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon
    Technologies, Inc
    Content-Type: text/xml
    ETag: "33bee59f4c1f859a7aedd36779b321cf"
    Date: Sat, 03 Dec 2011 07:12:31 GMT
    Content-Length: 0

Sample Response for Uploading Objects to a Bucket with Versioning Enabled
-------------------------------------------------------------------------

.. code-block::

   HTTP/1.1 200 OK
    Server: OBS
    x-amz-request-id: DCD2FC9CAB78000001438AB633CF1A73
    x-amz-id-2: zvOE6GmblPrMk544Fg7BEt4LAmwdRuPx5s2qDVeGHZZJhUMmdxKsW4MzeJLkoVvX
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Content-Type: text/xml
    ETag: "ba1f2511fc30423bdbb183fe33f3dd0f"
    x-amz-version-id: AAABQ4q2M9_c0vycq3gAAAAAVURTRkha
    Date: Mon, 13 Jan 2014 08:27:13 GMT
    Content-Length: 0

Sample Response for Uploading Objects to a Bucket with Versioning Suspended
---------------------------------------------------------------------------

.. code-block::

   HTTP/1.1 200 OK
    Server: OBS
    x-amz-request-id: DCD2FC9CAB78000001439A51DB2B2577
    x-amz-id-2: GcVgfeOJHx8JZHTHrRqkPsbKdB583fYbr3RBbHT6mMrBstReVILBZbMAdLiBYy1l
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Content-Type: text/xml
    ETag: "0b55edbacf50d5086ea83ee08e55cbbd"
    Date: Thu, 13 Jan 2014 09:11:32 GMT
    Content-Length: 0
