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

This request uses common headers. For details, see :ref:`Table 3 <obs_04_0007__table25197309>`. The request can use additional headers shown in :ref:`Table 1 <obs_04_0080__table5707453135616>`.

.. note::

   OBS supports the six HTTP request headers: Cache-Control, Expires, Content-Encoding, Content-Disposition, Content-Type, and Content-Language. If these headers are carried in an object upload request, their values are saved. You can also call the metadata modification API, provided by OBS, to change the values of the six headers. When the object is downloaded or queried, the saved values are set for corresponding HTTP headers and returned to the client.

.. _obs_04_0080__table5707453135616:

.. table:: **Table 1** Request headers

   +-------------------------------------+-----------------+--------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Header                              | Type            | Mandatory (Yes/No)                                                       | Description                                                                                                                                                                                                                           |
   +=====================================+=================+==========================================================================+=======================================================================================================================================================================================================================================+
   | Content-MD5                         | String          | No                                                                       | **Explanation**:                                                                                                                                                                                                                      |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | Base64-encoded 128-bit MD5 digest of the message according to RFC 1864.                                                                                                                                                               |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | Example: **n58IG6hfM7vqI4K0vnWpog==**                                                                                                                                                                                                 |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | **Restrictions**:                                                                                                                                                                                                                     |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | None                                                                                                                                                                                                                                  |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | **Value range**:                                                                                                                                                                                                                      |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | None                                                                                                                                                                                                                                  |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | **Default value**:                                                                                                                                                                                                                    |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | None                                                                                                                                                                                                                                  |
   +-------------------------------------+-----------------+--------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | x-obs-acl                           | String          | No                                                                       | **Explanation**:                                                                                                                                                                                                                      |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | When creating an object, you can use this parameter to set a pre-defined ACL.                                                                                                                                                         |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | **Restrictions**:                                                                                                                                                                                                                     |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | Pre-defined policies must be displayed in character strings.                                                                                                                                                                          |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | **Value range**:                                                                                                                                                                                                                      |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | -  private                                                                                                                                                                                                                            |
   |                                     |                 |                                                                          | -  public-read                                                                                                                                                                                                                        |
   |                                     |                 |                                                                          | -  public-read-write                                                                                                                                                                                                                  |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | **Default value**:                                                                                                                                                                                                                    |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | private                                                                                                                                                                                                                               |
   +-------------------------------------+-----------------+--------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | x-obs-grant-read                    | String          | No                                                                       | **Explanation**:                                                                                                                                                                                                                      |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | When creating an object, you can use this header to grant all users in a domain the permissions to read the object and obtain the object metadata.                                                                                    |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | Example: **x-obs-grant-read: id=**\ *domainID*                                                                                                                                                                                        |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | **Restrictions**:                                                                                                                                                                                                                     |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | Use commas (,) to separate multiple domains.                                                                                                                                                                                          |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | **Value range**:                                                                                                                                                                                                                      |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | The value must be a valid ID. For details, see :ref:`Obtaining a Domain ID and a User ID <obs_04_0117>`.                                                                                                                              |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | **Default value**:                                                                                                                                                                                                                    |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | None                                                                                                                                                                                                                                  |
   +-------------------------------------+-----------------+--------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | x-obs-grant-read-acp                | String          | No                                                                       | **Explanation**:                                                                                                                                                                                                                      |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | When creating an object, you can use this header to grant all users in a domain the permissions to obtain the object ACL.                                                                                                             |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | Example: **x-obs-grant-read-acp: id=**\ *domainID*                                                                                                                                                                                    |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | **Restrictions**:                                                                                                                                                                                                                     |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | Use commas (,) to separate multiple domains.                                                                                                                                                                                          |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | **Value range**:                                                                                                                                                                                                                      |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | The value must be a valid ID. For details, see :ref:`Obtaining a Domain ID and a User ID <obs_04_0117>`.                                                                                                                              |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | **Default value**:                                                                                                                                                                                                                    |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | None                                                                                                                                                                                                                                  |
   +-------------------------------------+-----------------+--------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | x-obs-grant-write-acp               | String          | No                                                                       | **Explanation**:                                                                                                                                                                                                                      |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | When creating an object, you can use this header to grant all users in a domain the permission to write the object ACL.                                                                                                               |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | Example: **x-obs-grant-write-acp: id=**\ *domainID*                                                                                                                                                                                   |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | **Restrictions**:                                                                                                                                                                                                                     |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | Use commas (,) to separate multiple domains.                                                                                                                                                                                          |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | **Value range**:                                                                                                                                                                                                                      |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | The value must be a valid ID. For details, see :ref:`Obtaining a Domain ID and a User ID <obs_04_0117>`.                                                                                                                              |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | **Default value**:                                                                                                                                                                                                                    |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | None                                                                                                                                                                                                                                  |
   +-------------------------------------+-----------------+--------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | x-obs-grant-full-control            | String          | No                                                                       | **Explanation**:                                                                                                                                                                                                                      |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | When creating an object, you can use this header to grant all users in a domain the permissions to read the object, obtain the object metadata and ACL, and write the object ACL.                                                     |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | Example: **x-obs-grant-full-control: id=**\ *domainID*                                                                                                                                                                                |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | **Restrictions**:                                                                                                                                                                                                                     |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | Use commas (,) to separate multiple domains.                                                                                                                                                                                          |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | **Value range**:                                                                                                                                                                                                                      |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | The value must be a valid ID. For details, see :ref:`Obtaining a Domain ID and a User ID <obs_04_0117>`.                                                                                                                              |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | **Default value**:                                                                                                                                                                                                                    |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | None                                                                                                                                                                                                                                  |
   +-------------------------------------+-----------------+--------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | x-obs-storage-class                 | String          | No                                                                       | **Explanation**:                                                                                                                                                                                                                      |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | When creating an object, you can use this header to specify the storage class for the object. If you do not use this header, the object storage class is the default storage class of the bucket.                                     |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | Example: **x-obs-storage-class: STANDARD**                                                                                                                                                                                            |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | **Restrictions**:                                                                                                                                                                                                                     |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | The value is case-sensitive.                                                                                                                                                                                                          |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | **Value range**:                                                                                                                                                                                                                      |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | -  STANDARD                                                                                                                                                                                                                           |
   |                                     |                 |                                                                          | -  WARM                                                                                                                                                                                                                               |
   |                                     |                 |                                                                          | -  COLD                                                                                                                                                                                                                               |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | **Default value**:                                                                                                                                                                                                                    |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | By default, the storage class of the bucket is inherited.                                                                                                                                                                             |
   +-------------------------------------+-----------------+--------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | x-obs-meta-\*                       | String          | No                                                                       | **Explanation**:                                                                                                                                                                                                                      |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | When creating an object, you can use a header starting with **x-obs-meta-** to define object metadata in an HTTP request. Such metadata will be returned in the response when you retrieve the object or query the object metadata.   |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | Example: **x-obs-meta-test: test metadata**                                                                                                                                                                                           |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | **Restrictions**:                                                                                                                                                                                                                     |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | Both metadata keys and their values must conform to US-ASCII standards.                                                                                                                                                               |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | **Value range**:                                                                                                                                                                                                                      |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | None                                                                                                                                                                                                                                  |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | **Default value**:                                                                                                                                                                                                                    |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | None                                                                                                                                                                                                                                  |
   +-------------------------------------+-----------------+--------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | x-obs-website-redirect-location     | String          | No                                                                       | **Explanation**:                                                                                                                                                                                                                      |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | If a bucket is configured with the static website hosting function, it will redirect requests for this object to another object in the same bucket or to an external URL. OBS stores the value of this header in the object metadata. |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | In the following example, the request header sets the redirection to an object (**anotherPage.html**) in the same bucket:                                                                                                             |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | x-obs-website-redirect-location:/anotherPage.html                                                                                                                                                                                     |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | In the following example, the request header sets the object redirection to an external URL:                                                                                                                                          |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | x-obs-website-redirect-location:http://www.example.com/                                                                                                                                                                               |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | **Restrictions**:                                                                                                                                                                                                                     |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | The value must start with a slash (/), **http://**, or **https://** and cannot exceed 2 KB.                                                                                                                                           |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | **Value range**:                                                                                                                                                                                                                      |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | None                                                                                                                                                                                                                                  |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | **Default value**:                                                                                                                                                                                                                    |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | None                                                                                                                                                                                                                                  |
   +-------------------------------------+-----------------+--------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | success-action-redirect             | String          | No                                                                       | **Explanation**:                                                                                                                                                                                                                      |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | The redirection address used when requests were successfully responded to.                                                                                                                                                            |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | -  If the value is valid and the request is successful, OBS returns status code 303. **Location** contains **success_action_redirect** as well as the bucket name, object name, and object ETag.                                      |
   |                                     |                 |                                                                          | -  If this parameter value is invalid, OBS ignores this parameter. In such case, the **Location** header is the object address, and OBS returns the response code based on whether the operation succeeds or fails.                   |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | **Restrictions**:                                                                                                                                                                                                                     |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | The value must be a valid URL, for example, **http://**\ *domainname* or **https://**\ *domainname*.                                                                                                                                  |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | **Value range**:                                                                                                                                                                                                                      |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | URL                                                                                                                                                                                                                                   |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | **Default value**:                                                                                                                                                                                                                    |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | None                                                                                                                                                                                                                                  |
   +-------------------------------------+-----------------+--------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | x-obs-expires                       | Integer         | No                                                                       | **Explanation**:                                                                                                                                                                                                                      |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | Specifies when an object expires. It is measured in days. Once the object expires, it is automatically deleted. (The validity calculates from the object's creation time.)                                                            |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | You can configure this field when uploading an object or modify this field by using the metadata modification API after the object is uploaded.                                                                                       |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | Example: **x-obs-expires:3**                                                                                                                                                                                                          |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | **Restrictions**:                                                                                                                                                                                                                     |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | The value must be greater than the number of days that have passed since the object was created. For example, if the object was uploaded 10 days ago, you must specify a value greater than 10.                                       |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | **Value range**:                                                                                                                                                                                                                      |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | The value is an integer greater than 0.                                                                                                                                                                                               |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | **Default value**:                                                                                                                                                                                                                    |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | None                                                                                                                                                                                                                                  |
   +-------------------------------------+-----------------+--------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | x-obs-tagging                       | String          | No                                                                       | **Explanation**:                                                                                                                                                                                                                      |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | Object's tag information in key-value pairs. Multiple tags can be added at the same time.                                                                                                                                             |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | Example: **x-obs-tagging:TagA=A&TagB&TagC**                                                                                                                                                                                           |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | **Restrictions**:                                                                                                                                                                                                                     |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | -  If a tag key or value contains special characters, equal signs (=), or full-width characters, it must be URL-encoded.                                                                                                              |
   |                                     |                 |                                                                          | -  If there is no equal sign (=) in a configuration, the tag value is considered left blank.                                                                                                                                          |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | **Value range**:                                                                                                                                                                                                                      |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | None                                                                                                                                                                                                                                  |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | **Default value**:                                                                                                                                                                                                                    |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | None                                                                                                                                                                                                                                  |
   +-------------------------------------+-----------------+--------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | x-obs-object-lock-mode              | String          | No, but required when **x-obs-object-lock-retain-until-date** is present | **Explanation**:                                                                                                                                                                                                                      |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | WORM mode applied to the object.                                                                                                                                                                                                      |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | Example: **x-obs-object-lock-mode:COMPLIANCE**                                                                                                                                                                                        |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | **Restrictions**:                                                                                                                                                                                                                     |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | -  Only COMPLIANCE (compliance mode) is supported.                                                                                                                                                                                    |
   |                                     |                 |                                                                          | -  This parameter must be used together with **x-obs-object-lock-retain-until-date**.                                                                                                                                                 |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | **Value range**:                                                                                                                                                                                                                      |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | COMPLIANCE                                                                                                                                                                                                                            |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | **Default value**:                                                                                                                                                                                                                    |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | None                                                                                                                                                                                                                                  |
   +-------------------------------------+-----------------+--------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | x-obs-object-lock-retain-until-date | String          | No, but required when **x-obs-object-lock-mode** is present.             | **Explanation**:                                                                                                                                                                                                                      |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | When the WORM policy of the object expires.                                                                                                                                                                                           |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | Example: **x-obs-object-lock-retain-until-date:2015-07-01T04:11:15Z**                                                                                                                                                                 |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | **Restrictions**:                                                                                                                                                                                                                     |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | -  The value must be a UTC time that complies with the ISO 8601 standard. Example: **2015-07-01T04:11:15Z**                                                                                                                           |
   |                                     |                 |                                                                          | -  This parameter must be used together with **x-obs-object-lock-mode**.                                                                                                                                                              |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | **Value range**:                                                                                                                                                                                                                      |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | The time must be later than the current time.                                                                                                                                                                                         |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | **Default value**:                                                                                                                                                                                                                    |
   |                                     |                 |                                                                          |                                                                                                                                                                                                                                       |
   |                                     |                 |                                                                          | None                                                                                                                                                                                                                                  |
   +-------------------------------------+-----------------+--------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

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

In addition to the common response headers, the headers listed in :ref:`Table 2 <obs_04_0080__table8930193215584>` might also be needed.

.. _obs_04_0080__table8930193215584:

.. table:: **Table 2** Additional response headers

   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------+
   | Header                | Type                  | Description                                                                                                |
   +=======================+=======================+============================================================================================================+
   | x-obs-version-id      | String                | **Explanation**:                                                                                           |
   |                       |                       |                                                                                                            |
   |                       |                       | Version ID of the object. If versioning is enabled for the bucket, the object version ID will be returned. |
   |                       |                       |                                                                                                            |
   |                       |                       | **Restrictions**:                                                                                          |
   |                       |                       |                                                                                                            |
   |                       |                       | None                                                                                                       |
   |                       |                       |                                                                                                            |
   |                       |                       | **Value range**:                                                                                           |
   |                       |                       |                                                                                                            |
   |                       |                       | None                                                                                                       |
   |                       |                       |                                                                                                            |
   |                       |                       | **Default value**:                                                                                         |
   |                       |                       |                                                                                                            |
   |                       |                       | None                                                                                                       |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------+
   | x-obs-storage-class   | String                | **Explanation**:                                                                                           |
   |                       |                       |                                                                                                            |
   |                       |                       | Storage class of an object                                                                                 |
   |                       |                       |                                                                                                            |
   |                       |                       | **Restrictions**:                                                                                          |
   |                       |                       |                                                                                                            |
   |                       |                       | This header is returned when the storage class of an object is not Standard.                               |
   |                       |                       |                                                                                                            |
   |                       |                       | **Value range**:                                                                                           |
   |                       |                       |                                                                                                            |
   |                       |                       | -  WARM                                                                                                    |
   |                       |                       | -  COLD                                                                                                    |
   |                       |                       |                                                                                                            |
   |                       |                       | **Default value**:                                                                                         |
   |                       |                       |                                                                                                            |
   |                       |                       | None                                                                                                       |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------+

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

Sample Request: Uploading an Object (with a Storage Class Specified)
--------------------------------------------------------------------

.. code-block:: text

   PUT /object01 HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: WED, 01 Jul 2015 04:15:07 GMT
   x-obs-storage-class: WARM
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:uFVJhp/dJqj/CJIVLrSZ0gpw3ng=
   Content-Length: 10240
   Expect: 100-continue

   [1024 Byte data content]

Sample Response: Uploading an Object (with a Storage Class Specified)
---------------------------------------------------------------------

::

   HTTP/1.1 200 OK
   Server: OBS
   x-obs-request-id: BB7800000164846A2112F98BF970AA7E
   ETag: "d41d8cd98f00b204e9800998ecf8427e"
   x-obs-id-2: a39E0UgAIAABAAAQAAEAABAAAQAAEAABCTPOUJu5XlNyU32fvKjM/92MQZK2gtoB
   Date: WED, 01 Jul 2015 04:15:07 GMT
   x-obs-storage-class: WARM
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
