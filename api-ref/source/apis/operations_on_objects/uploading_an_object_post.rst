:original_name: obs_04_0081.html

.. _obs_04_0081:

Uploading an Object - POST
==========================

Functions
---------

This operation uploads an object to a bucket. To use this operation, you must have the write permission for the bucket.

.. note::

   The name of each object in a bucket must be unique.

With versioning not enabled, if an object to be uploaded has the same name as an existing object in the bucket, the newly uploaded object will overwrite the existing one. To protect data from being corrupted during transmission, you can add the **Content-MD5** parameter in the form field. After receiving the uploaded object, OBS compares the provided MD5 value to the MD5 value it calculates. If the two values do not match, OBS reports an error. You can also specify the value of the **x-obs-acl** parameter to configure an access control policy for the object.

You can also upload an object using the POST method.

For a single upload, the size of the object to be uploaded ranges [0, 5 GB]. To upload a file greater than 5 GB, see :ref:`Operations on Multipart Upload <obs_04_0096>`.

Differences Between PUT and POST Methods
----------------------------------------

Parameters are passed through the request header if the PUT method is used to upload objects; if the POST method is used to upload objects, parameters are passed through the form field in the message body.

With the PUT method, you need to specify the object name in the URL, but object name is not required with the POST method, which uses the bucket domain name as the URL. Request lines of these two methods are given as follows:

.. code-block:: text

   PUT /ObjectName HTTP/1.1

.. code-block:: text

   POST / HTTP/1.1

For details about PUT upload, see :ref:`Uploading an Object - PUT <obs_04_0080>`.

Versioning
----------

If versioning is enabled for a bucket, the system automatically generates a unique version ID for the requested object in this bucket and returns the version ID in response header **x-obs-version-id**. If versioning is suspended for a bucket, the version ID of the requested object in this bucket is **null**. For details about the versioning statuses of a bucket, see :ref:`Configuring Versioning for a Bucket <obs_04_0037>`.

WORM
----

If a bucket has WORM enabled, you can configure retention policies for objects in the bucket. You can specify the **x-obs-object-lock-mode** and **x-obs-object-lock-retain-until-date** headers to configure a retention policy when you upload an object. If you do not specify these two headers but have configured a default bucket-level WORM policy, this default policy automatically applies to the object newly uploaded. You can also configure or update a WORM retention policy for an existing object.

.. note::

   When you enable WORM for a bucket, OBS automatically enables versioning for the bucket. WORM protects objects based on the object version IDs. Only object versions with any WORM retention policy configured will be protected. Assume that object **test.txt 001** is protected by WORM. If another file with the same name is uploaded, a new object version **test.txt 002** with no WORM policy configured will be generated. In such case, **test.txt 002** is not protected and can be deleted. When you download an object without specifying a version ID, the current object version (**test.txt 002**) will be downloaded.

Request Syntax
--------------

.. code-block:: text

   POST / HTTP/1.1
   Host: bucketname.obs.region.example.com
   User-Agent: browser_data
   Accept: file_types
   Accept-Language: Regions
   Accept-Encoding: encoding
   Accept-Charset: character_set
   Keep-Alive: 300
   Connection: keep-alive
   Content-Type: multipart/form-data; boundary=9431149156168
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
   Content-Disposition: form-data; name="x-obs-meta-uuid"

   uuid
   --9431149156168
   Content-Disposition: form-data; name="x-obs-meta-tag"

   metadata
   --9431149156168
   Content-Disposition: form-data; name="AccessKeyId"

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

This request contains no parameters.

Request Headers
---------------

This request uses common headers. For details, see :ref:`Table 3 <obs_04_0007__table25197309>`.

If you want to get CORS configuration information, you must use the headers in :ref:`Table 1 <obs_04_0081__table45572552212656>`.

.. _obs_04_0081__table45572552212656:

