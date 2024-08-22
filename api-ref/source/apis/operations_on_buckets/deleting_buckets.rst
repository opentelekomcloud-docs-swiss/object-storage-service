:original_name: obs_04_0025.html

.. _obs_04_0025:

Deleting Buckets
================

Functions
---------

This operation deletes specified buckets. This operation can be performed only by the bucket owner and users who have been authorized (via a policy) with the permission to delete the bucket. The bucket to be deleted must be an empty bucket. If a bucket has an object or a multipart task, the bucket is not empty. You can list objects and multipart upload tasks in a bucket to check whether the bucket is empty.

Note:

If the server returns a **5XX** error or times out when a bucket is being deleted, the system needs to synchronize the bucket information. During this period, the bucket information may be inaccurate. Therefore, wait a while and then check whether the bucket is successfully deleted. If the bucket can still be queried, send the deletion request again.

Request Syntax
--------------

.. code-block:: text

   DELETE / HTTP/1.1
   Host: bucketname.obs.region.example.com
   Date: date
   Authorization: authorization

Request Parameters
------------------

This request contains no parameters.

Request Headers
---------------

This request uses common request headers. For details, see :ref:`Table 3 <obs_04_0007__table25197309>`.

Request Elements
----------------

This request involves no elements.

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

   DELETE / HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: WED, 01 Jul 2015 02:31:25 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:jZiAT8Vx4azWEvPRMWi0X5BpJMA=

Sample Response
---------------

::

   HTTP/1.1 204 No Content
   Server: OBS
   x-obs-request-id: BF260000016435DE6D67C35F9B969C47
   x-obs-id-2: 32AAAQAAEAABKAAQAAEAABAAAQAAEAABCTukraCnXLsb7lEw4ZKjzDWWhzXdgme3
   Date: WED, 01 Jul 2015 02:31:25 GMT
