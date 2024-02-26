:original_name: en-us_topic_0125560444.html

.. _en-us_topic_0125560444:

PUT Bucket versioning
=====================

You can use this operation to enable or suspend versioning for a bucket.

Versioning can be used to restore an object that is incorrectly overwritten or deleted. You can use versioning to save, query, and restore objects of different versions. Versioning allows you to easily recover data lost due to misoperations or program faults. Versioning can also be used for retaining and archiving data.

By default, versioning is disabled for a bucket.

Once WORM is enabled for a bucket, OBS automatically enables versioning for the bucket and the versioning cannot be suspended for that bucket.

After the versioning state is set to **Enabled**:

-  OBS creates a unique version ID for each uploaded object. Namesake objects are not overwritten and are distinguished by their own version IDs.
-  Objects can be downloaded by version ID. By default, the latest object is downloaded if the version ID is not specified.
-  Objects can be deleted by version ID. If an object is deleted with no version ID specified, the object is only attached with a deletion mark and a unique version ID but is not physically deleted.
-  The latest objects in a bucket are returned by default after a **GET Object** request. You can also send a request to obtain a bucket's objects with all version IDs.
-  Except deletion marks and object metadata, storage space occupied by objects with all version IDs is billed.

After the versioning state is set to **Suspended**:

-  Existing objects with version IDs are not affected.
-  OBS creates version ID **null** to an uploaded object and the object will be overwritten after a namesake one is uploaded.
-  Objects can be downloaded by version ID. By default, the latest object is downloaded if the version ID is not specified.
-  Objects can be deleted by version ID. If an object is deleted with no version ID specified, the object is only attached with a deletion mark and version ID **null**. Objects with version ID **null** are physically deleted.
-  Except deletion marks and object metadata, storage space occupied by objects with all version IDs is billed.

Only the bucket owner can set the bucket versioning state.

Request Syntax
--------------

.. code-block:: text

   PUT /?versioning HTTP/1.1
    User-Agent: agent
    Host: bucketname.obs.example.com
    Accept: */*
    Date: date
    Authorization: authorization
    Content-Length: length
    Expect: expect

   <VersioningConfiguration>
    <Status>status</Status>
   </VersioningConfiguration>

Request Parameters
------------------

This request involves no parameters.

Request Headers
---------------

This request uses common headers. For details about common request headers, see section :ref:`Common Request Headers <en-us_topic_0125560462>`.

Request Elements
----------------

This request contains elements to configure the bucket versioning in the XML format. :ref:`Table 1 <en-us_topic_0125560444__table62924030>` describes the elements.

.. _en-us_topic_0125560444__table62924030:

.. table:: **Table 1** Elements for configuring bucket versioning

   +-------------------------+-----------------------------------------------------------------+-----------------------+
   | Element                 | Description                                                     | Remarks               |
   +=========================+=================================================================+=======================+
   | VersioningConfiguration | Indicates the container for the versioning state configuration. | Mandatory             |
   |                         |                                                                 |                       |
   |                         | Ancestor: None                                                  |                       |
   +-------------------------+-----------------------------------------------------------------+-----------------------+
   | Status                  | Specifies the versioning state of the bucket.                   | Mandatory             |
   |                         |                                                                 |                       |
   |                         | Type: Enumeration                                               |                       |
   |                         |                                                                 |                       |
   |                         | Ancestor: VersioningConfiguration                               |                       |
   |                         |                                                                 |                       |
   |                         | Valid Values: Enabled, Suspended                                |                       |
   +-------------------------+-----------------------------------------------------------------+-----------------------+

Response Syntax
---------------

.. code-block::

   HTTP/1.1 status_code
    Server: Server Name
    x-amz-request-id: request id
    x-amz-id-2: id
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Date: date
    Content-Length: length

Response Headers
----------------

This response uses common headers. For details about common response headers, see section :ref:`Common Response Headers <en-us_topic_0125560484>`.

Response elements
-----------------

This response involves no elements.

Error Responses
---------------

No special error responses are returned. For details about error responses, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`.

Sample Request
--------------

.. code-block:: text

   PUT /?versioning HTTP/1.1
   User-Agent: curl/7.29.0
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Mon, 13 Jan 2014 07:33:22 +0000
    Authorization: AWS C5780CDE717D50F4CDAA:MxAazqX4BdUfCXpbNd1VpZqyDD4=
    Content-Length: 80
    Expect: 100-continue

   <VersioningConfiguration>
    <Status>Enabled</Status>
   </VersioningConfiguration>

Sample Response
---------------

.. code-block::

   HTTP/1.1 200 OK
    Server: OBS
    x-amz-request-id: DCD2FC9CAB78000001438A84E693000F
    x-amz-id-2: iRQ+xOfSLXxasHqbPqqtDcXRKHXzrz9cNrrW4wjNum2DGHAgr359+tU6QCcwiT0y
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Date: Mon, 13 Jan 2014 07:33:22 GMT
    Content-Length: 0