.. table:: **Table 1** Request headers for obtaining CORS configuration

   +--------------------------------+--------------------------------------------------------------------------------------------------+-----------------------+
   | Header                         | Description                                                                                      | Mandatory             |
   +================================+==================================================================================================+=======================+
   | Origin                         | Origin of the cross-domain request specified by the pre-request. Generally, it is a domain name. | Yes                   |
   |                                |                                                                                                  |                       |
   |                                | Type: string                                                                                     |                       |
   +--------------------------------+--------------------------------------------------------------------------------------------------+-----------------------+
   | Access-Control-Request-Headers | Indicates the HTTP headers of a request. The request can use multiple HTTP headers.              | No                    |
   |                                |                                                                                                  |                       |
   |                                | Type: string                                                                                     |                       |
   +--------------------------------+--------------------------------------------------------------------------------------------------+-----------------------+

Request Elements
----------------

This request uses form elements. :ref:`Table 2 <obs_04_0081__table13225554>` describes the form elements.

.. _obs_04_0081__table13225554:

.. table:: **Table 2** Form elements

   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | Parameter                           | Description                                                                                                                                                                                                                                                                                                     | Mandatory                                                                 |
   +=====================================+=================================================================================================================================================================================================================================================================================================================+===========================================================================+
   | file                                | Specifies the object content uploaded. Both the file name and file path are ignored and will not be used as the object name. The object name is the value of parameter **key**.                                                                                                                                 | Yes                                                                       |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Type: binary content or text                                                                                                                                                                                                                                                                                    |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Constraint: This parameter must be the last parameter in a form. Otherwise, parameters after this parameter will be all discarded. Additionally, each request contains only one file parameter.                                                                                                                 |                                                                           |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | key                                 | Indicates the name of the object to be created.                                                                                                                                                                                                                                                                 | Yes                                                                       |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Type: string                                                                                                                                                                                                                                                                                                    |                                                                           |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | AccessKeyId                         | Access key ID (AK) of the requester.                                                                                                                                                                                                                                                                            | Yes when the constraint is met.                                           |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Type: string                                                                                                                                                                                                                                                                                                    |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Constraint: This parameter is mandatory if there is security policy parameter **policy** or **signature** in the request.                                                                                                                                                                                       |                                                                           |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | policy                              | Indicates the security policy in the request. For details about the policy format, see the policy format in :ref:`Authentication of Signature Carried in the Table Uploaded Through a Browser <obs_04_0012>`.                                                                                                   | Yes when the constraint is met.                                           |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Type: string                                                                                                                                                                                                                                                                                                    |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Constraint: This parameter is mandatory if the bucket provides the **AccessKeyId** (or **signature**).                                                                                                                                                                                                          |                                                                           |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | signature                           | Indicates a signature string calculated based on StringToSign.                                                                                                                                                                                                                                                  | Yes when the constraint is met.                                           |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Type: string                                                                                                                                                                                                                                                                                                    |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Constraint: This parameter is mandatory if the bucket provides the **AccessKeyId** (or **policy**).                                                                                                                                                                                                             |                                                                           |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | token                               | Specifies the AK, signature, and security policy of the request initiator. The priority of a token is higher than that of a specified AK, the request signature, and the security policy of the request initiator.                                                                                              | No                                                                        |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Type: string                                                                                                                                                                                                                                                                                                    |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Example:                                                                                                                                                                                                                                                                                                        |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | In HTML: <input type= "text" name="token" value="ak:signature:policy" />                                                                                                                                                                                                                                        |                                                                           |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | x-obs-acl                           | When creating an object, you can use this parameter in a form to configure the permissions control policy for the object. The predefined common policies are as follows: **private**, **public-read**, **public-read-write**, **public-read-delivered**, and **public-read-write-delivered**.                   | No                                                                        |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Type: string                                                                                                                                                                                                                                                                                                    |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Examples:                                                                                                                                                                                                                                                                                                       |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | In POLICY: {"acl": "public-read" }                                                                                                                                                                                                                                                                              |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | In HTML: <input type="text" name="acl" value="public-read" />                                                                                                                                                                                                                                                   |                                                                           |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | x-obs-grant-read                    | When creating an object, you can use this parameter to grant all users in a domain the permissions to read the object and obtain the object metadata.                                                                                                                                                           | No                                                                        |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Type: string                                                                                                                                                                                                                                                                                                    |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Examples:                                                                                                                                                                                                                                                                                                       |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | In POLICY: {'grant-read': 'id=domainId1' },                                                                                                                                                                                                                                                                     |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | In HTML: <input type="text" name="grant-read" value="id=domainId1" />                                                                                                                                                                                                                                           |                                                                           |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | x-obs-grant-read-acp                | When creating an object, you can use this parameter to grant all users in a domain the permission to obtain the object ACL.                                                                                                                                                                                     | No                                                                        |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Type: string                                                                                                                                                                                                                                                                                                    |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Examples:                                                                                                                                                                                                                                                                                                       |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | In POLICY: {"grant-read-acp": "id=domainId1" },                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | In HTML: <input type="text" name="grant-read-acp" value="id=domainId1" />                                                                                                                                                                                                                                       |                                                                           |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | x-obs-grant-write-acp               | When creating an object, you can use this parameter to grant all users in a domain the permission to write the object ACL.                                                                                                                                                                                      | No                                                                        |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Type: string                                                                                                                                                                                                                                                                                                    |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Examples:                                                                                                                                                                                                                                                                                                       |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | In POLICY: {"grant-write-acp": "id=domainId1" },                                                                                                                                                                                                                                                                |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | In HTML: <input type="text" name="grant-write-acp" value="id=domainId1" />                                                                                                                                                                                                                                      |                                                                           |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | x-obs-grant-full-control            | When creating an object, you can use this parameter to grant all users in a domain the permissions to read the object, obtain the object metadata and ACL, and write the object ACL.                                                                                                                            | No                                                                        |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Type: string                                                                                                                                                                                                                                                                                                    |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Examples:                                                                                                                                                                                                                                                                                                       |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | In POLICY: {"grant-full-control": "id=domainId1" },                                                                                                                                                                                                                                                             |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | In HTML: <input type="text" name="grant-full-control" value="id=domainId1" />                                                                                                                                                                                                                                   |                                                                           |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | Cache-Control,                      | Standard HTTP parameters. OBS records these parameters and returns them when you later download an object or send a HEAD Object request.                                                                                                                                                                        | No                                                                        |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   | Content-Type,                       | Type: string                                                                                                                                                                                                                                                                                                    |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   | Content-Disposition,                | Examples:                                                                                                                                                                                                                                                                                                       |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   | Content-Encoding                    | In POLICY: ["starts-with", "$Content-Type", "text/"],                                                                                                                                                                                                                                                           |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   | Expires                             | In HTML: <input type="text" name="content-type" value="text/plain" />                                                                                                                                                                                                                                           |                                                                           |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | success_action_redirect             | Indicates the address (URL) to which a successfully responded request is redirected.                                                                                                                                                                                                                            | No                                                                        |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | -  If the value is valid and the request is successful, OBS returns status code 303. **Location** contains **success_action_redirect** as well as the bucket name, object name, and object ETag.                                                                                                                |                                                                           |
   |                                     | -  If this parameter value is invalid, OBS ignores this parameter. In such case, the **Location** header is the object address, and OBS returns the response code based on whether the operation succeeds or fails.                                                                                             |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Type: string                                                                                                                                                                                                                                                                                                    |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Examples:                                                                                                                                                                                                                                                                                                       |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | In POLICY: {"success_action_redirect": "http://123458.com"},                                                                                                                                                                                                                                                    |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | In HTML: <input type="text" name="success_action_redirect" value="http://123458.com" />                                                                                                                                                                                                                         |                                                                           |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | x-obs-meta-\*                       | Indicates user-defined metadata. When creating an object, you can use this parameter or a parameter starting with **x-obs-meta-** in a form to define object metadata in an HTTP request. The user-defined metadata will be returned in the response when you retrieve the object or query the object metadata. | No                                                                        |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Type: string                                                                                                                                                                                                                                                                                                    |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Examples:                                                                                                                                                                                                                                                                                                       |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | In POLICY: {" x-obs-meta-test ": " test metadata " },                                                                                                                                                                                                                                                           |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | In HTML: <input type="text" name=" x-obs-meta-test " value=" test metadata " />                                                                                                                                                                                                                                 |                                                                           |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | success_action_status               | Indicates the status code returned after the request is successfully received. Possible values are **200**, **201**, and **204**.                                                                                                                                                                               | No                                                                        |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | -  If this parameter is set to **200** or **204**, the body in the OBS response message is empty.                                                                                                                                                                                                               |                                                                           |
   |                                     | -  If this parameter is set to **201**, the OBS response message contains an XML document that describes the response to the request.                                                                                                                                                                           |                                                                           |
   |                                     | -  If the request does not include this parameter or the parameter value is invalid, OBS returns status code **204**.                                                                                                                                                                                           |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Type: string                                                                                                                                                                                                                                                                                                    |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Examples:                                                                                                                                                                                                                                                                                                       |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | In POLICY: ["starts-with", "$success_action_status", ""],                                                                                                                                                                                                                                                       |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | In HTML: <input type="text" name="success_action_status" value="200" />                                                                                                                                                                                                                                         |                                                                           |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | x-obs-website-redirect-location     | If a bucket is configured with static website hosting, and a request redirection is configured for an object in the bucket (either redirection to another object in the same bucket or to an external URL), OBS stores the value of this parameter in the object metadata.                                      | No                                                                        |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Default value: none                                                                                                                                                                                                                                                                                             |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Constraint: The value must start with a slash (/), **http://**, or **https://**, and cannot exceed 2 KB.                                                                                                                                                                                                        |                                                                           |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | x-obs-expires                       | Specifies when an object expires. It is measured in days. Once the object expires, it is automatically deleted. (The calculation starts from when the object was last modified).                                                                                                                                | No                                                                        |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Type: integer                                                                                                                                                                                                                                                                                                   |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Example: **x-obs-expires:3**                                                                                                                                                                                                                                                                                    |                                                                           |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | x-obs-object-lock-mode              | WORM mode that will be applied to the object. Currently, only **COMPLIANCE** is supported. This header must be used together with **x-obs-object-lock-retain-until-date**.                                                                                                                                      | No, but required when **x-obs-object-lock-retain-until-date** is present. |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Type: string                                                                                                                                                                                                                                                                                                    |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Example: **x-obs-object-lock-mode:COMPLIANCE**                                                                                                                                                                                                                                                                  |                                                                           |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | x-obs-object-lock-retain-until-date | Indicates the expiration time of the Object Lock retention. The value must be a UTC time that complies with ISO 8601, for example, **2015-07-01T04:11:15Z**. This header must be used together with **x-obs-object-lock-mode**.                                                                                 | No, but required when **x-obs-object-lock-mode** is present.              |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Type: string                                                                                                                                                                                                                                                                                                    |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Example: **x-obs-object-lock-retain-until-date:2015-07-01T04:11:15Z**                                                                                                                                                                                                                                           |                                                                           |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+

