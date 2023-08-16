:original_name: en-us_topic_0125560345.html

.. _en-us_topic_0125560345:

GET Bucket versioning
=====================

The owner of a bucket can use this operation to get the versioning state of the bucket\ :sub:`.`

If versioning is not configured for a bucket, no versioning state information will be returned after this operation. For details, see **Sample Response (Bucket Versioning Not Configured)**.

Request Syntax
--------------

.. code-block:: text

   GET /?versioning HTTP/1.1
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
    x-amz-id-2: id
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Content-Type: type
    Date: date
    Content-Length: length

    <VersioningConfiguration xmlns="http://obs.example.com/doc/2015-06-30/">
    <Status>status</Status>
    </VersioningConfiguration>

Response Headers
----------------

This response uses common headers. For details about common response headers, see section :ref:`Common Response Headers <en-us_topic_0125560484>`.

Response elements
-----------------

This response contains elements to specify the bucket versioning state. :ref:`Table 1 <en-us_topic_0125560345__table57299616>` describes the elements.

.. _en-us_topic_0125560345__table57299616:

.. table:: **Table 1** Response elements

   +-------------------------+-----------------------------------------------------------+-----------------------+
   | Element                 | Description                                               | Remarks               |
   +=========================+===========================================================+=======================+
   | VersioningConfiguration | Indicates the container for versioning state information. | Mandatory             |
   |                         |                                                           |                       |
   |                         | Type: Container                                           |                       |
   +-------------------------+-----------------------------------------------------------+-----------------------+
   | Status                  | Specifies the versioning state of the bucket.             | Optional              |
   |                         |                                                           |                       |
   |                         | Type: Enumeration                                         |                       |
   |                         |                                                           |                       |
   |                         | Valid Values: Enabled, Suspended                          |                       |
   +-------------------------+-----------------------------------------------------------+-----------------------+

Error Responses
---------------

No special error responses are returned. For details about error responses, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`.

Sample Request
--------------

.. code-block:: text

   GET /?versioning HTTP/1.1
   User-Agent: curl/7.29.0
   Host: bucketname.obs.example.com
   Accept: */*
   Date: Mon, 13 Jan 2014 07:41:08 +0000
   Authorization: AWS C5780CDE717D50F4CDAA:0FuFgUd3e9dqi3OeXPj1DiQMJgk=

Sample Response (Bucket Versioning Enabled)
-------------------------------------------

.. code-block::

   HTTP/1.1 200 OK
    Server: OBS
    x-amz-request-id: DCD2FC9CAB78000001438A8C029703EB
    x-amz-id-2: TazfhHdpZ7V0YzmLQynVfaQ2+9zaWlTiNokK3wk8+HZPW9lWWBdsz35BXWZiQ1lk
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Content-Type: application/xml
    Date: Mon, 13 Jan 2014 09:41:08 GMT
    Content-Length: 178

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <VersioningConfiguration xmlns="http://obs.example.com/doc/2015-06-30/">
    <Status>Enabled</Status>
    </VersioningConfiguration>

Sample Response (Bucket Versioning Suspended)
---------------------------------------------

.. code-block::

   HTTP/1.1 200 OK
    Server: OBS
    x-amz-request-id: DCD2FC9CAB7800000143954C3AE7C0A0
    x-amz-id-2: zmHdfVr7HvmASeSRQ70pbCkpuiV2shwt2V3pBGzAzue65i8HdixOtLi4ud5ZemN0
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Content-Type: application/xml
    Date: Wed, 13 Jan 2014 09:47:17 GMT
    Content-Length: 180

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <VersioningConfiguration xmlns="http://obs.example.com/doc/2015-06-30/">
    <Status>Suspended</Status>
    </VersioningConfiguration>

Sample Response (Bucket Versioning Not Configured)
--------------------------------------------------

.. code-block::

   HTTP/1.1 200 OK
    Server: OBS
    x-amz-request-id: DCD2FC9CAB780000014395468DB0BDB4
    x-amz-id-2: iDh4134qyYwtV7mlUr7vhe33DSDiDs/AuGOiU8ggUaz+B1wrNVUO6grsQDDsWf7J
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Content-Type: application/xml
    Date: Wed, 13 Jan 2014 09:40:00 GMT
    Content-Length: 129

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <VersioningConfiguration xmlns="http://obs.example.com/doc/2015-06-30/">
