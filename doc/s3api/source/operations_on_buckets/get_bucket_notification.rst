:original_name: en-us_topic_0125560442.html

.. _en-us_topic_0125560442:

GET Bucket Notification
=======================

Obtains the notification configuration of a bucket.

The **s3:GetBucketNotification** permission is required to perform this operation. By default, the permission is granted to the bucket owner only. However, it can be granted to other users by configuring the bucket policy.

Request Syntax
--------------

.. code-block:: text

   GET /?notification HTTP/1.1
   User-Agent: agent
   Host: bucketname.obs.example.com
   Accept: */*
   Date: date
   Authorization: authorization

Request Parameters
------------------

This request contains no parameter.

Request Headers
---------------

This request uses common headers. For details, see section :ref:`Common Request Headers <en-us_topic_0125560462>`.

Request Elements
----------------

This request contains no element.

Response Syntax
---------------

.. code-block::

   HTTP/1.1 status_code
   x-amz-request-id: id
   x-amz-id-2: id
   x-reserved: reserved info
   Content-Type: type
   Date: date
   Content-Length: lenth

   <?xml version="1.0" encoding="UTF-8"?>
   <NotificationConfiguration xmlns="http://obs.example.com/doc/2015-06-30/">
    <TopicConfiguration>
     <Id>topic_001</Id>
     <Topic>urn:smn:example:35667523564:topic001</Topic>
     <Event>s3:ObjectCreated:*</Event>
     ....
    </TopicConfiguration>
   </NotificationConfiguration>

Response Headers
----------------

This response uses common headers. For details, see section :ref:`Common Response Headers <en-us_topic_0125560484>`.

Response Elements
-----------------

The following table describes the elements contained in this response.

.. table:: **Table 1** Response elements

   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------+
   | Element                           | Description                                                                                                               |
   +===================================+===========================================================================================================================+
   | NotificationConfiguration         | Container for configuring the event notification function of a bucket. If this element is null, the function is disabled. |
   |                                   |                                                                                                                           |
   |                                   | Type: Container                                                                                                           |
   |                                   |                                                                                                                           |
   |                                   | Ancestor: None                                                                                                            |
   |                                   |                                                                                                                           |
   |                                   | Children: one TopicConfiguration or TopicConfigurations                                                                   |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------+
   | TopicConfiguration                | Container for configuring the event notification topic                                                                    |
   |                                   |                                                                                                                           |
   |                                   | Type: Container                                                                                                           |
   |                                   |                                                                                                                           |
   |                                   | Ancestor: NotificationConfiguration                                                                                       |
   |                                   |                                                                                                                           |
   |                                   | Children: Id, Filter, Topic, Event or Events                                                                              |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------+
   | Topic                             | URN of the event notification topic. After detecting a specific event, OBS sends a message to the topic.                  |
   |                                   |                                                                                                                           |
   |                                   | Type: String                                                                                                              |
   |                                   |                                                                                                                           |
   |                                   | Ancestor: TopicConfiguration                                                                                              |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------+
   | Id                                | Unique ID of each event notification. If the user does not specify an ID, the system assigns an ID automatically.         |
   |                                   |                                                                                                                           |
   |                                   | Type: String                                                                                                              |
   |                                   |                                                                                                                           |
   |                                   | Ancestor: TopicConfiguration                                                                                              |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------+
   | Filter                            | Container of S3Key used to store rules of filtering object names                                                          |
   |                                   |                                                                                                                           |
   |                                   | Type: Container                                                                                                           |
   |                                   |                                                                                                                           |
   |                                   | Ancestor: TopicConfiguration                                                                                              |
   |                                   |                                                                                                                           |
   |                                   | Children: S3Key                                                                                                           |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------+
   | S3Key                             | Container of S3Key used to store rules of filtering object names                                                          |
   |                                   |                                                                                                                           |
   |                                   | Type: Container                                                                                                           |
   |                                   |                                                                                                                           |
   |                                   | Ancestor: TopicConfiguration                                                                                              |
   |                                   |                                                                                                                           |
   |                                   | Children: Name,Value                                                                                                      |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------+
   | FilterRule                        | Container that defines key-value pairs of filtering rules                                                                 |
   |                                   |                                                                                                                           |
   |                                   | Type: Container                                                                                                           |
   |                                   |                                                                                                                           |
   |                                   | Ancestor: S3Key                                                                                                           |
   |                                   |                                                                                                                           |
   |                                   | Children: Name, Value                                                                                                     |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------+
   | Name                              | Specifies the prefix or suffix of object names for filtering The value contains a maximum of 1024 characters.             |
   |                                   |                                                                                                                           |
   |                                   | Type: String                                                                                                              |
   |                                   |                                                                                                                           |
   |                                   | Ancestor: FilterRule                                                                                                      |
   |                                   |                                                                                                                           |
   |                                   | Legal value: prefix or suffix                                                                                             |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------+
   | Value                             | Specifies keywords of object names so that objects can be filtered based on the prefixes or suffixes.                     |
   |                                   |                                                                                                                           |
   |                                   | Type: String                                                                                                              |
   |                                   |                                                                                                                           |
   |                                   | Ancestor: FilterRule                                                                                                      |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------+
   | Event                             | Type of events that need to be notified                                                                                   |
   |                                   |                                                                                                                           |
   |                                   | .. note::                                                                                                                 |
   |                                   |                                                                                                                           |
   |                                   |    Multiple event types can be added in one TopicConfiguration configuration item.                                        |
   |                                   |                                                                                                                           |
   |                                   | Type: String                                                                                                              |
   |                                   |                                                                                                                           |
   |                                   | Ancestor: TopicConfiguration                                                                                              |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------+

Error Responses
---------------

No special error responses are returned. For details about error responses, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`.

Sample Request
--------------

.. code-block:: text

   GET /?notification HTTP/1.1
   User-Agent: curl/7.19.0 (x86_64-suse-linux-gnu) libcurl/7.19.0 OpenSSL/0.9.8{ zlib/1.2.3 libidn/1.10
   Host: bucketname.obs.example.com
   Accept: */*
   Date: Tue, 28 Apr 2015 09:11:35 +0000
   Authorization: AWS D13E0C94E722DD69423C:FJt2xJ1gEnozLSdpRNTJUoy6344=

Sample Response
---------------

.. code-block::

   HTTP/1.1 200 OK
   x-amz-id-2: YgIPIfBiKa2bj0KMgUAdQkf3ShJTOOpXUueF6QKo
   x-amz-request-id: 236A8905248E5A02
   Date: Wed, 15 Oct 2014 16:59:04 GMT
   Server: AmazonS3

   <?xml version="1.0" encoding="UTF-8"?>
   <NotificationConfiguration xmlns="http://obs.huawie.com/doc/2015-06-30/">
    <TopicConfiguration>
     <Id>id001</Id>
     <Topic>urn:smn:example:1236598854:topic1</Topic>
     <Event>s3:ObjectCreated:*</Event>
    </TopicConfiguration>
   </NotificationConfiguration>