Response Syntax
---------------

::

   HTTP/1.1 status_code
   Content-Type: application/xml
   Location: location
   Date: date
   ETag: etag

Response Headers
----------------

The response to the request uses common headers. For details, see :ref:`Table 1 <obs_04_0013__d0e686>`.

In addition to the common response headers, the headers listed in :ref:`Table 3 <obs_04_0081__table35215532173747>` may be used.

.. _obs_04_0081__table35215532173747:

.. table:: **Table 3** Additional response headers

   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Header                            | Description                                                                                                                                                                                       |
   +===================================+===================================================================================================================================================================================================+
   | x-obs-version-id                  | Object version ID. If versioning is enabled for the bucket, the object version ID will be returned. A string **null** will be returned if the bucket housing the object has versioning suspended. |
   |                                   |                                                                                                                                                                                                   |
   |                                   | Type: string                                                                                                                                                                                      |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access-Control-Allow-Origin       | Indicates that the origin is included in the response if the origin in the request meets the CORS configuration requirements when CORS is configured for buckets.                                 |
   |                                   |                                                                                                                                                                                                   |
   |                                   | Type: string                                                                                                                                                                                      |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access-Control-Allow-Headers      | Indicates that the headers are included in the response if headers in the request meet the CORS configuration requirements when CORS is configured for buckets.                                   |
   |                                   |                                                                                                                                                                                                   |
   |                                   | Type: string                                                                                                                                                                                      |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access-Control-Max-Age            | Indicates MaxAgeSeconds in the CORS configuration of the server when CORS is configured for buckets.                                                                                              |
   |                                   |                                                                                                                                                                                                   |
   |                                   | Type: integer                                                                                                                                                                                     |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access-Control-Allow-Methods      | Indicates that methods in the rule are included in the response if Access-Control-Request-Method in the request meets the CORS configuration requirements when CORS is configured for buckets.    |
   |                                   |                                                                                                                                                                                                   |
   |                                   | Type: string                                                                                                                                                                                      |
   |                                   |                                                                                                                                                                                                   |
   |                                   | Value options: **GET**, **PUT**, **HEAD**, **POST**, **DELETE**                                                                                                                                   |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access-Control-Expose-Headers     | Value of **ExposeHeader** in the CORS configuration of a server when CORS is configured for buckets.                                                                                              |
   |                                   |                                                                                                                                                                                                   |
   |                                   | Type: string                                                                                                                                                                                      |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Response Elements
