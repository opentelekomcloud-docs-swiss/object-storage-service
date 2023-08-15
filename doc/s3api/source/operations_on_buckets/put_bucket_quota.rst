:original_name: en-us_topic_0125560329.html

.. _en-us_topic_0125560329:

PUT Bucket quota
================

Using this operation, an active bucket owner can modify the bucket quota.

A bucket quota must be a non-negative integer expressed in bytes. The maximum allowed quota is (2^63 - 1) bytes. If a bucket quota is set to **0**, the quota has no upper limit.

Request Syntax
--------------

.. code-block:: text

   PUT /?quota HTTP/1.1
    User-Agent: agent
    Host: bucketname.obs.example.com
    Accept: */*
    Date: date
    Authorization: authorization
    Content-Length:length

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <Quota xmlns="http://obs.example.com/doc/2015-06-30/">
    <StorageQuota>value</StorageQuota>
    </Quota>

Request Parameters
------------------

This request involves no parameters.

Request Headers
---------------

This request uses common headers. For details about common request headers, see section :ref:`Common Request Headers <en-us_topic_0125560462>`.

Request Elements
----------------

This request contains one element to specify the bucket quota, as described in :ref:`Table 1 <en-us_topic_0125560329__table63485364>`.

.. _en-us_topic_0125560329__table63485364:

.. table:: **Table 1** Request element

   +-----------------------+---------------------------+-----------------------+
   | Element               | Description               | Remarks               |
   +=======================+===========================+=======================+
   | StorageQuota          | Indicates a bucket quota. | Mandatory             |
   |                       |                           |                       |
   |                       | Type: Integer             |                       |
   +-----------------------+---------------------------+-----------------------+

Response Syntax
---------------

.. code-block::

   HTTP/1.1 status_code
    Server: Server Name
    x-amz-request-id: request id
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    x-amz-id-2: id
    Date: date
    Content-Length: length

Response Headers
----------------

This response uses common headers. For details about common response headers, see section :ref:`Common Response Headers <en-us_topic_0125560484>`.

Response Elements
-----------------

This response involves no elements.

Error Responses
---------------

No special error responses are returned. For details about error responses, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`.

Sample Request
--------------

.. code-block:: text

   PUT /?quota HTTP/1.1
    User-Agent: Jakarta Commons-HttpClient/3.1
    Host: bucketname.obs.example.com
    Accept-Encoding: gzip,deflate
    Date: Thu, 22 Nov 2012 09:37:17 +0000
    Authorization: AWS 08350B985315591007AD:O4jTB/FzS3gXDouwRZgz1wiE2PE=
    Content-Length:149

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <Quota xmlns="http://obs.example.com/doc/2015-06-30/">
    <StorageQuota>8</StorageQuota>
    </Quota>

Sample Response
---------------

.. code-block::

   HTTP/1.1 200 OK
    Server: OBS
    x-amz-request-id: 90E2BA0F80EC0000013B277A80860000
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    x-amz-id-2: dSLkVtVbslB8z967VtfTQmFbD3q4IzeNUBL+tlpGLMGT1FgXnlady4r+oRI/bx2y
    Date: Thu, 22 Nov 2012 09:37:17 GMT
    Content-Length: 0
