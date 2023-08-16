:original_name: en-us_topic_0125560383.html

.. _en-us_topic_0125560383:

GET Bucket quota
================

Using this operation, an active bucket owner can obtain its quota.

A bucket quota is expressed in bytes. If the quota is set to **0**, the quota has no upper limit.

Request Syntax
--------------

.. code-block:: text

   GET /?quota HTTP/1.1
    User-Agent: agent
    Host: bucketname.obs.example.com
    Accept: */*
    Date: date
    Authorization: authorization

Request Parameters
------------------

This request involves no parameters.

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
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    x-amz-id-2: id
    Content-Type: type
    Date: date
    Content-Length: length

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <Quota xmlns="http://obs.example.com/doc/2015-06-30/">
    <StorageQuota>value</StorageQuota>
    </Quota>

Response Headers
----------------

This response uses common headers. For details about common response headers, see section :ref:`Common Response Headers <en-us_topic_0125560484>`.

Response Elements
-----------------

This response contains elements to provide details about a bucket quota. :ref:`Table 1 <en-us_topic_0125560383__table40100219>` describes the elements.

.. _en-us_topic_0125560383__table40100219:

.. table:: **Table 1** Response elements

   +-----------------------------------+-------------------------------------------------------------------------------------+
   | Element                           | Description                                                                         |
   +===================================+=====================================================================================+
   | Quota                             | Indicates bucket quota details. This element contains the **StorageQuota** element. |
   |                                   |                                                                                     |
   |                                   | Type: XML                                                                           |
   +-----------------------------------+-------------------------------------------------------------------------------------+
   | StorageQuota                      | Indicates the bucket quota value.                                                   |
   |                                   |                                                                                     |
   |                                   | Type: String                                                                        |
   +-----------------------------------+-------------------------------------------------------------------------------------+

Error Responses
---------------

No special error responses are returned. For details about error responses, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`.

Sample Request
--------------

.. code-block:: text

   GET /?quota HTTP/1.1
    User-Agent: Jakarta Commons-HttpClient/3.1
    Host: bucketname.obs.example.com
    Accept-Encoding: gzip,deflate
    Date: Thu, 22 Nov 2012 09:37:38 +0000
    Authorization: AWS 08350B985315591007AD:O4jTB/FzS3gXDouwRZgz1wiE2PE=

Sample Response
---------------

.. code-block::

   HTTP/1.1 200 OK
    Server: OBS
    x-amz-request-id: 90E2BA0F80EC0000013B277AD1970001
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    x-amz-id-2: ReSvzDszzWqXunSRGkNv+aIjXO56ekT48XVAOcyjIEU6zufqkoqJRO6z1VPLvDcm
    Content-Type: application/xml
    Date: Thu, 22 Nov 2012 09:37:38 GMT
    Content-Length: 148

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <Quota xmlns="http://obs.example.com/doc/2015-06-30/">
    <StorageQuota>8</StorageQuota>
    </Quota>