-----------------

This response contains no elements.

Error Responses
---------------

No special error responses are returned. For details about error responses, see :ref:`Table 2 <obs_04_0115__d0e843>`.

Sample Request: Uploading an Object Using POST
----------------------------------------------

.. code-block:: text

   POST / HTTP/1.1
   Date: WED, 01 Jul 2015 04:15:23 GMT
   Host: examplebucket.obs.region.example.com
   Content-Type: multipart/form-data; boundary=7db143f50da2
   Content-Length: 2424
   Origin: www.example.com
   Access-Control-Request-Headers:acc_header_1

   --7db143f50da2
   Content-Disposition: form-data; name="key"

   object01
   --7db143f50da2
   Content-Disposition: form-data; name="acl"

   public-read
   --7db143f50da2
   Content-Disposition: form-data; name="content-type"

   text/plain
   --7db143f50da2
   Content-Disposition: form-data; name="expires"

   WED, 01 Jul 2015 04:16:15 GMT
   --7db143f50da2
   Content-Disposition: form-data; name="AccessKeyId"

   14RZT432N80TGDF2Y2G2
   --7db143f50da2
   Content-Disposition: form-data; name="policy"

   ew0KICAiZXhaaXJhdGlvbiI6ICIyMDE1LTA3LTAxVDEyOjAwOjAwLjAwMFoiLA0KICAiY29uZGl0aW9ucyI6IFsNCiAgICB7ImJ1Y2tldCI6ICJleG1hcGxlYnVja2V0IiB9LA0KICAgIHsiYWNsIjogInB1YmxpYy1yZWFkIiB9LA0KICAgIHsiRXhaaXJlcyI6ICIxMDAwIiB9LA0KICAgIFsiZXEiLCAiJGtleSIsICJvYmplY3QwMSJdLA0KICAgIFsic3RhcnRzLXdpdGgiLCAiJENvbnRlbnQtVHlwZSIsICJ0ZXh0LyJdLA0KICBdDQp9DQo=
   --7db143f50da2
   Content-Disposition: form-data; name="signature"

   Vk6rwO0Nq09BLhvNSIYwSJTRQ+k=
   --7db143f50da2
   Content-Disposition: form-data; name="x-obs-persistent-headers"

   test:dmFsdWUx
   --7db143f50da2
   Content-Disposition: form-data; name="x-obs-grant-read"

   id=52f24s3593as5730ea4f722483579xxx
   --7db143f50da2
   Content-Disposition: form-data; name="x-obs-server-side-encryption"

   http://www.example.com/
   --7db143f50da2
   Content-Disposition: form-data; name="file"; filename="C:\Testtools\UpLoadFiles\object\1024Bytes.txt"
   Content-Type: text/plain

   01234567890
   --7db143f50da2
   Content-Disposition: form-data; name="submit"

   Upload
   --7db143f50da2--

