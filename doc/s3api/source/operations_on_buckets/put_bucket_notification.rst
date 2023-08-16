:original_name: en-us_topic_0125560248.html

.. _en-us_topic_0125560248:

PUT Bucket Notification
=======================

When the notification function is enabled, you will be notified of all the specified operations on your bucket.

By default, the notification function of your bucket is not enabled. Namely, the NotificationConfiguration element is null. If you want to disable the function, set the NotificationConfiguration element to null.

After receiving the notification request, OBS verifies whether the specified Simple Message Notification (SMN) topic exists and whether the topic is authorized to OBS. If the topic exists and is authorized to OBS, OBS sends a test notification to the topic.

The **s3:PutBucketNotification** permission is required to configure the notification function. By default, the permission is granted to the bucket owner only. However, it can be granted to other users by configuring the bucket policy.

.. note::

   For details about how to authorize topics to OBS, see the *SMN User Guide*

Request Syntax
--------------

.. code-block:: text

   PUT /?notification HTTP/1.1
   User-Agent: agent
   Host: bucketname.obs.example.com
   Accept: */*
   Date: date
   Authorization: authorization
   Content-Length: length
   Expect: expect

   <NotificationConfiguration>
    <TopicConfiguration>
     <Id>ConfigurationId</Id>
     <Filter>
      <S3Key>
       <FilterRule>
        <Name>prefix</Name>
        <Value>prefix-value</Value>
       </FilterRule>
       <FilterRule>
        <Name>suffix</Name>
        <Value>suffix-value</Value>
       </FilterRule>
      </S3Key>
     </Filter>
     <Topic>TopicARN</Topic>
     <Event>event-type</Event>
     <Event>event-type</Event>
     ...
    </TopicConfiguration>
   </NotificationConfiguration>

Request Parameters
------------------

This request contains no parameter.

Request Headers
---------------

This request uses common headers. For details, see section :ref:`Common Request Headers <en-us_topic_0125560462>`.

Request Elements
----------------

This request contains elements to specify the notification configuration for the bucket in XML format. The following table lists the request elements.

.. table:: **Table 1** Request elements of notification function configuration

   +---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------+
   | Element                   | Description                                                                                                                                            | Mandatory or Not                            |
   +===========================+========================================================================================================================================================+=============================================+
   | NotificationConfiguration | Container for configuring the event notification function of a bucket. If this element is null, the function is disabled.                              | Yes                                         |
   |                           |                                                                                                                                                        |                                             |
   |                           | Type: Container                                                                                                                                        |                                             |
   |                           |                                                                                                                                                        |                                             |
   |                           | Ancestor: None                                                                                                                                         |                                             |
   |                           |                                                                                                                                                        |                                             |
   |                           | Children: zero TopicConfiguration, one TopicConfiguration, or TopicConfigurations                                                                      |                                             |
   +---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------+
   | TopicConfiguration        | Container for configuring the event notification topic                                                                                                 | No                                          |
   |                           |                                                                                                                                                        |                                             |
   |                           | Type: Container                                                                                                                                        |                                             |
   |                           |                                                                                                                                                        |                                             |
   |                           | Ancestor: NotificationConfiguration                                                                                                                    |                                             |
   |                           |                                                                                                                                                        |                                             |
   |                           | Children: Id, Filter, Topic, Event or Events                                                                                                           |                                             |
   +---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------+
   | Topic                     | URN of the event notification topic. After detecting a specific event, OBS sends a message to the topic.                                               | Yes if ancestor TopicConfiguration is added |
   |                           |                                                                                                                                                        |                                             |
   |                           | Type: String                                                                                                                                           |                                             |
   |                           |                                                                                                                                                        |                                             |
   |                           | Ancestor: TopicConfiguration                                                                                                                           |                                             |
   +---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------+
   | Id                        | Unique ID of each event notification. If the user does not specify an ID, the system assigns an ID automatically.                                      | No                                          |
   |                           |                                                                                                                                                        |                                             |
   |                           | Type: String                                                                                                                                           |                                             |
   |                           |                                                                                                                                                        |                                             |
   |                           | Ancestor: TopicConfiguration                                                                                                                           |                                             |
   +---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------+
   | Filter                    | Container of S3Key used to store rules of filtering object names                                                                                       | No                                          |
   |                           |                                                                                                                                                        |                                             |
   |                           | Type: Container                                                                                                                                        |                                             |
   |                           |                                                                                                                                                        |                                             |
   |                           | Ancestor: TopicConfiguration                                                                                                                           |                                             |
   |                           |                                                                                                                                                        |                                             |
   |                           | Children: S3Key                                                                                                                                        |                                             |
   +---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------+
   | S3Key                     | Container that defines filtering rules. The rules filter objects based on the prefixes and suffixes of object names.                                   | No                                          |
   |                           |                                                                                                                                                        |                                             |
   |                           | Type: Container                                                                                                                                        |                                             |
   |                           |                                                                                                                                                        |                                             |
   |                           | Ancestor: Filter                                                                                                                                       |                                             |
   |                           |                                                                                                                                                        |                                             |
   |                           | Children: One FilterRule or FilterRules                                                                                                                |                                             |
   +---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------+
   | FilterRule                | Container that defines key-value pairs of filtering rules                                                                                              | No                                          |
   |                           |                                                                                                                                                        |                                             |
   |                           | Type: Container                                                                                                                                        |                                             |
   |                           |                                                                                                                                                        |                                             |
   |                           | Ancestor: S3Key                                                                                                                                        |                                             |
   |                           |                                                                                                                                                        |                                             |
   |                           | Children: Name, Value                                                                                                                                  |                                             |
   +---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------+
   | Name                      | Specifies the prefix or suffix of object names for filtering.                                                                                          | No                                          |
   |                           |                                                                                                                                                        |                                             |
   |                           | Type: String                                                                                                                                           |                                             |
   |                           |                                                                                                                                                        |                                             |
   |                           | Ancestor: FilterRule                                                                                                                                   |                                             |
   |                           |                                                                                                                                                        |                                             |
   |                           | Legal value: prefix or suffix                                                                                                                          |                                             |
   +---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------+
   | Value                     | Specifies keywords of object names so that objects can be filtered based on the prefixes or suffixes. The value contains a maximum of 1024 characters. | No                                          |
   |                           |                                                                                                                                                        |                                             |
   |                           | Type: String                                                                                                                                           |                                             |
   |                           |                                                                                                                                                        |                                             |
   |                           | Ancestor: FilterRule                                                                                                                                   |                                             |
   +---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------+
   | Event                     | Type of events that need to be notified                                                                                                                | Yes if ancestor TopicConfiguration is added |
   |                           |                                                                                                                                                        |                                             |
   |                           | .. note::                                                                                                                                              |                                             |
   |                           |                                                                                                                                                        |                                             |
   |                           |    Multiple event types can be added in one TopicConfiguration configuration item.                                                                     |                                             |
   |                           |                                                                                                                                                        |                                             |
   |                           | Type: String                                                                                                                                           |                                             |
   |                           |                                                                                                                                                        |                                             |
   |                           | Ancestor: TopicConfiguration                                                                                                                           |                                             |
   +---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------+

Response Syntax
---------------

.. code-block::

   HTTP/1.1 status_code
   x-amz-request-id: request id
   x-amz-id-2: id
   x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
   Date: date
   Content-Length: length

Response Headers
----------------

This response uses common headers. For details, see section :ref:`Common Response Headers <en-us_topic_0125560484>`.

Response Elements
-----------------

This response involves no elements.

Error Responses
---------------

When the user invokes the interface, the system checks whether the NotificationConfiguration element and the configuration are valid. The following table lists common errors and possible causes.

.. table:: **Table 2** Error codes and possible causes

   +-----------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | Error Code            | Possible Cause                                                                                     | HTTP Status Code      |
   +=======================+====================================================================================================+=======================+
   | InvalidArgument       | -  Unsupported events were specified.                                                              | 400 Bad Request       |
   |                       | -  The specified URN does not exist or is incorrect.                                               |                       |
   |                       | -  The specified region in the URN is different as the region where the bucket resides.            |                       |
   |                       | -  The specified filtering rules overlap.                                                          |                       |
   +-----------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | AccessDenied          | The operator is not the bucket owner and not granted with the s3:PutBucketNotification permission. | 403 Forbidden         |
   +-----------------------+----------------------------------------------------------------------------------------------------+-----------------------+

Sample Request
--------------

.. code-block:: text

   PUT /?notification HTTP/1.1
   User-Agent: curl/7.19.0 (x86_64-suse-linux-gnu) libcurl/7.19.0
   OpenSSL/0.9.8{ zlib/1.2.3 libidn/1.10
   Host: bucketname.obs.example.com
   Pragma: no-cache
   Accept: */*Date: Tue, 28 Apr 2015 08:56:07 +0000
   Authorization:AWS D13E0C94E722DD69423C:QhHpU6Amg/2r6wIYdU3RXIx7Tlc=
   Content-Length: 468 [request body]
   Expect: 100-continue

   <NotificationConfiguration>
    <TopicConfiguration>
     <Id>Id001</Id>
     <Topic>urn:smn:example:35667523564:topic001</Topic>
     <Event>s3:ObjectCreated:*</Event>
     <Filter>
      <S3Key>
       <FilterRule>
        <Name>prefix</Name>
        <Value>smn/</Value>
       </FilterRule>
       <FilterRule>
        <Name>suffix</Name>
        <Value>.jpg</Value>
       </FilterRule>
      </S3Key>
     </Filter>
    </TopicConfiguration>
   </NotificationConfiguration>

Sample Response
---------------

.. code-block::

   HTTP/1.1 200 OK
   x-amz-request-id: C2D2F581B3C5AF6C6698322AB56836F6
   x-amz-id-2: lDGZAj4h+A33eYauDCTsPvFSHzBXEtZon6Eg1idIZl18/2/odotyqJUJ/lTh80uA
   x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
   Content-Type: text/xml
   Date: Tue, 28 Apr 2015 08:56:07 GMT
   Content-Length: 0
