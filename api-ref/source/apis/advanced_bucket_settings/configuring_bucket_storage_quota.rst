:original_name: obs_04_0052.html

.. _obs_04_0052:

Configuring Bucket Storage Quota
================================

Functions
---------

The bucket storage quota must be a positive integer in the unit of byte. The maximum storage quota is 2\ :sup:`63` - 1 bytes. The default bucket storage quota is **0**, indicating that the bucket storage quota is not limited.

.. note::

   #. For a bucket that has a specified storage quota, you can change the quota to **0** to cancel the quota limitation.
   #. The bucket storage quota verification depends on how much space is used in the bucket. However, the used storage space is measured at the background. Therefore, bucket storage quotas may not take effect immediately, and delay is expected. The used storage space in a bucket may exceed the bucket storage quota, or the used storage space may remain unchanged after data is deleted from the bucket.
   #. For details about the API for querying used storage space, see :ref:`Obtaining Storage Information of a Bucket <obs_04_0054>`.
   #. If the used storage space in a bucket reaches the upper limit of the bucket storage quota, object upload will fail and the HTTP status code 403 Forbidden will be returned, indicating **InsufficientStorageSpace**. In this case, you can increase the quota, cancel the quota limitation (by changing the quota to **0**), or delete unwanted objects from the bucket.

Request Syntax
--------------

.. code-block:: text

   PUT /?quota HTTP/1.1
   Host: bucketname.obs.region.example.com
   Date: date
   Content-Length: length
   Authorization: authorization

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <Quota xmlns="http://obs.region.example.com/doc/2015-06-30/">
       <StorageQuota>value</StorageQuota>
   </Quota>

Request Parameters
------------------

This request contains no parameters.

Request Headers
---------------

This request uses common headers. For details, see :ref:`Table 3 <obs_04_0007__table25197309>`.

Request Elements
----------------

This request uses an additional element to specify a bucket quota. :ref:`Table 1 <obs_04_0052__table32716508105325>` describes the element.

.. _obs_04_0052__table32716508105325:

.. table:: **Table 1** Additional request elements

   +-----------------------+-------------------------------------------------------+-----------------------+
   | Element               | Description                                           | Mandatory             |
   +=======================+=======================================================+=======================+
   | StorageQuota          | Specifies the bucket storage quota. The unit is byte. | Yes                   |
   |                       |                                                       |                       |
   |                       | Type: integer                                         |                       |
   +-----------------------+-------------------------------------------------------+-----------------------+

Response Syntax
---------------

::

   HTTP/1.1 status_code
   Date: date
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

   PUT /?quota HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: WED, 01 Jul 2015 03:24:37 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:k/rbwnYaqYf0Ae6F0M3OJQ0dmI8=
   Content-Length: 106

   <Quota xmlns="http://obs.region.example.com/doc/2015-06-30/">
     <StorageQuota>10240000</StorageQuota>
   </Quota>

Sample Response
---------------

::

   HTTP/1.1 100 Continue
   HTTP/1.1 200 OK
   Server: OBS
   x-obs-request-id: BF260000016435E09A2BCA388688AA08
   x-obs-id-2: 32AAAQAAEAABSAAgAAEAABAAAQAAEAABCSHbmBecv7ohDSvqaRObpxzgzJ9+l8xT
   Date: WED, 01 Jul 2015 03:24:37 GMT
   Content-Length: 0