Sample Response: Uploading an Object Using POST
-----------------------------------------------

After CORS is configured for a bucket, the response contains the **Access-Control-\*** information.

::

   HTTP/1.1 204 No Content
   x-obs-request-id: 90E2BA00C26C00000133B442A90063FD
   x-obs-id-2: OTBFMkJBMDBDMjZDMDAwMDAxMzNCNDQyQTkwMDYzRkRBQUFBQUFBQWJiYmJiYmJi
   Access-Control-Allow-Origin: www.example.com
   Access-Control-Allow-Methods: POST,GET,HEAD,PUT
   Access-Control-Allow-Headers: acc_header_01
   Access-Control-Max-Age: 100
   Access-Control-Expose-Headers: exp_header_01
   Content-Type: text/xml
   Location: http://examplebucket.obs.region.example.com/object01
   Date: WED, 01 Jul 2015 04:15:23 GMT
   ETag: "ab7abb0da4bca5323ab6119bb5dcd296"

Sample Request: Using a Token for Authentication
------------------------------------------------

.. code-block:: text

   POST / HTTP/1.1
   Content-Type:multipart/form-data; boundary=9431149156168
   Content-Length: 634
   Host: examplebucket.obs.region.example.com

   --9431149156168
   Content-Disposition: form-data; name="key"
   obj01

   --9431149156168
   Content-Disposition: form-data; name="token"
   UDSIAMSTUBTEST002538:XsVcTzR2/A284oE4VH9qPndGcuE=:eyJjb25kaXRpb25zIjogW3siYnVja2V0IjogInRlc3QzMDAzMDU4NzE2NjI2ODkzNjcuMTIifSwgeyJDb250ZW50LVR5cGUiOiAiYXBwbGljYXRpb24veG1sIn0sIFsiZXEiLCAiJGtleSIsICJvYmoudHh0Il1dLCAiZXhwaXJhdGlvbiI6ICIyMDIyLTA5LTA5VDEyOjA5OjI3WiJ9

   --9431149156168
   Content-Disposition: form-data; name="file"; filename="myfile"
   Content-Type: text/plain
   01234567890

   --9431149156168--
   Content-Disposition: form-data; name="submit"
   Upload to OBS

