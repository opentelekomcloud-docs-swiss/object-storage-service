:original_name: obs_04_0053.html

.. _obs_04_0053:

Querying Bucket Storage Quota
=============================

Functions
---------

A bucket owner can query the bucket storage quota, but a bucket owner who is frozen due to arrears cannot. The bucket storage quota is measured by byte. **0** indicates that no upper limit is set.

Request Syntax
--------------

.. code-block:: text

   GET /?quota HTTP/1.1
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
   Content-Type: application/xml
   Content-Length: length

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <Quota xmlns="http://obs.region.example.com/doc/2015-06-30/">
       <StorageQuota>quota</StorageQuota>
   </Quota>

Response Headers
----------------

The response to the request uses common headers. For details, see :ref:`Table 1 <obs_04_0013__d0e686>`.

Response Elements
-----------------

This response contains elements of information about the bucket quota. :ref:`Table 1 <obs_04_0053__d0e8370>` describes the elements.

.. _obs_04_0053__d0e8370:

.. table:: **Table 1** Response elements

   +-----------------------------------+-----------------------------------------------------------------------+
   | Element                           | Description                                                           |
   +===================================+=======================================================================+
   | Quota                             | Bucket storage quota. This element contains the StorageQuota element. |
   |                                   |                                                                       |
   |                                   | Type: XML                                                             |
   +-----------------------------------+-----------------------------------------------------------------------+
   | StorageQuota                      | Bucket storage quota quantity. The unit is byte.                      |
   |                                   |                                                                       |
   |                                   | Type: string                                                          |
   +-----------------------------------+-----------------------------------------------------------------------+

Error Responses
---------------

No special error responses are returned. For details about error responses, see :ref:`Table 2 <obs_04_0115__d0e843>`.

Sample Request
--------------

.. code-block:: text

   GET /?quota HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: WED, 01 Jul 2015 03:27:45 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:8m4bW1gFCNeXQlfu45uO2gpo7l8=

Sample Response
---------------

::

   HTTP/1.1 200 OK
   Server: OBS
   x-obs-request-id: BF260000016436B55D8DED9AE26C4D18
   x-obs-id-2: 32AAAQAAEAABAAAQAAEAABAAAQAAEAABCSs2Q5vz5AfpAJ/CMNgCfo2hmDowp7M9
   Content-Type: application/xml
   Date: WED, 01 Jul 2015 03:27:45 GMT
   Content-Length: 150

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <Quota xmlns="http://obs.example.com/doc/2015-06-30/">
     <StorageQuota>0</StorageQuota>
   </Quota>
