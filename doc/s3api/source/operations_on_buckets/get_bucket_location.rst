:original_name: en-us_topic_0125560404.html

.. _en-us_topic_0125560404:

GET Bucket location
===================

Only the bucket owner or a user that is granted with the **s3:GetBucketLocation** permission in the bucket policy can obtain the bucket location information.

Request Syntax
--------------

.. code-block:: text

   GET /?location HTTP/1.1
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
    <CreateBucketConfiguration xmlns="http://obs.example.com/doc/2015-06-30/">
    <LocationConstraint>Location</LocationConstraint>
    </CreateBucketConfiguration>

Response Headers
----------------

This response uses common headers. For details about common response headers, see section :ref:`Common Response Headers <en-us_topic_0125560484>`.

Response Elements
-----------------

This response contains an element to describe the bucket Region. :ref:`Table 1 <en-us_topic_0125560404__table25305148>` describes this element.

.. _en-us_topic_0125560404__table25305148:

.. table:: **Table 1** Response element

   +-----------------------------------+------------------------------------------------+
   | Element                           | Description                                    |
   +===================================+================================================+
   | LocationConstraint                | Indicates information about a bucket's Region. |
   |                                   |                                                |
   |                                   | Type: String                                   |
   +-----------------------------------+------------------------------------------------+

Error Responses
---------------

No special error responses are returned. For details about error responses, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`.

Sample Request
--------------

.. code-block:: text

   GET /?location HTTP/1.1
    User-Agent: Jakarta Commons-HttpClient/3.1
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Sun, 26 Sep 2010 09:16:00 GMT
    Authorization: AWS 04RZT432N80TGDF2Y2G2:JUtd9kkJFjbKbkP9f6T/tAxozYY=

Sample Response
---------------

.. code-block::

   HTTP/1.1 200 OK
    Server: OBS
    x-amz-request-id: 367CB63A2F283044981285492719060
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    x-amz-id-2: MzY3Q0I2M0EyRjI4MzA0NDk4MTI4NTQ5MjcxOTA2MEFBQUFBQUFBYmJiYmJiYmJD
    Content-Type: application/xml
    Date: Sun, 26 Sep 2010 09:18:36 GMT
    Content-Length: 560

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <CreateBucketConfiguration xmlns="http://obs.example.com/doc/2015-06-30/">
    <LocationConstraint>example</LocationConstraint>
    </CreateBucketConfiguration>