Sample Response: Using a Token for Authentication
-------------------------------------------------

::

   HTTP/1.1 204 No Content
   Server: OBS
   Location: http://examplebucket.obs.region.example.com/my-obs-object-key-demo
   ETag: "7eda50a430fed940023acb9c4c6a2fff"
   x-obs-request-id: 000001832010443D80F30B649B969C47
   x-obs-id-2: 32AAAUgAIAABAAAQAAEAABAAAQAAEAABCTj0yO9KJd5In+i9pzTgCDVG9vMnk7O/
   Date: Fri,09Sep 2022 02: 24:40 GMT

Sample Request: Specifying an Object Expiration Time
----------------------------------------------------

.. code-block:: text

   POST / HTTP/1.1
   Date: WED, 01 Jul 2015 04:15:23 GMT
   Host: examplebucket.obs.region.example.com
   Content-Type: multipart/form-data; boundary=148828969260233905620870
   Content-Length: 1639
   Origin: www.example.com
   Access-Control-Request-Headers:acc_header_1

   --148828969260233905620870
   Content-Disposition: form-data; name="key"

   object01
   --148828969260233905620870
   Content-Disposition: form-data; name="ObsAccessKeyId"

   55445349414d5354554254455354303030303033
   --148828969260233905620870
   Content-Disposition: form-data; name="signature"

   396246666f6f42793872792f7a3958524f6c44334e4e69763950553d--7db143f50da2
   --148828969260233905620870
   Content-Disposition: form-data; name="policy"

   65794a6c65484270636d463061573975496a6f694d6a41794d7930774e6930784e565178...
   --148828969260233905620870
   Content-Disposition: form-data; name="x-obs-expires"

   4
   --148828969260233905620870
   Content-Disposition: form-data; name="file"; filename="test.txt"
   Content-Type: text/plain

   01234567890
   --148828969260233905620870
   Content-Disposition: form-data; name="submit"

   Upload
   --148828969260233905620870--

