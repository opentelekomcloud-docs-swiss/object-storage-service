:original_name: obs_04_0039.html

.. _obs_04_0039:

Configuring Event Notification for a Bucket
===========================================

Functions
---------

This operation notifies users of their operations on buckets, allowing users know events happened on buckets in a timely manner.

By default, the notification function of a bucket is not enabled, and the **NotificationConfiguration** element is **null**. If you want to disable the function, set the **NotificationConfiguration** element to **null**.

::

   <NotificationConfiguration>
   </NotificationConfiguration>

After receiving a request for configuring event notification, OBS verifies whether the specified SMN topic exists and whether the topic is authorized to OBS. If the topic exists and is authorized to OBS, OBS sends a test notification to the topic subscriber.

To perform this operation, you must have the **PutBucketNotification** permission. By default, the permission is granted to the bucket owner only. However, it can be granted to other users by configuring the bucket policy.

Request Syntax
--------------

.. code-block:: text

   PUT /?notification HTTP/1.1
   Host: bucketname.obs.region.example.com
   Date: date
   Authorization: authorization string

   <NotificationConfiguration>
       <TopicConfiguration>
           <Id>ConfigurationId</Id>
           <Filter>
               <Object>
                   <FilterRule>
                       <Name>prefix</Name>
                       <Value>prefix-value</Value>
                   </FilterRule>
                   <FilterRule>
                       <Name>suffix</Name>
                       <Value>suffix-value</Value>
                   </FilterRule>
              </Object>
           </Filter>
           <Topic>TopicARN</Topic>
           <Event>event-type</Event>
           <Event>event-type</Event>
           ...
       </TopicConfiguration>
       ...
   </NotificationConfiguration>

Request Parameters
------------------

This request contains no message parameters.

Request Headers
---------------

This request uses common headers. For details, see :ref:`Table 3 <obs_04_0007__table25197309>`.

Request Elements
----------------

This request contains elements to specify the notification configuration for the bucket in XML format. For details about the configuration elements, see :ref:`Table 1 <obs_04_0039__table18031264>`.

.. _obs_04_0039__table18031264:

.. table:: **Table 1** Request elements for notification function configuration

   +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------+
   | Element                   | Description                                                                                                                                                                                                                                 | Mandatory                                   |
   +===========================+=============================================================================================================================================================================================================================================+=============================================+
   | NotificationConfiguration | Root element for configuring the event notification function of a bucket. If the sub element is **null**, the function is disabled.                                                                                                         | Yes                                         |
   |                           |                                                                                                                                                                                                                                             |                                             |
   |                           | Type: container                                                                                                                                                                                                                             |                                             |
   |                           |                                                                                                                                                                                                                                             |                                             |
   |                           | Ancestor: none                                                                                                                                                                                                                              |                                             |
   |                           |                                                                                                                                                                                                                                             |                                             |
   |                           | Children: zero or multiple TopicConfiguration elements                                                                                                                                                                                      |                                             |
   +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------+
   | TopicConfiguration        | Element for configuring the event notification topic.                                                                                                                                                                                       | No                                          |
   |                           |                                                                                                                                                                                                                                             |                                             |
   |                           | Type: container                                                                                                                                                                                                                             |                                             |
   |                           |                                                                                                                                                                                                                                             |                                             |
   |                           | Ancestor: NotificationConfiguration                                                                                                                                                                                                         |                                             |
   |                           |                                                                                                                                                                                                                                             |                                             |
   |                           | Children: Id, Filter, Topic, Event, or Events                                                                                                                                                                                               |                                             |
   +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------+
   | Topic                     | URN of the event notification topic. When OBS detects a specific event in the bucket, it publishes a notification message to the topic. The topic value can be found in SMN topics.                                                         | Required if **TopicConfiguration** is added |
   |                           |                                                                                                                                                                                                                                             |                                             |
   |                           | Type: string                                                                                                                                                                                                                                |                                             |
   |                           |                                                                                                                                                                                                                                             |                                             |
   |                           | Ancestor: TopicConfiguration                                                                                                                                                                                                                |                                             |
   |                           |                                                                                                                                                                                                                                             |                                             |
   |                           | Template:                                                                                                                                                                                                                                   |                                             |
   |                           |                                                                                                                                                                                                                                             |                                             |
   |                           | ::                                                                                                                                                                                                                                          |                                             |
   |                           |                                                                                                                                                                                                                                             |                                             |
   |                           |    <Topic>urn:smn:region:project_id:smn_topic</Topic>                                                                                                                                                                                       |                                             |
   |                           |                                                                                                                                                                                                                                             |                                             |
   |                           | Example:                                                                                                                                                                                                                                    |                                             |
   |                           |                                                                                                                                                                                                                                             |                                             |
   |                           | ::                                                                                                                                                                                                                                          |                                             |
   |                           |                                                                                                                                                                                                                                             |                                             |
   |                           |    <Topic>urn:smn:exampleRegion:d745b885f14941369b2d2138e7a65bef:obs_test</Topic>                                                                                                                                                           |                                             |
   +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------+
   | Id                        | Unique ID of each event notification. If the user does not specify an ID, the system assigns an ID automatically.                                                                                                                           | No                                          |
   |                           |                                                                                                                                                                                                                                             |                                             |
   |                           | Type: string                                                                                                                                                                                                                                |                                             |
   |                           |                                                                                                                                                                                                                                             |                                             |
   |                           | Ancestor: TopicConfiguration                                                                                                                                                                                                                |                                             |
   +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------+
   | Filter                    | Element used to store rules of filtering object names.                                                                                                                                                                                      | No                                          |
   |                           |                                                                                                                                                                                                                                             |                                             |
   |                           | Type: container                                                                                                                                                                                                                             |                                             |
   |                           |                                                                                                                                                                                                                                             |                                             |
   |                           | Ancestor: TopicConfiguration                                                                                                                                                                                                                |                                             |
   |                           |                                                                                                                                                                                                                                             |                                             |
   |                           | Children: Object                                                                                                                                                                                                                            |                                             |
   +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------+
   | Object                    | Element that defines the filtering rule. The rule filters objects based on the prefixes and suffixes of object names.                                                                                                                       | No                                          |
   |                           |                                                                                                                                                                                                                                             |                                             |
   |                           | Type: container                                                                                                                                                                                                                             |                                             |
   |                           |                                                                                                                                                                                                                                             |                                             |
   |                           | Ancestor: Filter                                                                                                                                                                                                                            |                                             |
   |                           |                                                                                                                                                                                                                                             |                                             |
   |                           | Children: one or more FilterRules                                                                                                                                                                                                           |                                             |
   +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------+
   | FilterRule                | Element that defines key-value pairs of the filtering rule                                                                                                                                                                                  | No                                          |
   |                           |                                                                                                                                                                                                                                             |                                             |
   |                           | Type: container                                                                                                                                                                                                                             |                                             |
   |                           |                                                                                                                                                                                                                                             |                                             |
   |                           | Ancestor: Object                                                                                                                                                                                                                            |                                             |
   |                           |                                                                                                                                                                                                                                             |                                             |
   |                           | Children: Name, Value                                                                                                                                                                                                                       |                                             |
   +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------+
   | Name                      | Prefix or suffix of object names for filtering                                                                                                                                                                                              | No                                          |
   |                           |                                                                                                                                                                                                                                             |                                             |
   |                           | Type: string                                                                                                                                                                                                                                |                                             |
   |                           |                                                                                                                                                                                                                                             |                                             |
   |                           | Ancestor: FilterRule                                                                                                                                                                                                                        |                                             |
   |                           |                                                                                                                                                                                                                                             |                                             |
   |                           | Value options: **prefix**, **suffix**                                                                                                                                                                                                       |                                             |
   +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------+
   | Value                     | Key word of object names. Based on the prefix or suffix defined by **Name**, enter the key word for filtering objects. A longer string of characters delivers a more accurate filtering result. A maximum of 1024 characters are supported. | No                                          |
   |                           |                                                                                                                                                                                                                                             |                                             |
   |                           | Type: string                                                                                                                                                                                                                                |                                             |
   |                           |                                                                                                                                                                                                                                             |                                             |
   |                           | Ancestor: FilterRule                                                                                                                                                                                                                        |                                             |
   +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------+
   | Event                     | Type of events that need to be notified                                                                                                                                                                                                     | Required if TopicConfiguration is added     |
   |                           |                                                                                                                                                                                                                                             |                                             |
   |                           | .. note::                                                                                                                                                                                                                                   |                                             |
   |                           |                                                                                                                                                                                                                                             |                                             |
   |                           |    Multiple event types can be added in one TopicConfiguration element.                                                                                                                                                                     |                                             |
   |                           |                                                                                                                                                                                                                                             |                                             |
   |                           | Type: string                                                                                                                                                                                                                                |                                             |
   |                           |                                                                                                                                                                                                                                             |                                             |
   |                           | Value options:                                                                                                                                                                                                                              |                                             |
   |                           |                                                                                                                                                                                                                                             |                                             |
   |                           | The following values can be used to upload an object:                                                                                                                                                                                       |                                             |
   |                           |                                                                                                                                                                                                                                             |                                             |
   |                           | -  ObjectCreated:Put                                                                                                                                                                                                                        |                                             |
   |                           | -  ObjectCreated:Post                                                                                                                                                                                                                       |                                             |
   |                           | -  ObjectCreated:Copy                                                                                                                                                                                                                       |                                             |
   |                           | -  ObjectCreated:CompleteMultipartUpload                                                                                                                                                                                                    |                                             |
   |                           |                                                                                                                                                                                                                                             |                                             |
   |                           | Or use wildcard characters to support all upload operations:                                                                                                                                                                                |                                             |
   |                           |                                                                                                                                                                                                                                             |                                             |
   |                           | -  ObjectCreated:\*                                                                                                                                                                                                                         |                                             |
   |                           |                                                                                                                                                                                                                                             |                                             |
   |                           | The following values can be used to delete an object:                                                                                                                                                                                       |                                             |
   |                           |                                                                                                                                                                                                                                             |                                             |
   |                           | -  ObjectRemoved:Delete                                                                                                                                                                                                                     |                                             |
   |                           | -  ObjectRemoved:DeleteMarkerCreated                                                                                                                                                                                                        |                                             |
   |                           |                                                                                                                                                                                                                                             |                                             |
   |                           | Or use wildcard characters to support all delete operations:                                                                                                                                                                                |                                             |
   |                           |                                                                                                                                                                                                                                             |                                             |
   |                           | -  ObjectRemoved:\*                                                                                                                                                                                                                         |                                             |
   |                           |                                                                                                                                                                                                                                             |                                             |
   |                           | Ancestor: TopicConfiguration                                                                                                                                                                                                                |                                             |
   +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------+

