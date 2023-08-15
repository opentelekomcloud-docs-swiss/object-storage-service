:original_name: obs_04_0024.html

.. _obs_04_0024:

Obtaining Bucket Location
=========================

Functions
---------

This operation obtains the location of a bucket. To use this operation, you must have the permission to read the bucket.

Request Syntax
--------------

.. code-block:: text

   GET /?location HTTP/1.1
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
   <Location xmlns="http://obs.region.example.com/doc/2015-06-30/">region</Location>

Response Headers
----------------

The response to the request uses common headers. For details, see :ref:`Table 1 <obs_04_0013__d0e686>`.

Response Elements
-----------------

This response contains elements of information about a bucket's region. :ref:`Table 1 <obs_04_0024__table63691781>` describes the elements.

.. _obs_04_0024__table63691781:

.. table:: **Table 1** Response elements

   +-----------------------------------+------------------------------------------------+
   | Element                           | Description                                    |
   +===================================+================================================+
   | Location                          | Indicates the region where the bucket resides. |
   |                                   |                                                |
   |                                   | Type: string                                   |
   +-----------------------------------+------------------------------------------------+

Error Responses
---------------

No special error responses are involved. For details about error responses, see :ref:`Table 2 <obs_04_0115__d0e843>`.

Sample Request
--------------

.. code-block:: text

   GET /?location HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: WED, 01 Jul 2015 02:30:25 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:1DrmbCV+lhz3zV7uywlj7lrh0MY=

Sample Response
---------------

::

   HTTP/1.1 200 OK
   Server: OBS
   x-obs-request-id: BF260000016435D9F27CB2758E9B41A5
   x-obs-id-2: 32AAAQAAEAABAAAQAAEAABAAAQAAEAABCSKWoJmaMyRXqofHgapbETDyI2LM9rUw
   Content-Type: application/xml
   Date: WED, 01 Jul 2015 02:30:25 GMT
   Content-Length: 128

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <Location xmlns="http://obs.region.example.com/doc/2015-06-30/">region</Location>
