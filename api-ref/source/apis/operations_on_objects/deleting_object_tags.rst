:original_name: obs_04_0165.html

.. _obs_04_0165:

Deleting Object Tags
====================

Functions
---------

This operation deletes tags from an object.

If you do not specify a version ID in a request, make sure that you have the **DeleteObjectTagging** permission. If you do specify a version ID in a request, make sure that you have the **DeleteObjectTagging** and **DeleteObjectVersionTagging** permissions. By default, only the object owner can perform this operation. The object owner can grant this permission to others by using a bucket or user policy.

OBS deletes tags from the current object version by default. You can use the **versionId** parameter to delete tags from any other version. If the version you are deleting tags from is a delete marker, OBS returns **404 Not Found**.

.. note::

   Tags are not supported for files in parallel file systems.

Request Syntax
--------------

.. code-block:: text

   DELETE /objectname?tagging&versionId=versionid  HTTP/1.1
   Host: bucketname.obs.region.example.com
   Date: date
   Authorization: authorization string

Request Parameters
------------------

:ref:`Table 1 <obs_04_0165__table416285709507>` describes the parameters in the request.

.. _obs_04_0165__table416285709507:

.. table:: **Table 1** Request parameters

   +-----------------------+---------------------------------------------------------------------------------------------+-----------------------+
   | Parameter             | Description                                                                                 | Mandatory (Yes/No)    |
   +=======================+=============================================================================================+=======================+
   | tagging               | Indicates an object tag request.                                                            | Yes                   |
   |                       |                                                                                             |                       |
   |                       | Type: string                                                                                |                       |
   +-----------------------+---------------------------------------------------------------------------------------------+-----------------------+
   | versionId             | ID of the tagged object version. Its corresponding response header is **x-obs-version-id**. | No                    |
   |                       |                                                                                             |                       |
   |                       | Type: string                                                                                |                       |
   +-----------------------+---------------------------------------------------------------------------------------------+-----------------------+

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
   x-obs-request-id: request id
   x-obs-id-2: id
   x-obs-version-id: version id
   Content-Length: length
   Date: date

Response Headers
----------------

This request uses common headers. For details, see :ref:`Table 3 <obs_04_0007__table25197309>`.

Response Elements
-----------------

This response contains no elements.

Error Responses
---------------

No special error responses are returned. For details, see :ref:`Table 2 <obs_04_0115__d0e843>`. If the object has no tags or the tag deletion is successful, OBS returns a 204 error.

Sample Request
--------------

.. code-block:: text

   DELETE /objectname?tagging&versionId=G001018455096CE600005306000000DD HTTP/1.1
   User-Agent: curl/7.19.7
   Host: bucketname.obs.region.example.com
   Accept: */*
   Date: Wed, 27 Jun 2018 13:46:58 GMT
   Authorization: authorization string

Sample Response
---------------

::

   HTTP/1.1 204 No Content
   x-obs-request-id: 0002B7532E0000015BEB2C212E53A17L
   x-obs-id-2: CqT+86nnOkB+Cv9KZoVgZ28pSgMF+uGQBUC68flvkQeq6CxoCz65wWFMNBpXvea4
   x-obs-version-id: G001018455096CE600005306000000DD
   Content-Length: 0
   Date: Wed, 27 Jun 2018 13:46:58 GMT
