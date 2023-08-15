:original_name: obs_04_0038.html

.. _obs_04_0038:

Obtaining Bucket Versioning Status
==================================

Functions
---------

This operation allows a bucket owner to get the versioning status of the bucket.

If versioning is not configured for a bucket, no versioning status information will be returned following this operation.

Request Syntax
--------------

.. code-block:: text

   GET /?versioning HTTP/1.1
   Host: bucketname.obs.region.example.com
   Date: date
   Authorization: authorization

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
   Date: date
   Content-Type: type
   Content-Length: length

   <VersioningConfiguration xmlns="http://obs.region.example.com/doc/2015-06-30/">
       <Status>status</Status>
   </VersioningConfiguration>

Response Headers
----------------

The response to the request uses common headers. For details, see :ref:`Table 1 <obs_04_0013__d0e686>`.

Response Elements
-----------------

This response contains elements to specify the bucket versioning status. :ref:`Table 1 <obs_04_0038__table29764434204455>` describes the elements.

.. _obs_04_0038__table29764434204455:

.. table:: **Table 1** Response elements

   +-----------------------------------+-------------------------------------------+
   | Element                           | Description                               |
   +===================================+===========================================+
   | VersioningConfiguration           | Element of versioning status information. |
   |                                   |                                           |
   |                                   | Type: element                             |
   +-----------------------------------+-------------------------------------------+
   | Status                            | Versioning status of the bucket.          |
   |                                   |                                           |
   |                                   | Type: enumeration                         |
   |                                   |                                           |
   |                                   | Value options: Enabled, Suspended         |
   +-----------------------------------+-------------------------------------------+

Error Responses
---------------

No special error responses are involved. For details about error responses, see :ref:`Table 2 <obs_04_0115__d0e843>`.

Sample Request
--------------

.. code-block:: text

   GET /?versioning HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: WED, 01 Jul 2015 03:15:20 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:4N5qQIoluLO9xMY0m+8lIn/UWXM=

Sample Response
---------------

::

   HTTP/1.1 200 OK
   Server: OBS
   x-obs-request-id: BF260000016436BBA4930622B4FC9F17
   x-obs-id-2: 32AAAQAAEAABAAAQAAEAABAAAQAAEAABCSQIrNJ5/Ag6EPN8DAwWlPWgBc/xfBnx
   Content-Type: application/xml
   Date: WED, 01 Jul 2015 03:15:20 GMT
   Content-Length: 180

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <VersioningConfiguration xmlns="http://obs.example.com/doc/2015-06-30/">
     <Status>Enabled</Status>
   </VersioningConfiguration>
