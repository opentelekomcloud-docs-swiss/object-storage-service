:original_name: obs_04_0080.html

.. _obs_04_0080:

Uploading an Object - PUT
=========================

Functions
---------

After creating a bucket in OBS, you can use this operation to upload an object to the bucket. This operation uploads an object to a bucket. To use this operation, you must have the write permission for the bucket.

.. note::

   The name of each object in a bucket must be unique.

With versioning not enabled, if an object to be uploaded has the same name as an existing object in the bucket, the newly uploaded object will overwrite the existing one. To protect data from being corrupted during transmission, you can add the **Content-MD5** header in the request. After receiving the uploaded object, OBS compares the provided MD5 value to the MD5 value it calculates. If the two values do not match, OBS reports an error.

You can also specify the value of the **x-obs-acl** parameter to configure an access control policy for the object. If the **x-obs-acl** parameter is not specified when an anonymous user uploads an object, the object can be accessed by all OBS users by default.

For a single upload, the size of the object to be uploaded ranges [0, 5 GB]. To upload a file greater than 5 GB, see :ref:`Operations on Multipart Upload <obs_04_0096>`.

OBS does not have real folders. To facilitate data management, OBS provides a method to simulate a folder by adding a slash (/) to the object name, for example, **test/123.jpg**. You can simulate **test** as a folder and **123.jpg** as the name of a file under the **test** folder. However, the object key remains **test/123.jpg**. Objects named in this format appear as folders on the console. When you upload an object larger than 0 in size using this format, an empty folder will be displayed on the console, but the occupied storage capacity is the actual object size.

Differences Between PUT and POST Methods
----------------------------------------

Parameters are passed through the request header if the PUT method is used to upload objects; if the POST method is used to upload objects, parameters are passed through the form field in the message body.

With the PUT method, you need to specify the object name in the URL, but object name is not required with the POST method, which uses the bucket domain name as the URL. Request lines of these two methods are given as follows:

.. code-block:: text

   PUT /ObjectName HTTP/1.1

.. code-block:: text

   POST / HTTP/1.1

.. note::

   In a PUT request, if you write the message body in POST format, the object uploaded to OBS will be displayed in a form.

For details about POST upload, see :ref:`Uploading an Object - POST <obs_04_0081>`.

Versioning
----------

If versioning is enabled for a bucket, the system automatically generates a unique version ID for the requested object in this bucket and returns the version ID in response header **x-obs-version-id**. If versioning is suspended for the bucket, the object version ID is **null**. For details about the versioning statuses of a bucket, see :ref:`Configuring Versioning for a Bucket <obs_04_0037>`.

WORM
----

If a bucket has WORM enabled, you can configure retention policies for objects in the bucket. You can specify the **x-obs-object-lock-mode** and **x-obs-object-lock-retain-until-date** headers to configure a retention policy when you upload an object. If you do not specify these two headers but have configured a default bucket-level WORM policy, this default policy automatically applies to the object newly uploaded. You can also configure or update a WORM retention policy for an existing object.

.. note::

   When you enable WORM for a bucket, OBS automatically enables versioning for the bucket. WORM protects objects based on the object version IDs. Only object versions with any WORM retention policy configured will be protected. Assume that object **test.txt 001** is protected by WORM. If another file with the same name is uploaded, a new object version **test.txt 002** with no WORM policy configured will be generated. In such case, **test.txt 002** is not protected and can be deleted. When you download an object without specifying a version ID, the current object version (**test.txt 002**) will be downloaded.

Request Syntax
--------------

.. code-block:: text

   PUT /ObjectName HTTP/1.1
   Host: bucketname.obs.region.example.com
   Content-Type: application/xml
   Content-Length: length
   Authorization: authorization
   Date: date
   <Optional Additional Header>
   <object Content>

Request Parameters
------------------

This request contains no parameters.

Request Headers
---------------

