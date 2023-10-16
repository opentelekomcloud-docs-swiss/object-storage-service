:original_name: obs_04_0029.html

.. _obs_04_0029:

Deleting a Bucket Policy
========================

Functions
---------

This operation uses the policy sub-resources to delete the policy of a specified bucket.

To perform this operation, the user must be the bucket owner or the bucket owner's IAM user that has permissions required for deleting bucket policies.

The 204 error code "No Content" is returned regardless of whether a requested bucket policy exists or not.

Request Syntax
--------------

.. code-block:: text

   DELETE /?policy HTTP/1.1
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
   Content-Type: text/xml
   Content-Length: length

Response Headers
----------------

The response to the request uses common headers. For details, see :ref:`Table 1 <obs_04_0013__d0e686>`.

Response Elements
-----------------

This response contains no elements.

Error Responses
---------------

No special error responses are returned. For details, see :ref:`Table 2 <obs_04_0115__d0e843>`.

Sample Request
--------------

.. code-block:: text

   DELETE /?policy HTTP/1.1
   Host: examplebucket.obs.region.example.com
   Date: WED, 01 Jul 2015 02:36:06 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:jZiAT8Vx4azWEvPRMWi0X5BpJMA=

Sample Response
---------------

::

   HTTP/1.1 204 No Content
   x-obs-request-id: 9006000001643AAAF70BF6152D71BE8A
   x-obs-id-2: 32AAAQAAEAABSAAgAAEAABAAAQAAEAABCSB4oWmNX3gVGGLr1cRPWjOhffEbq1XV
   Date: WED, 01 Jul 2015 02:36:06 GMT
   Server: OBS
