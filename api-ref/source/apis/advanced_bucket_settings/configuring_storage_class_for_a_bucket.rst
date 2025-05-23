:original_name: obs_04_0044.html

.. _obs_04_0044:

Configuring Storage Class for a Bucket
======================================

Functions
---------

This operation sets or updates the default storage class of a bucket.

To perform this operation, you must have the **PutBucketStoragePolicy** permission. By default, only the bucket owner can perform this operation. The bucket owner can grant the permission to other users by configuring the bucket policy or user policy.

If you do not specify a storage class when uploading or copying an object, or initiating a multipart upload, the object inherits the bucket's storage class.

The default storage class of a bucket is Standard.

Request Syntax
--------------

.. code-block:: text

   PUT /?storageClass HTTP/1.1
   Host: bucketname.obs.region.example.com
   Date: date
   Content-Type: type
   Content-Length: length
   Authorization: authorization

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <StorageClass xmlns="http://obs.example.com/doc/2015-06-30/">STANDARD</StorageClass>

Request Parameters
------------------

This request contains no parameters.

Request Headers
---------------

This request uses common headers. For details, see :ref:`Table 3 <obs_04_0007__table25197309>`.

Request Elements
----------------

This request needs an additional element to specify the default bucket storage class. For details, see :ref:`Table 1 <obs_04_0044__table63485364>`.

.. _obs_04_0044__table63485364:

.. table:: **Table 1** Additional request elements

   +-----------------------+------------------------------------------------------------------------------------------------------+-----------------------+
   | Element               | Description                                                                                          | Mandatory             |
   +=======================+======================================================================================================+=======================+
   | StorageClass          | Specifies the default storage class for a bucket.                                                    | Yes                   |
   |                       |                                                                                                      |                       |
   |                       | Type: string                                                                                         |                       |
   |                       |                                                                                                      |                       |
   |                       | Value options: **STANDARD**, **WARM**, **COLD**                                                      |                       |
   |                       |                                                                                                      |                       |
   |                       | The storage class options are as follows: **STANDARD** (Standard), **WARM** (Warm), **COLD** (Cold). |                       |
   +-----------------------+------------------------------------------------------------------------------------------------------+-----------------------+

Response Syntax
---------------

::

   HTTP/1.1 status_code
   Date: date

Response Headers
----------------

The response to the request uses common headers. For details, see :ref:`Table 1 <obs_04_0013__d0e686>`.

Response Elements
-----------------

This response contains no elements.

Error Responses
---------------

No special error responses are returned. For details about error responses, see :ref:`Table 2 <obs_04_0115__d0e843>`.

Sample Request
--------------

.. code-block:: text

   PUT /?storageClass HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: WED, 01 Jul 2015 03:18:19 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:Tf6XbndPx/yNgfAVQ6KIXr7tMj4=
   Content-Length: 87

   <StorageClass xmlns="http://obs.example.com/doc/2015-06-30/">STANDARD</StorageClass>

Sample Response
---------------

::

   HTTP/1.1 200 OK
   Server: OBS
   x-obs-request-id: BF2600000164368E704B571F328A8797
   x-obs-id-2: 32AAAQAAEAABSAAgAAEAABAAAQAAEAABCSIsw3tPtUn6damTI5acQmQAcEfmTwl3
   Date: WED, 01 Jul 2015 03:18:19 GMT
   Content-Length: 0
