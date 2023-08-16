:original_name: en-us_topic_0125560494.html

.. _en-us_topic_0125560494:

GET Bucket website
==================

You can use this operation to get the website configuration of a bucket.

Only users granted the **s3:GetBucketWebsite** permission can get the bucket website configuration. By default, only the bucket owner can get the bucket website configuration. The bucket owner can allow other users to get the bucket website configuration by granting them the permission.

Request Syntax
--------------

.. code-block::

    GET /?website HTTP/1.1
    User-Agent: agent
    Host: bucketname.obs.example.com
    Accept: */*
    Date: date
    Authoirization: authorization

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
   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <WebsiteConfiguration xmlns="http://obs.example.com/doc/2015-06-30/">
      <RedirectAllRequestsTo>
        <HostName>hostName</HostName>
      </RedirectAllRequestsTo>
    </WebsiteConfiguration>

Response Headers
----------------

This response uses common headers. For details about common response headers, see section :ref:`Common Response Headers <en-us_topic_0125560484>`.

Response Elements
-----------------

This response contains elements the same as those used by the **PUT Bucket website** request. For details, see section :ref:`PUT Bucket website <en-us_topic_0125560321>`.

Error Responses
---------------

This response contains common errors. For details, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`. In addition, this response contains one special error, as described in :ref:`Table 1 <en-us_topic_0125560494__table19964345>`.

.. _en-us_topic_0125560494__table19964345:

.. table:: **Table 1** Special error

   +----------------------------+----------------------------------------------------------+------------------+
   | Error Code                 | Description                                              | HTTP Status Code |
   +============================+==========================================================+==================+
   | NoSuchWebsiteConfiguration | Indicates that the website configuration does not exist. | 404 Not Found    |
   +----------------------------+----------------------------------------------------------+------------------+

Sample Request
--------------

.. code-block:: text

   GET /?website HTTP/1.1
    User-Agent: curl/7.29.0
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Sat, 04 Jan 2014 06:47:16 +0000
    Authorization: AWS C6630CD15B645CB8A3BA:XrepYUF0mA/m1RPvpA0M18FdCfg=

Sample Response
---------------

.. code-block::

   HTTP/1.1 200 OK
    Server: OBS
    x-amz-request-id: DCD2FC9CAB78000001435C0176F28223
    x-amz-id-2: 8BSYBZcQKwR5nCgMsLY86TRLwhUZpLbQTxAKIAuMJqx3OURwOMhILeVNwTrEQWyc
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Content-Type: application/xml
    Date: Sat, 04 Jan 2014 06:47:16 GMT
    Content-Length: 230

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <WebsiteConfiguration xmlns="http://obs.example.com/doc/2015-06-30/">
    <RedirectAllRequestsTo>
    <HostName>www.example.com</HostName>
    </RedirectAllRequestsTo>
    </WebsiteConfiguration>