Sample Response: Specifying an Object Expiration Time
-----------------------------------------------------

.. code-block::


   HTTP/1.1 204 No Content
   Server: OBS
   Date: Thu, 15 Jun 2023 12:39:03 GMT
   Connection: keep-alive
   Location: http://examplebucket.obs.region.example.com/my-obs-object-key-demo
   x-obs-expiration: expiry-date="Tue, 20 Jun 2023 00:00:00 GMT"
   ETag: "d41d8cd98f00b204e9800998ecf8427e"
   x-obs-request-id: 00000188BF11049553064911000FC30D
   x-obs-id-2: 32AAAUJAIAABAAAQAAEAABAAAQAAEAABCSwj2PcBE0YcoLHUDO7GSj+rVByzjflA
   x-forward-status: 0x40020000000001
   x-dae-api-type: REST.POST.OBJECT

Sample Request: Specifying a Status Code
----------------------------------------

**Set the status code of a successful action to 200.**

.. code-block:: text

   POST /srcbucket HTTP/1.1
   User-Agent: PostmanRuntime/7.26.8
   Accept: */*
   Postman-Token: 667dcc44-1c48-41ba-9e41-9f87d8975089
   Host: obs.region.example.com
   Accept-Encoding: gzip, deflate, br
   Connection: keep-alive
   Content-Type: multipart/form-data; boundary=--------------------------285613759795901770404350
   Content-Length: 1134

   ----------------------------285613759795901770404350
   Content-Disposition: form-data; name="key"

   obj
   ----------------------------285613759795901770404350
   Content-Disposition: form-data; name="ObsAccessKeyId"

   XXXXXXXXXXXXXXX000003
   ----------------------------285613759795901770404350
   Content-Disposition: form-data; name="signature"

   9rc4bVhDPQ7eHtw17hWtYxLnBWU=
   ----------------------------285613759795901770404350
   Content-Disposition: form-data; name="policy"

   eyJleHBpcmF0aW9uIjoiMjAyMy0wNi0xNVQxNDoxMTozNFoiLCAiY29uZGl0aW9ucyI6W3siYnVja2V0Ijoic3JjYnVja2V0MiJ9LHsic3VjY2Vzc19hY3Rpb25fc3RhdHVzIjoiMjAwIn0seyJjb250ZW50LXR5cGUiOiJ0ZXh0L3BsYWluIn0seyJrZXkiOiIzMzMifSxdfQ==
   ----------------------------285613759795901770404350
   Content-Disposition: form-data; name="success_action_status"

   200
   ----------------------------285613759795901770404350
   Content-Disposition: form-data; name="file"; filename="test.txt"
   Content-Type: text/plain


   ----------------------------285613759795901770404350
   Content-Disposition: form-data; name="submit"

   Upload to OBS
   ----------------------------285613759795901770404350--

Sample Response: Specifying a Status Code
-----------------------------------------

**Response to the configuration of success status code 200**

.. code-block::

   HTTP/1.1 200 OK
   Server: OBS
   Date: Thu, 15 Jun 2023 13:12:51 GMT
   Content-Length: 0
   Connection: keep-alive
   Location: http://obs.region.example.com/srcbucket/obj
   ETag: "d41d8cd98f00b204e9800998ecf8427e"
   x-obs-request-id: 00000188BF2FF55F5306426E000FE366
   x-obs-id-2: 32AAAUJAIAABAAAQAAEAABAAAQAAEAABCScDjcXgZ7oMYSVnZnk4+HrClVwLVPTi
   x-forward-status: 0x40020000000001
   x-dae-api-type: REST.POST.OBJECT

Sample Request: Uploading an Object (with a WORM Retention Policy Configured)
-----------------------------------------------------------------------------

.. code-block:: text

   POST /srcbucket HTTP/1.1
   User-Agent: PostmanRuntime/7.26.8
   Accept: */*
   Postman-Token: 4c2f4c7e-2e0b-46c0-b1a7-4a5da560b6a1
   Host: obs.region.example.com
   Accept-Encoding: gzip, deflate, br
   Connection: keep-alive
   Content-Type: multipart/form-data; boundary=--------------------------940435396775653808840608
   Content-Length: 1409

   ----------------------------940435396775653808840608
   Content-Disposition: form-data; name="key"

   obj
   ----------------------------940435396775653808840608
   Content-Disposition: form-data; name="ObsAccessKeyId"

   XXXXXXXXXXXXXXX000003
   ----------------------------940435396775653808840608
   Content-Disposition: form-data; name="signature"

   X/7QiyMYUvxUWk0R5fToeTcgMMU=
   ----------------------------940435396775653808840608
   Content-Disposition: form-data; name="policy"

   eyJleHBpcmF0aW9uIjoiMjAyMy0wNi0xNVQxNDoyMjo1MVoiLCAiY29uZGl0aW9ucyI6W3sieC1vYnMtb2JqZWN0LWxvY2stcmV0YWluLXVudGlsLWRhdGUiOiJUaHUsIDIwIEp1biAyMDIzIDEzOjEyOjUxIEdNVCJ9LHsieC1vYnMtb2JqZWN0LWxvY2stbW9kZSI6IkNPTVBMSUFOQ0UifSx7ImJ1Y2tldCI6InNyY2J1Y2tldDIifSx7ImNvbnRlbnQtdHlwZSI6InRleHQvcGxhaW4ifSx7ImtleSI6IjMzMyJ9LF19
   ----------------------------940435396775653808840608
   Content-Disposition: form-data; name="x-obs-object-lock-mode"

   COMPLIANCE
   ----------------------------940435396775653808840608
   Content-Disposition: form-data; name="x-obs-object-lock-retain-until-date"

   Thu, 20 Jun 2023 13:12:51 GMT
   ----------------------------940435396775653808840608
   Content-Disposition: form-data; name="file"; filename="test.txt"
   Content-Type: text/plain


   ----------------------------940435396775653808840608
   Content-Disposition: form-data; name="submit"

   Upload to OBS
   ----------------------------940435396775653808840608--

Sample Response: Uploading an Object (with a WORM Retention Policy Configured)
------------------------------------------------------------------------------

.. code-block::

   HTTP/1.1 204 No Content
   Server: OBS
   Date: Thu, 15 Jun 2023 13:24:03 GMT
   Connection: keep-alive
   Location: http://obs.region.example.com/srcbucket/obj
   ETag: "d41d8cd98f00b204e9800998ecf8427e"
   x-obs-request-id: 00000188BF3A36EE5306427D000FEE0A
   x-obs-id-2: 32AAAUJAIAABAAAQAAEAABAAAQAAEAABCS/5pj0p0hAQcDVI3B6E5y167zy4eAQv
   x-forward-status: 0x40020000000001
   x-dae-api-type: REST.POST.OBJECT
