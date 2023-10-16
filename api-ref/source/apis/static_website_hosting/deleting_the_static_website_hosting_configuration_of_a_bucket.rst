:original_name: obs_04_0073.html

.. _obs_04_0073:

Deleting the Static Website Hosting Configuration of a Bucket
=============================================================

Functions
---------

You can perform this operation to delete the website configuration of a bucket.

To perform this operation, you must have the **DeleteBucketWebsite** permission. By default, only the bucket owner can perform this operation. The bucket owner can grant the permission to other users by configuring the bucket policy or user policy.

Request Syntax
--------------

.. code-block:: text

   DELETE /?website HTTP/1.1
   Host: bucketname.obs.region.example.com
   Date: date
   Authorization: authorization

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
   Content-Type: type
   Content-Length: length

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

   DELETE /?website HTTP/1.1
   User-Agent: curl/7.29.0
   Host: bucketname.obs.region.example.com
   Accept: */*
   Date: WED, 01 Jul 2015 03:44:37 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:AZ1b0N5eLknxNOe/c0BISV1bEqc=

Sample Response
---------------

::

   HTTP/1.1 204 No Content
   Server: OBS
   x-obs-request-id: BF2600000164363786230E2001DC0807
   x-obs-id-2: 32AAAQAAEAABSAAgAAEAABAAAQAAEAABCSFUG4fEyDRgzUiEY2i71bJndBCy+wUZ
   Date: WED, 01 Jul 2015 03:44:37 GMT
