:original_name: obs_04_0036.html

.. _obs_04_0036:

Deleting Lifecycle Rules
========================

Functions
---------

This operation deletes the lifecycle configuration of a bucket. After the lifecycle configuration of a bucket is deleted, OBS will not automatically delete objects in that bucket.

To perform this operation, you must have the **PutLifecycleConfiguration** permission. By default, only the bucket owner can perform this operation. The bucket owner can grant the permission to other users by configuring the bucket policy or user policy.

Request Syntax
--------------

.. code-block:: text

   DELETE /?lifecycle HTTP/1.1
   Host: bucketname.obs.region.example.com
   Date: date
   Authorization: Authorization

Request Parameters
------------------

This request contains no message parameters.

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
   Date: date
   Content-Type: text/xml
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

   DELETE /?lifecycle HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: WED, 01 Jul 2015 03:12:22 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:5DGAS7SBbMC1YTC4tNXY57Zl2Fo=

Sample Response
---------------

::

   HTTP/1.1 204 No Content
   Server: OBS
   x-obs-request-id: BF260000016436C2550A1EEA97614A98
   x-obs-id-2: 32AAAQAAEAABSAAgAAEAABAAAQAAEAABCSB7A0KZEBOCutgcfZvaGVthTGOJSuyk
   Date: WED, 01 Jul 2015 03:12:22 GMT
