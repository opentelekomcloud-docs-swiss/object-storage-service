:original_name: obs_04_0045.html

.. _obs_04_0045:

Obtaining Bucket Storage Class Information
==========================================

Functions
---------

This operation obtains the default storage class of a bucket.

To perform this operation, you must have the **GetBucketStoragePolicy** permission. By default, only the bucket owner can perform this operation. The bucket owner can grant the permission to other users by configuring the bucket policy or user policy.

Request Syntax
--------------

.. code-block:: text

   GET /?storageClass HTTP/1.1
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

This request contains no elements.

Response Syntax
---------------

::

   HTTP/1.1 status_code
   Date: date
   Content-Type: type
   Content-Length: length

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>

   <StorageClass xmlns="http://obs.example.com/doc/2015-06-30/">STANDARD</StorageClass>

Response Headers
----------------

The response to the request uses common headers. For details, see :ref:`Table 1 <obs_04_0013__d0e686>`.

Response Elements
-----------------

This response contains elements to provide details about the storage class information of a bucket. :ref:`Table 1 <obs_04_0045__d0e9764>` describes the elements.

.. _obs_04_0045__d0e9764:

.. table:: **Table 1** Response elements

   +-----------------------------------+---------------------------------------------------------------------------------------------------------+
   | Element                           | Description                                                                                             |
   +===================================+=========================================================================================================+
   | StorageClass                      | Default storage class of the bucket.                                                                    |
   |                                   |                                                                                                         |
   |                                   | Type: string. For details about the enumeration types, see :ref:`Table 1 <obs_04_0044__table63485364>`. |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------+

Error Responses
---------------

No special error responses are returned. For details about error responses, see :ref:`Table 2 <obs_04_0115__d0e843>`.

Sample Request
--------------

.. code-block:: text

   GET /?storageClass HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: WED, 01 Jul 2015 03:20:28 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:0zVTSdKG6OFCIH2dKvmsVGYCQyw=

Sample Response
---------------

::

   HTTP/1.1 200 OK
   Server: OBS
   x-obs-request-id: BF260000016436BE45820FDF3A65B42C
   x-obs-id-2: 32AAAQAAEAABAAAQAAEAABAAAQAAEAABCSCju1CZy3ZfRVW5hiNd024lRFdUoqWy
   Content-Type: application/xml
   Date: WED, 01 Jul 2015 03:20:28 GMT
   Content-Length: 142

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>

   <StorageClass xmlns="http://obs.example.com/doc/2015-06-30/">STANDARD</StorageClass>
