:original_name: obs_04_0085.html

.. _obs_04_0085:

Deleting an Object
==================

Functions
---------

You can perform this operation to delete an object. If you try to delete an object that does not exist, OBS will return a success message.

Versioning
----------

When versioning is enabled for a bucket, a deletion marker with a unique version number is generated when an object is deleted without specifying the version. However, the object is not actually deleted. If versioning is suspended for a bucket and no version is specified when you delete an object, the object whose version number is **null** is deleted, and a deletion marker with version number **null** is generated.

To delete an object of a specified version, the **versionId** parameter can be used to specify the desired version.

WORM
----

OBS automatically enables versioning when you enable WORM for a bucket. If you delete an object without specifying a version ID, OBS does not really delete this object thanks to versioning, but inserts a delete marker with a unique version ID, which turns into the current version. If you specify a version ID when deleting an object protected by WORM, OBS prevents you from deleting this object and returns a 403 error. Delete markers are not protected by WORM.

Request Syntax
--------------

.. code-block:: text

   DELETE /ObjectName HTTP/1.1
   Host: bucketname.obs.region.example.com
   Date: date
   Authorization: authorization

Request Parameters
------------------

:ref:`Table 1 <obs_04_0085__d0e15727>` describes the request parameters.

.. important::

   For deleting an object, only parameters listed in :ref:`Table 1 <obs_04_0085__d0e15727>` are supported. If the request contains parameters that cannot be identified by OBS, the server returns the 400 error code.

.. _obs_04_0085__d0e15727:

.. table:: **Table 1** Request parameters

   +-----------------------+-----------------------+-----------------------+
   | Parameter             | Description           | Mandatory             |
   +=======================+=======================+=======================+
   | versionId             | Object version ID     | No                    |
   |                       |                       |                       |
   |                       | Type: string          |                       |
   +-----------------------+-----------------------+-----------------------+

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

Response Headers
----------------

The response to the request uses common headers. For details, see :ref:`Table 1 <obs_04_0013__d0e686>`.

If versioning is enabled for the bucket, the headers listed in :ref:`Table 2 <obs_04_0085__table862048515455>` may also be used.

.. _obs_04_0085__table862048515455:

.. table:: **Table 2** Additional response headers

   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------+
   | Header                            | Description                                                                                                                |
   +===================================+============================================================================================================================+
   | x-obs-delete-marker               | Indicates whether an object is deleted. If the object is not marked as deleted, the response does not contain this header. |
   |                                   |                                                                                                                            |
   |                                   | Type: boolean                                                                                                              |
   |                                   |                                                                                                                            |
   |                                   | Value options: **true**, **false**                                                                                         |
   |                                   |                                                                                                                            |
   |                                   | The default value is **false**.                                                                                            |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------+
   | x-obs-version-id                  | Object version ID. If the object has no version number specified, the response does not contain this header.               |
   |                                   |                                                                                                                            |
   |                                   | Valid value: character string                                                                                              |
   |                                   |                                                                                                                            |
   |                                   | Default value: none                                                                                                        |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------+

Response Elements
-----------------

This response contains no elements.

Error Responses
---------------

No special error responses are returned. For details about error responses, see :ref:`Table 2 <obs_04_0115__d0e843>`.

Sample Request
--------------

.. code-block:: text

   DELETE /object2 HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: WED, 01 Jul 2015 04:19:21 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:MfK9JCnSFHCrJmjv7iRkRrrce2s=

Sample Response
---------------

::

   HTTP/1.1 204 No Content
   Server: OBS
   x-obs-request-id: 8DF400000163D3F51DEA05AC9CA066F1
   x-obs-id-2: 32AAAUgAIAABAAAQAAEAABAAAQAAEAABCSgkM4Dij80gAeFY8pAZIwx72QhDeBZ5
   Date: WED, 01 Jul 2015 04:19:21 GMT
