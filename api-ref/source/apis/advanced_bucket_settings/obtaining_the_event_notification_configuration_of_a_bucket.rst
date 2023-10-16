:original_name: obs_04_0040.html

.. _obs_04_0040:

Obtaining the Event Notification Configuration of a Bucket
==========================================================

Functions
---------

This operation obtains the notification configuration of a bucket.

To perform this operation, you must have the **GetBucketNotification** permission. By default, the permission is granted to the bucket owner only. However, it can be granted to other users by configuring the bucket policy or user policy.

Request Syntax
--------------

.. code-block:: text

   GET /?notification HTTP/1.1
   Host: bucketname.obs.region.example.com
   Date: date
   Authorization: authorization

Request Parameters
------------------

This request contains no message parameters.

Request Headers
---------------

This request uses common headers. For details, see :ref:`Table 3 <obs_04_0007__table25197309>`.

Request Elements
----------------

This request involves no elements.

Response Syntax
---------------

::

   HTTP/1.1 status_code
   Content-Type: type
   Date: date
   Content-Length: length

   <?xml version="1.0" encoding="UTF-8"?>
   <NotificationConfiguration xmlns="http://obs.example.com/doc/2015-06-30/">
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
   </NotificationConfiguration>

Response Headers
----------------

The response to the request uses common headers. For details, see :ref:`Table 1 <obs_04_0013__d0e686>`.

Response Elements
-----------------

This response contains elements to detail the configuration. :ref:`Table 1 <obs_04_0040__table6153252715448>` describes the elements.

.. _obs_04_0040__table6153252715448:

.. table:: **Table 1** Response elements for configuring event notifications

   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------+
   | Element                           | Description                                                                                                                 |
   +===================================+=============================================================================================================================+
   | NotificationConfiguration         | Element for configuring the event notification function of a bucket. If this element is **null**, the function is disabled. |
   |                                   |                                                                                                                             |
   |                                   | Type: container                                                                                                             |
   |                                   |                                                                                                                             |
   |                                   | Ancestor: none                                                                                                              |
   |                                   |                                                                                                                             |
   |                                   | Children: one or more TopicConfiguration elements                                                                           |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------+
   | TopicConfiguration                | Element for configuring the event notification topic.                                                                       |
   |                                   |                                                                                                                             |
   |                                   | Type: container                                                                                                             |
   |                                   |                                                                                                                             |
   |                                   | Ancestor: NotificationConfiguration                                                                                         |
   |                                   |                                                                                                                             |
   |                                   | Children: Id, Filter, Topic, Event, or Events                                                                               |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------+
   | Topic                             | URN of the event notification topic. After detecting a specific event in the bucket, OBS sends a message to the topic.      |
   |                                   |                                                                                                                             |
   |                                   | Type: string                                                                                                                |
   |                                   |                                                                                                                             |
   |                                   | Ancestor: TopicConfiguration                                                                                                |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------+
   | Id                                | Unique ID of each event notification. If the user does not specify an ID, the system assigns an ID automatically.           |
   |                                   |                                                                                                                             |
   |                                   | Type: string                                                                                                                |
   |                                   |                                                                                                                             |
   |                                   | Ancestor: TopicConfiguration                                                                                                |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------+
   | Filter                            | Element used to store rules of filtering object names.                                                                      |
   |                                   |                                                                                                                             |
   |                                   | Type: container                                                                                                             |
   |                                   |                                                                                                                             |
   |                                   | Ancestor: TopicConfiguration                                                                                                |
   |                                   |                                                                                                                             |
   |                                   | Children: Object                                                                                                            |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------+
   | Object                            | Element used to store rules of filtering object names.                                                                      |
   |                                   |                                                                                                                             |
   |                                   | Type: container                                                                                                             |
   |                                   |                                                                                                                             |
   |                                   | Ancestor: TopicConfiguration                                                                                                |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------+
   | FilterRule                        | Element that defines key-value pairs of the filtering rule.                                                                 |
   |                                   |                                                                                                                             |
   |                                   | Type: container                                                                                                             |
   |                                   |                                                                                                                             |
   |                                   | Ancestor: Object                                                                                                            |
   |                                   |                                                                                                                             |
   |                                   | Children: Name, Value                                                                                                       |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------+
   | Name                              | Prefix or suffix of object names for filtering                                                                              |
   |                                   |                                                                                                                             |
   |                                   | Type: string                                                                                                                |
   |                                   |                                                                                                                             |
   |                                   | Ancestor: FilterRule                                                                                                        |
   |                                   |                                                                                                                             |
   |                                   | Value options: **prefix**, **suffix**                                                                                       |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------+
   | Value                             | Keywords of object names so that objects can be filtered based on the prefixes or suffixes                                  |
   |                                   |                                                                                                                             |
   |                                   | Type: string                                                                                                                |
   |                                   |                                                                                                                             |
   |                                   | Ancestor: FilterRule                                                                                                        |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------+
   | Event                             | Type of events that need to be notified                                                                                     |
   |                                   |                                                                                                                             |
   |                                   | .. note::                                                                                                                   |
   |                                   |                                                                                                                             |
   |                                   |    Multiple event types can be added in one TopicConfiguration element.                                                     |
   |                                   |                                                                                                                             |
   |                                   | Type: string                                                                                                                |
   |                                   |                                                                                                                             |
   |                                   | Value options:                                                                                                              |
   |                                   |                                                                                                                             |
   |                                   | The following values can be used to upload an object:                                                                       |
   |                                   |                                                                                                                             |
   |                                   | -  ObjectCreated:Put                                                                                                        |
   |                                   | -  ObjectCreated:Post                                                                                                       |
   |                                   | -  ObjectCreated:Copy                                                                                                       |
   |                                   | -  ObjectCreated:CompleteMultipartUpload                                                                                    |
   |                                   |                                                                                                                             |
   |                                   | Or use wildcard characters to support all upload operations:                                                                |
   |                                   |                                                                                                                             |
   |                                   | -  ObjectCreated:\*                                                                                                         |
   |                                   |                                                                                                                             |
   |                                   | The following values can be used to delete an object:                                                                       |
   |                                   |                                                                                                                             |
   |                                   | -  ObjectRemoved:Delete                                                                                                     |
   |                                   | -  ObjectRemoved:DeleteMarkerCreated                                                                                        |
   |                                   |                                                                                                                             |
   |                                   | Or use wildcard characters to support all delete operations:                                                                |
   |                                   |                                                                                                                             |
   |                                   | -  ObjectRemoved:\*                                                                                                         |
   |                                   |                                                                                                                             |
   |                                   | Ancestor: TopicConfiguration                                                                                                |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------+

Error Responses
---------------

No special error responses are returned. For details about error responses, see :ref:`Table 2 <obs_04_0115__d0e843>`.

Sample Request
--------------

.. code-block:: text

   GET /?notification HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: WED, 01 Jul 2015 03:16:32 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:r5+2zwPTKwupMg6lkeTUUqPcHfQ=

Sample Response
---------------

::

   HTTP/1.1 200 OK
   Server: OBS
   x-obs-request-id: 900B000001643FDDD751B37BA87590D8
   x-obs-id-2: 32AAAQAAEAABAAAQAAEAABAAAQAAEAABCSJRBSladan5ZCVw6ZIY/DAs0zs6z7Hh
   Content-Type: application/xml
   Date: WED, 01 Jul 2015 03:16:32 GMT
   Content-Length: 490

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <NotificationConfiguration xmlns="http://obs.example.com/doc/2015-06-30/">
     <TopicConfiguration>
       <Topic>urn:smn:region:4b29a3cb5bd64581bda5714566814bb7:tet522</Topic>
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
       <Event>ObjectCreated:Put</Event>
     </TopicConfiguration>
   </NotificationConfiguration>
