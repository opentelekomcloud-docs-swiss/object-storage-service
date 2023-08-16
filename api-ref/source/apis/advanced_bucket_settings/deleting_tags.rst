:original_name: obs_04_0051.html

.. _obs_04_0051:

Deleting Tags
=============

Functions
---------

This operation deletes the tags of a bucket.

To perform this operation, you must have the **PutBucketTagging** permission. By default, only the bucket owner can delete the tags of a bucket. The bucket owner can allow other users to perform this operation by setting a bucket policy or granting them the permission.

Request Syntax
--------------

.. code-block:: text

   DELETE /?tagging HTTP/1.1
   Host: bucketname.obs.region.example.com
   Date: date
   Authorization: authorization string

Request Parameters
------------------

This request contains no parameter.

Request Headers
---------------

This request uses common headers. For details, see :ref:`Table 3 <obs_04_0007__table25197309>`.

Request Elements
----------------

This request involves no elements.

Response Syntax
---------------

::

   HTTP/1.1 status_code
   x-obs-request-id: request id
   x-obs-id-2: id
   Content-Length: length
   Date: date

Response Headers
----------------

The response to the request uses common headers. For details, see :ref:`Table 1 <obs_04_0013__d0e686>`.

Response Elements
-----------------

This response involves no elements.

Error Responses
---------------

No special error responses are returned. For details about error responses, see :ref:`Table 2 <obs_04_0115__d0e843>`.

Sample Request
--------------

.. code-block:: text

   DELETE /?tagging HTTP/1.1
   User-Agent: curl/7.19.7
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: Wed, 27 Jun 2018 13:46:58 GMT
   Authorization: authorization string

Sample Response
---------------

::

   HTTP/1.1 204 No Content
   x-obs-request-id: 0002B7532E0000015BEB2C212E53A17L
   x-obs-id-2: CqT+86nnOkB+Cv9KZoVgZ28pSgMF+uGQBUC68flvkQeq6CxoCz65wWFMNBpXvea4
   Content-Length: 0
   Date: Wed, 27 Jun 2018 13:46:58 GMT
