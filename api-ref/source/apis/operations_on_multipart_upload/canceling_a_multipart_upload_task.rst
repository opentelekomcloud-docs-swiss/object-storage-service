:original_name: obs_04_0103.html

.. _obs_04_0103:

Canceling a Multipart Upload Task
=================================

Functions
---------

You can perform this operation to abort a multipart upload. You cannot upload or list parts after operations to merge parts or abort a multipart upload are performed.

Request Syntax
--------------

.. code-block:: text

   DELETE /ObjectName?uploadId=uplaodID HTTP/1.1
   Host: bucketname.obs.region.example.com
   Date: date
   Authorization: auth

Request Parameters
------------------

This request uses message parameters to specify the multipart upload task number of the segment task. :ref:`Table 1 <obs_04_0103__table46411854>` describes the parameters.

.. _obs_04_0103__table46411854:

.. table:: **Table 1** Request parameters

   +-----------------------+-------------------------------+-----------------------+
   | Parameter             | Description                   | Mandatory             |
   +=======================+===============================+=======================+
   | uploadId              | Indicates a multipart upload. | Yes                   |
   |                       |                               |                       |
   |                       | Type: string                  |                       |
   +-----------------------+-------------------------------+-----------------------+

Request Headers
---------------

This request uses common headers. For details, see :ref:`Table 3 <obs_04_0007__table25197309>`.

Request Elements
----------------

This request involves no elements.

Response Syntax
---------------

.. code-block::

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

#. If the AK or signature is invalid, OBS returns **403 Forbidden** and the error code is **AccessDenied**.
#. If the requested bucket is not found, OBS returns **404 Not Found** and the error code is **NoSuchBucket**.
#. If you are neither the initiator of a multipart upload nor the bucket owner, OBS returns **403 Forbidden**.
#. If the operation is successful, OBS returns **204 No Content** to the user.

Other errors are included in :ref:`Table 2 <obs_04_0115__d0e843>`.

Sample Request
--------------

.. code-block:: text

   DELETE /object02?uploadId=00000163D46218698DF407362295674C HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: WED, 01 Jul 2015 05:28:27 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:QmM2d1DBXZ/b8drqtEv1QJHPbM0=

Sample Response
---------------

::

   HTTP/1.1 204 No Content
   Server: OBS
   x-obs-request-id: 8DF400000163D463E02A07EC2295674C
   x-obs-id-2: 32AAAQAAEAABAAAQAAEAABAAAQAAEAABCTp5YDlzn0UgqG3laRfkHLGyz7RpR9ON
   Date: WED, 01 Jul 2015 05:28:27 GMT
