:original_name: obs_04_0054.html

.. _obs_04_0054:

Obtaining Storage Information of a Bucket
=========================================

Functions
---------

This operation queries the number of bucket objects and the space occupied by the objects. The size of the object space is a positive integer, measured by bytes.

.. note::

   OBS bucket storage statistics are calculated in the background and are not updated in real time. Therefore, it isn't recommended to use storage data for real-time verification or monitoring purposes, as slight delays or inconsistencies may occur.

Request Syntax
--------------

.. code-block:: text

   GET /?storageinfo HTTP/1.1
   Host: bucketname.obs.region.example.com
   Date: date
   Authorization: authorization

Request Parameters
------------------

This request contains no parameters.

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
   <GetBucketStorageInfoResult xmlns="http://obs.region.example.com/doc/2015-06-30/">
   <Size>size</Size>
   <ObjectNumber>number</ObjectNumber>
   </GetBucketStorageInfoResult>

Response Headers
----------------

The response to the request uses common headers. For details, see :ref:`Table 1 <obs_04_0013__d0e686>`.

Response Elements
-----------------

This response contains elements of information about the used storage capacity of a bucket. :ref:`Table 1 <obs_04_0054__table4057783695910>` describes the elements.

.. _obs_04_0054__table4057783695910:

.. table:: **Table 1** Response elements

   +-----------------------------------+----------------------------------------------------------------------------------------------------------------+
   | Element                           | Description                                                                                                    |
   +===================================+================================================================================================================+
   | GetBucketStorageInfoResult        | Request result that saves bucket storage information, including the stored data size and the number of objects |
   |                                   |                                                                                                                |
   |                                   | Type: XML                                                                                                      |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------+
   | Size                              | Size of stored data                                                                                            |
   |                                   |                                                                                                                |
   |                                   | Type: long                                                                                                     |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------+
   | ObjectNumber                      | Number of objects returned                                                                                     |
   |                                   |                                                                                                                |
   |                                   | Type: integer                                                                                                  |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------+

Error Responses
---------------

No special error responses are returned. For details about error responses, see :ref:`Table 2 <obs_04_0115__d0e843>`.

Sample Request
--------------

.. code-block:: text

   GET /?storageinfo HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: WED, 01 Jul 2015 03:31:18 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:bLcdeJGYWw/eEEjMhPZx2MK5R9U=

Sample Response
---------------

::

   HTTP/1.1 200 OK
   Server: OBS
   x-obs-request-id: BF260000016435DD2958BFDCDB86B55E
   x-obs-id-2: 32AAAQAAEAABAAAQAAEAABAAAQAAEAABCSitZctaPYVnat49fVMd1O+OWIP1yrg3
   Content-Type: application/xml
   WED, 01 Jul 2015 03:31:18 GMT
   Content-Length: 206

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <GetBucketStorageInfoResult xmlns="http://obs.example.com/doc/2015-06-30/">
     <Size>25490</Size>
     <ObjectNumber>24</ObjectNumber>
   </GetBucketStorageInfoResult>