This request uses common headers. For details, see :ref:`Table 3 <obs_04_0007__table25197309>`. The request can use additional headers, as listed in :ref:`Table 1 <obs_04_0080__table21799862>`.

.. note::

   OBS supports the six HTTP request headers: Cache-Control, Expires, Content-Encoding, Content-Disposition, Content-Type, and Content-Language. If these headers are carried in an object upload request, their values are saved. You can also call the metadata modification API, provided by OBS, to change the values of the six headers. When the object is downloaded or queried, the saved values are set for corresponding HTTP headers and returned to the client.

.. _obs_04_0080__table21799862:

.. table:: **Table 1** Request headers

   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | Header                              | Description                                                                                                                                                                                                                                     | Mandatory                                                                 |
   +=====================================+=================================================================================================================================================================================================================================================+===========================================================================+
   | Content-MD5                         | Base64-encoded 128-bit MD5 digest of the message according to RFC 1864.                                                                                                                                                                         | No                                                                        |
   |                                     |                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Type: string                                                                                                                                                                                                                                    |                                                                           |
   |                                     |                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Example: **n58IG6hfM7vqI4K0vnWpog==**                                                                                                                                                                                                           |                                                                           |
   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | x-obs-acl                           | This header can be added to set access control policies for objects when creating the objects. The access control policies are the predefined common policies, including **private**, **public-read**, **public-read-write**.                   | No                                                                        |
   |                                     |                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Type: string                                                                                                                                                                                                                                    |                                                                           |
   |                                     |                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Note: This header is a predefined policy expressed in a character string.                                                                                                                                                                       |                                                                           |
   |                                     |                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Example: **x-obs-acl: public-read**                                                                                                                                                                                                             |                                                                           |
   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | x-obs-grant-read                    | When creating an object, you can use this header to grant all users in an account the permissions to read the object and obtain the object metadata.                                                                                            | No                                                                        |
   |                                     |                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Type: string                                                                                                                                                                                                                                    |                                                                           |
   |                                     |                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Example: **x-obs-grant-read: id=domainID**. If multiple accounts are authorized, separate them with commas (,).                                                                                                                                 |                                                                           |
   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | x-obs-grant-read-acp                | When creating an object, you can use this header to grant all users in an account the permissions to obtain the object ACL.                                                                                                                     | No                                                                        |
   |                                     |                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Type: string                                                                                                                                                                                                                                    |                                                                           |
   |                                     |                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Example: **x-obs-grant-read-acp: id=domainID**. If multiple accounts are authorized, separate them with commas (,).                                                                                                                             |                                                                           |
   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | x-obs-grant-write-acp               | When creating an object, you can use this header to grant all users in an account the permission to write the object ACL.                                                                                                                       | No                                                                        |
   |                                     |                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Type: string                                                                                                                                                                                                                                    |                                                                           |
   |                                     |                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Example: **x-obs-grant-write-acp: id=domainID**. If multiple accounts are authorized, separate them with commas (,).                                                                                                                            |                                                                           |
   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | x-obs-grant-full-control            | When creating an object, you can use this header to grant all users in an account the permissions to read the object, obtain the object metadata and ACL, and write the object ACL.                                                             | No                                                                        |
   |                                     |                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Type: string                                                                                                                                                                                                                                    |                                                                           |
   |                                     |                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Example: **x-obs-grant-full-control: id=domainID**. If multiple accounts are authorized, separate them with commas (,).                                                                                                                         |                                                                           |
   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | x-obs-meta-\*                       | When creating an object, you can use a header starting with **x-obs-meta-** to define object metadata in an HTTP request. The user-defined metadata will be returned in the response when you retrieve the object or query the object metadata. | No                                                                        |
   |                                     |                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Type: string                                                                                                                                                                                                                                    |                                                                           |
   |                                     |                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Example: **x-obs-meta-test: test metadata**                                                                                                                                                                                                     |                                                                           |
   |                                     |                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Constraint: Both user-defined metadata keys and their values must conform to US-ASCII standards.                                                                                                                                                |                                                                           |
   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | x-obs-website-redirect-location     | If a bucket is configured with the static website hosting function, it will redirect requests for this object to another object in the same bucket or to an external URL. OBS stores the value of this header in the object metadata.           | No                                                                        |
   |                                     |                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | In the following example, the request header sets the redirection to an object (**anotherPage.html**) in the same bucket:                                                                                                                       |                                                                           |
   |                                     |                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | x-obs-website-redirect-location:/anotherPage.html                                                                                                                                                                                               |                                                                           |
   |                                     |                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | In the following example, the request header sets the object redirection to an external URL:                                                                                                                                                    |                                                                           |
   |                                     |                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | x-obs-website-redirect-location:http://www.example.com/                                                                                                                                                                                         |                                                                           |
   |                                     |                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Type: string                                                                                                                                                                                                                                    |                                                                           |
   |                                     |                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Default value: none                                                                                                                                                                                                                             |                                                                           |
   |                                     |                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Constraint: The value must be prefixed by a slash (/), **http://**, or **https://**. The length of the value cannot exceed 2 KB.                                                                                                                |                                                                           |
   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | success-action-redirect             | Indicates the address (URL) to which a successfully responded request is redirected.                                                                                                                                                            | No                                                                        |
   |                                     |                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | -  If the value is valid and the request is successful, OBS returns status code 303. **Location** contains **success_action_redirect** as well as the bucket name, object name, and object ETag.                                                |                                                                           |
   |                                     | -  If this parameter value is invalid, OBS ignores this parameter. In such case, the **Location** header is the object address, and OBS returns the response code based on whether the operation succeeds or fails.                             |                                                                           |
   |                                     |                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Type: string                                                                                                                                                                                                                                    |                                                                           |
   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | x-obs-expires                       | Specifies when an object expires. It is measured in days. Once the object expires, it is automatically deleted. (The validity calculates from the object's creation time.)                                                                      | No                                                                        |
   |                                     |                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | You can configure this field when uploading an object or modify this field by using the metadata modification API after the object is uploaded.                                                                                                 |                                                                           |
   |                                     |                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Type: integer                                                                                                                                                                                                                                   |                                                                           |
   |                                     |                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Example: **x-obs-expires:3**                                                                                                                                                                                                                    |                                                                           |
   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | x-obs-object-lock-mode              | WORM mode that will be applied to the object. Currently, only **COMPLIANCE** is supported. This header must be used together with **x-obs-object-lock-retain-until-date**.                                                                      | No, but required when **x-obs-object-lock-retain-until-date** is present. |
   |                                     |                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Type: string                                                                                                                                                                                                                                    |                                                                           |
   |                                     |                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Example: **x-obs-object-lock-mode:COMPLIANCE**                                                                                                                                                                                                  |                                                                           |
   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | x-obs-object-lock-retain-until-date | Indicates the expiration time of the Object Lock retention. The value must be a UTC time that complies with ISO 8601, for example, **2015-07-01T04:11:15Z**. This header must be used together with **x-obs-object-lock-mode**.                 | No, but required when **x-obs-object-lock-mode** is present.              |
   |                                     |                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Type: string                                                                                                                                                                                                                                    |                                                                           |
   |                                     |                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Example: **x-obs-object-lock-retain-until-date:2015-07-01T04:11:15Z**                                                                                                                                                                           |                                                                           |
   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+

Request Elements
----------------

This request contains no elements. Its body contains only the content of the requested object.

Response Syntax
---------------

::

   HTTP/1.1 status_code
   Content-Length: length
   Content-Type: type

Response Headers
----------------

The response to the request uses common headers. For details, see :ref:`Table 1 <obs_04_0013__d0e686>`.

In addition to the common response headers, the headers listed in :ref:`Table 2 <obs_04_0080__table24122936102344>` may be used.

.. _obs_04_0080__table24122936102344:

.. table:: **Table 2** Additional response headers

   +-----------------------------------+-----------------------------------------------------------------------------------------------------+
   | Header                            | Description                                                                                         |
   +===================================+=====================================================================================================+
   | x-obs-version-id                  | Object version ID. If versioning is enabled for the bucket, the object version ID will be returned. |
   |                                   |                                                                                                     |
   |                                   | Type: string                                                                                        |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------+

Response Elements
-----------------

This response contains no elements.

Error Responses
---------------

No special error responses are returned. For details about error responses, see :ref:`Table 2 <obs_04_0115__d0e843>`.

Sample Request: Uploading an Object
-----------------------------------

.. code-block:: text

   PUT /object01 HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: WED, 01 Jul 2015 04:11:15 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:gYqplLq30dEX7GMi2qFWyjdFsyw=
   Content-Length: 10240
   Expect: 100-continue

   [1024 Byte data content]

Sample Response: Uploading an Object
------------------------------------

::

   HTTP/1.1 200 OK
   Server: OBS
   x-obs-request-id: BF2600000164364C10805D385E1E3C67
   ETag: "d41d8cd98f00b204e9800998ecf8427e"
   x-obs-id-2: 32AAAWJAMAABAAAQAAEAABAAAQAAEAABCTzu4Jp2lquWuXsjnLyPPiT3cfGhqPoY
   Date: WED, 01 Jul 2015 04:11:15 GMT
   Content-Length: 0

Sample Request: Uploading an Object (with the ACL Configured)
-------------------------------------------------------------

.. code-block:: text

   PUT /object01 HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: WED, 01 Jul 2015 04:13:55 GMT
   x-obs-grant-read:id=52f24s3593as5730ea4f722483579ai7,id=a93fcas852f24s3596ea8366794f7224
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:gYqplLq30dEX7GMi2qFWyjdFsyw=
   Content-Length: 10240
   Expect: 100-continue

   [1024 Byte data content]

Sample Response: Uploading an Object (with the ACL Configured)
--------------------------------------------------------------

::

   HTTP/1.1 200 OK
   Server: OBS
   x-obs-request-id: BB7800000164845759E4F3B39ABEE55E
   ETag: "d41d8cd98f00b204e9800998ecf8427e"
   x-obs-id-2: 32AAAQAAEAABAAAQAAEAABAAAQAAEAABCSReVRNuas0knI+Y96iXrZA7BLUgj06Z
   Date: WED, 01 Jul 2015 04:13:55 GMT
   Content-Length: 0

Sample Request: Uploading an Object to a Versioned Bucket
---------------------------------------------------------

.. code-block:: text

   PUT /object01 HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: WED, 01 Jul 2015 04:17:12 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:uFVJhp/dJqj/CJIVLrSZ0gpw3ng=
   Content-Length: 10240
   Expect: 100-continue

   [1024 Byte data content]

Sample Response: Uploading an Object to a Versioned Bucket
----------------------------------------------------------

::

   HTTP/1.1 200 OK
   Server: OBS
   x-obs-request-id: DCD2FC9CAB78000001439A51DB2B2577
   ETag: "d41d8cd98f00b204e9800998ecf8427e"
   X-OBS-ID-2: GcVgfeOJHx8JZHTHrRqkPsbKdB583fYbr3RBbHT6mMrBstReVILBZbMAdLiBYy1l
   Date: WED, 01 Jul 2015 04:17:12 GMT
   x-obs-version-id: AAABQ4q2M9_c0vycq3gAAAAAVURTRkha
   Content-Length: 0

Sample Request: Uploading an Object (with Its MD5 Specified)
------------------------------------------------------------

.. code-block:: text

   PUT /object01 HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: WED, 01 Jul 2015 04:17:50 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:uFVJhp/dJqj/CJIVLrSZ0gpw3ng=
   Content-Length: 10
   Content-MD5: 6Afx/PgtEy+bsBjKZzihnw==
   Expect: 100-continue

   1234567890

Sample Response: Uploading an Object (with Its MD5 Specified)
-------------------------------------------------------------

::

   HTTP/1.1 200 OK
   Server: OBS
   x-obs-request-id: BB7800000164B165971F91D82217D105
   X-OBS-ID-2: 32AAAUJAIAABAAAQAAEAABAAAQAAEAABCSEKhBpS4BB3dSMNqMtuNxQDD9XvOw5h
   ETag: "1072e1b96b47d7ec859710068aa70d57"
   Date: WED, 01 Jul 2015 04:17:50 GMT
   Content-Length: 0

Sample Request: Uploading an Object (with Website Hosting Configured)
---------------------------------------------------------------------

**If static website hosting has been configured for a bucket, you can configure parameters as follows when you upload an object. Then, users will be redirected when they download the object.**

.. code-block:: text

   PUT /object01 HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: WED, 01 Jul 2015 04:17:12 GMT
   x-obs-website-redirect-location: http://www.example.com/
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:uFVJhp/dJqj/CJIVLrSZ0gpw3ng=
   Content-Length: 10240
   Expect: 100-continue

   [1024 Byte data content]

Sample Response: Uploading an Object (with Website Hosting Configured)
----------------------------------------------------------------------

::

   HTTP/1.1 200 OK
   Server: OBS
   x-obs-request-id: DCD2FC9CAB78000001439A51DB2B2577
   x-obs-id-2: 32AAAUJAIAABAAAQAAEAABAAAQAAEAABCTmxB5ufMj/7/GzP8TFwTbp33u0xhn2Z
   ETag: "1072e1b96b47d7ec859710068aa70d57"
   Date: WED, 01 Jul 2015 04:17:12 GMT
   x-obs-version-id: AAABQ4q2M9_c0vycq3gAAAAAVURTRkha
   Content-Length: 0

Sample Request: Uploading an Object Using a Signed URL
------------------------------------------------------

.. code-block:: text

   PUT /object02?AccessKeyId=H4IPJX0TQTHTHEBQQCEC&Expires=1532688887&Signature=EQmDuOhaLUrzrzRNZxwS72CXeXM%3D HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Content-Length: 1024

   [1024 Byte data content]

Sample Response: Uploading an Object Using a Signed URL
-------------------------------------------------------

::

   HTTP/1.1 200 OK
   Server: OBS
   x-obs-request-id: DCD2FC9CAB78000001439A51DB2B2577
   x-obs-id-2: 32AAAUJAIAABAAAQAAEAABAAAQAAEAABCTmxB5ufMj/7/GzP8TFwTbp33u0xhn2Z
   ETag: "1072e1b96b47d7ec859710068aa70d57"
   Date: Fri, 27 Jul 2018 10:52:31 GMT
   x-obs-version-id: AAABQ4q2M9_c0vycq3gAAAAAVURTRkha
   Content-Length: 0

Sample Request: Uploading an Object (with a WORM Retention Policy Configured)
-----------------------------------------------------------------------------

.. code-block:: text

   PUT /object01 HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: WED, 01 Jul 2015 04:11:15 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:gYqplLq30dEX7GMi2qFWyjdFsyw=
   Content-Length: 10240
   x-obs-object-lock-mode:COMPLIANCE
   x-obs-object-lock-retain-until-date:2022-09-24T16:10:25Z
   Expect: 100-continue

   [1024 Byte data content]

Sample Response: Uploading an Object (with a WORM Retention Policy Configured)
------------------------------------------------------------------------------

::

   HTTP/1.1 200 OK
   Server: OBS
   x-obs-request-id: BF2600000164364C10805D385E1E3C67
   ETag: "d41d8cd98f00b204e9800998ecf8427e"
   x-obs-id-2: 32AAAWJAMAABAAAQAAEAABAAAQAAEAABCTzu4Jp2lquWuXsjnLyPPiT3cfGhqPoY
   Date: WED, 01 Jul 2015 04:11:15 GMT
   Content-Length: 0
