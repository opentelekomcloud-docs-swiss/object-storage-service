:original_name: en-us_topic_0125560459.html

.. _en-us_topic_0125560459:

DELETE Object
=============

You can use this operation to delete an object as long as you have **WRITE** permission for the object, you can delete the object. OBS returns a success response even if the object to be deleted does not exist.

Versioning
----------

If a bucket has versioning enabled, a deletion mark with a unique version ID is generated after an object in the bucket is deleted with no version ID specified.

If a bucket has versioning suspended, a deletion mark with version ID **null** is generated after an object in the bucket is deleted with no version ID specified. The object whose version is **null** (if such an object exists) is physically deleted.

You can specify **versionId** to delete an object of the specified version.

Request Syntax
--------------

.. code-block:: text

   DELETE /ObjectKey HTTP/1.1
    User-Agent: agent
    Host: bucketname.obs.example.com
    Accept: */*
    Date: date
    Authorization: authorization

Request parameters
------------------

:ref:`Table 1 <en-us_topic_0125560459__table57902635>` describes the request parameter.

.. important::

   For deleting an object, only parameters listed in :ref:`Table1 Request parameter <en-us_topic_0125560459__table57902635>` are supported. If the request contains parameters that cannot be identified by OBS, the server returns the 400 error code.

.. _en-us_topic_0125560459__table57902635:

.. table:: **Table 1** Request parameter

   +-----------------------+------------------------------------------------------+-----------------------+
   | Parameter             | Description                                          | Remarks               |
   +=======================+======================================================+=======================+
   | versionId             | Indicates the version ID of an object to be deleted. | Optional              |
   |                       |                                                      |                       |
   |                       | Type: String                                         |                       |
   +-----------------------+------------------------------------------------------+-----------------------+

Request Headers
---------------

This request uses common headers. For details about common request headers, see section :ref:`Common Request Headers <en-us_topic_0125560462>`.

Request Elements
----------------

This request involves no elements.

Response Syntax
---------------

.. code-block::

   HTTP/1.1 status_code
    Server: Server Name
    x-amz-request-id: request id
    x-amz-id-2: id
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Date: date

Response Headers
----------------

This response uses common headers. For details about common response headers, see section :ref:`Common Response Headers <en-us_topic_0125560484>`. In addition, this response also uses optional headers, as described in :ref:`Table 2 <en-us_topic_0125560459__table2749429>`.

.. _en-us_topic_0125560459__table2749429:

.. table:: **Table 2** Optional response headers

   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------+
   | Header                            | Description                                                                                                          |
   +===================================+======================================================================================================================+
   | x-amz-delete-marker               | Indicates whether an object is marked as deleted. If an object is not marked as deleted, the header is not returned. |
   |                                   |                                                                                                                      |
   |                                   | Type: Boolean                                                                                                        |
   |                                   |                                                                                                                      |
   |                                   | Valid values: true|false                                                                                             |
   |                                   |                                                                                                                      |
   |                                   | Default: false                                                                                                       |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------+
   | x-amz-version-id                  | Indicates the version ID of an object. If an object has no version ID, this header is not returned.                  |
   |                                   |                                                                                                                      |
   |                                   | Valid values: String                                                                                                 |
   |                                   |                                                                                                                      |
   |                                   | Default: None                                                                                                        |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------+

Response Elements
-----------------

This response involves no elements.

Error Responses
---------------

No special error responses are returned. For details about error responses, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`.

Sample Request
--------------

.. code-block:: text

   DELETE /test HTTP/1.1
    User-Agent: Jakarta Commons-HttpClient/3.1
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Sat, 03 Dec 2011 08:38:16 +0000
    Authorization: AWS BF6C09F302931425E9A7:wQ1Tp3rD7kaUCsYfPKxOIN7NoSA=

Sample Response
---------------

.. code-block::

   HTTP/1.1 204 No Content
    Server: OBS
    x-amz-request-id: 001B21A61C6C000001340312E226528D
    x-amz-id-2: MDAxQjIxQTYxQzZDMDAwMDAxMzQwMzEyRTIyNjUyOERBQUFBQUFBQWJiYmJiYmJi
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Content-Type: text/xml
    Date: Sat, 03 Dec 2011 08:38:18 GMT

Sample Request (Deleting an Object with Version ID Specified)
-------------------------------------------------------------

.. code-block:: text

   DELETE /object?versionId=AAABQ4-YOzfc0vycq3gAAAAUVURTRkha HTTP/1.1
    User-Agent: Jakarta Commons-HttpClient/3.1
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Tue, 14 Jan 2014 07:12:57 +0000
    Authorization: AWS C9590CEB8EC051BDEC9D:DxZpQ520WCv/yMgrUjBemFORuN0=

Sample Response (Deleting an Object with Version ID Specified)
--------------------------------------------------------------

.. code-block::

   HTTP/1.1 204 No Content
    Server: OBS
    x-amz-request-id: DCD2FC9CAB78000001438F98937AB673
    x-amz-id-2: UOWLHKBXWfKaBEToXGU3Om6pl0/Bid6OmhzgdJJDxN40twtrmuCHY0rEtDdSX7zp
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Content-Type: text/xml
    x-amz-version-id: AAABQ4-YOzfc0vycq3gAAAAUVURTRkha
    Date: Tue, 14 Jan 2014 07:12:57 GMT

Sample Request (Deleting an Object with a Deletion Mark from a Bucket with Versioning Enabled)
----------------------------------------------------------------------------------------------

.. code-block:: text

   DELETE /object HTTP/1.1
    User-Agent: Jakarta Commons-HttpClient/3.1
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Tue, 14 Jan 2014 06:16:51 +0000
    Authorization: AWS C9590CEB8EC051BDEC9D:VlzVUv3z3WOuSyu2l8NzVsOXY0U=

Sample Response (Deleting an Object with a Deletion Mark from a Bucket with Versioning Enabled)
-----------------------------------------------------------------------------------------------

.. code-block::

   HTTP/1.1 204 No Content
    Server: OBS
    x-amz-request-id: DCD2FC9CAB78000001438F65352A9AF5
    x-amz-id-2: CzNX/O9/H0oZRUwAk/sWgyfVDNJMMX+v9DAzArbD40AlLtZ/TCC7H73FNIo5K81I
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Content-Type: text/xml
    x-amz-delete-marker: true
    x-amz-version-id: AAABQ49lNT_c0vycq3gAAAAOVURTRkha
    Date: Tue, 14 Jan 2014 06:16:51 GMT
