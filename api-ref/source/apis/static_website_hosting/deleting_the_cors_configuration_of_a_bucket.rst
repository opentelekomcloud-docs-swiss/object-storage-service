:original_name: obs_04_0076.html

.. _obs_04_0076:

Deleting the CORS Configuration of a Bucket
===========================================

Functions
---------

This operation is used to delete the CORS configuration of a bucket. After the CORS configuration is deleted, the bucket and objects in it cannot be accessed by requests from other websites.

To perform this operation, you must have the **PutBucketCORS** permission.

Request Syntax
--------------

.. code-block:: text

   DELETE /?cors HTTP/1.1
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
   Content-Type:  application/xml
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

   DELETE /?cors HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: WED, 01 Jul 2015 03:56:41 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:mKUs/uIPb8BP0ZhvMd4wEy+EbiI=

Sample Response
---------------

::

   HTTP/1.1 204 No Content
   Server: OBS
   x-obs-request-id: BF26000001643639F290185BB27F793A
   x-obs-id-2: 32AAAQAAEAABSAAgAAEAABAAAQAAEAABCSLWMRFJfckapW+ktT/+1AnAz7XlNU0b
   Date: WED, 01 Jul 2015 03:56:41 GMT