Response Syntax
---------------

::

   HTTP/1.1 status_code
   Date: date
   Content-Length: length
   Content-Type: type

Response Headers
----------------

The response to the request uses common headers. For details, see :ref:`Table 1 <obs_04_0013__d0e686>`.

Response Elements
-----------------

This response contains no elements.

Error Responses
---------------

When this operation is being called, the system checks whether the **NotificationConfiguration** element is valid and whether the configuration is valid. The following table lists the common errors and possible causes of this operation.

.. table:: **Table 2** Error codes and possible causes

   +-----------------------+-----------------------------------------------------------------------------------------------------+-----------------------+
   | Error Code            | Description                                                                                         | HTTP Status Code      |
   +=======================+=====================================================================================================+=======================+
   | InvalidArgument       | Possible causes of this error are:                                                                  | 400 Bad Request       |
   |                       |                                                                                                     |                       |
   |                       | -  The specified event is not supported.                                                            |                       |
   |                       | -  The specified URN does not exist or is incorrect.                                                |                       |
   |                       | -  The specified region in the URN is different as the region where the bucket resides.             |                       |
   |                       | -  The specified filtering rules overlap.                                                           |                       |
   +-----------------------+-----------------------------------------------------------------------------------------------------+-----------------------+
   | AccessDenied          | The operator is not the bucket owner and not granted with the **PutBucketNotification** permission. | 403 Forbidden         |
   +-----------------------+-----------------------------------------------------------------------------------------------------+-----------------------+

Sample Request
--------------

.. code-block:: text

   PUT /?notification HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: WED, 01 Jul 2015 03:15:45 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:uRTt8YTkAqJCUfWfYkveEcIGAC0=
   Content-Length: 538

   <NotificationConfiguration>
     <TopicConfiguration>
       <Id>ConfigurationId</Id>
       <Filter>
         <Object>
           <FilterRule>
             <Name>prefix</Name>
             <Value>object</Value>
           </FilterRule>
           <FilterRule>
             <Name>suffix</Name>
             <Value>txt</Value>
           </FilterRule>
         </Object>
       </Filter>
       <Topic>urn:smn:region:4b29a3cb5bd64581bda5714566814bb7:tet555</Topic>
       <Event>ObjectCreated:Put</Event>
     </TopicConfiguration>
   </NotificationConfiguration>

Sample Response
---------------

::

   HTTP/1.1 200 OK
   Server: OBS
   x-obs-request-id: 9046000001643C8E80C19FAC4D8068E3
   x-obs-id-2: 32AAAQAAEAABSAAkgAIAABAAAQAAEAABCTFAxJPTib3GkcQ7nVVs4C8Z6NNcfVDu
   Date: WED, 01 Jul 2015 03:15:46 GMT
   Content-Length: 0
