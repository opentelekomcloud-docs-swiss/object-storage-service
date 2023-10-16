:original_name: obs_04_0033.html

.. _obs_04_0033:

Obtaining a Bucket Logging Configuration
========================================

Functions
---------

This operation queries the logging status of a bucket. It uses the logging sub-resource to return the logging status of a bucket.

Only the bucket owner or users granted the **GetBucketLogging** permission can query the bucket logging status.

Request Syntax
--------------

.. code-block:: text

   GET /?logging HTTP/1.1
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
   Content-Type: application/xml
   Date: date
   Content-Length: length

   <?xml version="1.0" encoding="UTF-8"?>
   <BucketLoggingStatus xmlns="http://obs.region.example.com/doc/2015-06-30/">
   <Agency>agency-name</Agency>
   <LoggingEnabled>
       <TargetBucket>bucketName</TargetBucket>
       <TargetPrefix>prefix</TargetPrefix>
           <TargetGrants>
               <Grant>
                   <Grantee>
                       <ID>id</ID>
                   </Grantee>
                   <Permission>permission</Permission>
               </Grant>
           </TargetGrants>
       </LoggingEnabled>
   </BucketLoggingStatus>

Response Headers
----------------

The response to the request uses common headers. For details, see :ref:`Table 1 <obs_04_0013__d0e686>`.

Response Elements
-----------------

This response contains elements to specify the bucket logging status. :ref:`Table 1 <obs_04_0033__table64048341152231>` describes the elements.

.. _obs_04_0033__table64048341152231:

.. table:: **Table 1** Response elements

   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Element                           | Description                                                                                                                                                                                                                                                                                                                 |
   +===================================+=============================================================================================================================================================================================================================================================================================================================+
   | BucketLoggingStatus               | Container for logging status information                                                                                                                                                                                                                                                                                    |
   |                                   |                                                                                                                                                                                                                                                                                                                             |
   |                                   | Type: container                                                                                                                                                                                                                                                                                                             |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Agency                            | Name of the agency created by the owner of the logging bucket for uploading log files by OBS                                                                                                                                                                                                                                |
   |                                   |                                                                                                                                                                                                                                                                                                                             |
   |                                   | Type: string                                                                                                                                                                                                                                                                                                                |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | LoggingEnabled                    | Container for logging information. This element enables or disables the logging function. Present this element when enabling the logging. Otherwise, absent it.                                                                                                                                                             |
   |                                   |                                                                                                                                                                                                                                                                                                                             |
   |                                   | Type: container                                                                                                                                                                                                                                                                                                             |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Grant                             | Container for the grantee and the granted permissions                                                                                                                                                                                                                                                                       |
   |                                   |                                                                                                                                                                                                                                                                                                                             |
   |                                   | Type: container                                                                                                                                                                                                                                                                                                             |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Grantee                           | Container for the user that is granted with the logging permission                                                                                                                                                                                                                                                          |
   |                                   |                                                                                                                                                                                                                                                                                                                             |
   |                                   | Type: container                                                                                                                                                                                                                                                                                                             |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ID                                | Grantee domain ID, a globally unique ID                                                                                                                                                                                                                                                                                     |
   |                                   |                                                                                                                                                                                                                                                                                                                             |
   |                                   | Type: string                                                                                                                                                                                                                                                                                                                |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Permission                        | Logging permission granted to the grantee for a bucket. The bucket owner is automatically granted the **FULL_CONTROL** permission when creating the bucket. Logging permissions control access to different logs.                                                                                                           |
   |                                   |                                                                                                                                                                                                                                                                                                                             |
   |                                   | Type: string                                                                                                                                                                                                                                                                                                                |
   |                                   |                                                                                                                                                                                                                                                                                                                             |
   |                                   | Value options: **FULL_CONTROL**, **READ**, **WRITE**                                                                                                                                                                                                                                                                        |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | TargetBucket                      | When enabling the logging function, the owner of the bucket being logged can specify a target bucket to store the generated log files. Log files generated for multiple buckets can be stored in the same target bucket. If you do so, you need to specify different TargetPrefixes to classify logs for different buckets. |
   |                                   |                                                                                                                                                                                                                                                                                                                             |
   |                                   | Type: string                                                                                                                                                                                                                                                                                                                |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | TargetPrefix                      | You can specify a prefix using this element so that log files are named with this prefix.                                                                                                                                                                                                                                   |
   |                                   |                                                                                                                                                                                                                                                                                                                             |
   |                                   | Type: string                                                                                                                                                                                                                                                                                                                |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | TargetGrants                      | Container for granting information                                                                                                                                                                                                                                                                                          |
   |                                   |                                                                                                                                                                                                                                                                                                                             |
   |                                   | Type: container                                                                                                                                                                                                                                                                                                             |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Error Responses
---------------

No special error responses are returned. For details about error responses, see :ref:`Table 2 <obs_04_0115__d0e843>`.

Sample Request
--------------

.. code-block:: text

   GET /?logging HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: WED, 01 Jul 2015 02:42:46 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:hUk+jTnR07hcKwJh4ousF2E1U3E=

Sample Response
---------------

::

   HTTP/1.1 200 OK
   Server: OBS
   x-obs-request-id: BF260000016436B8EEE7FBA2AA3335E3
   x-obs-id-2: 32AAAQAAEAABAAAQAAEAABAAAQAAEAABCShuQJoWFpS77C8bOv1mqURv0UY+0ejx
   Content-Type: application/xml
   Date: WED, 01 Jul 2015 02:42:46 GMT
   Content-Length: 429

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <BucketLoggingStatus xmlns="http://obs.example.com/doc/2015-06-30/">
     <Agency>agency-name</Agency>
     <LoggingEnabled>
       <TargetBucket>log-bucket</TargetBucket>
       <TargetPrefix>mybucket-access_log-/</TargetPrefix>
       <TargetGrants>
         <Grant>
           <Grantee>
             <ID>b4bf1b36d9ca43d984fbcb9491b6fce9</ID>
           </Grantee>
           <Permission>READ</Permission>
         </Grant>
       </TargetGrants>
     </LoggingEnabled>
   </BucketLoggingStatus>
