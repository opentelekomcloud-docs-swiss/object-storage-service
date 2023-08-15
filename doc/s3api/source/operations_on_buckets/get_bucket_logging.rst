:original_name: en-us_topic_0125560463.html

.. _en-us_topic_0125560463:

GET Bucket logging
==================

You can use this operation to query the logging status of a bucket. This GET operation uses the **logging** subresource to return the logging status of a bucket.

Only the bucket owner or users granted the **s3:GetBucketLogging** permission can query the bucket logging status.

Request Syntax
--------------

.. code-block:: text

   GET /?logging HTTP/1.1
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
    Content-Length:length

    <?xml version="1.0" encoding="UTF-8"?>
    <BucketLoggingStatus xmlns="http://obs.example.com/doc/2006-03-01/">
    <LoggingEnabled>
    <TargetBucket>bucketName</TargetBucket>
    <TargetPrefix>prefix</TargetPrefix>
    <TargetGrants>
    <Grant>
    <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="CanonicalUser">
    <ID>id</ID>
    <DisplayName>displayName</DisplayName>
    </Grantee>
    <Permission>permission</Permission>
    </Grant>
    </TargetGrants>
    </LoggingEnabled>
    </BucketLoggingStatus>

Response Headers
----------------

This response uses common headers. For details about common response headers, see section :ref:`Common Response Headers <en-us_topic_0125560484>`.

Response Elements
-----------------

This response contains elements to specify the bucket logging status. :ref:`Table 1 <en-us_topic_0125560463__table56643352>` describes the elements.

.. _en-us_topic_0125560463__table56643352:

.. table:: **Table 1** Response elements

   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Element               | Description                                                                                                                                                                                                                    | Remarks               |
   +=======================+================================================================================================================================================================================================================================+=======================+
   | BucketLoggingStatus   | Indicates the container for logging status information.                                                                                                                                                                        | Mandatory             |
   |                       |                                                                                                                                                                                                                                |                       |
   |                       | Type: Container                                                                                                                                                                                                                |                       |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | LoggingEnabled        | Indicates the container for logging information. This element is present when you are enabling logging (and not present when you are disabling logging).                                                                       | Optional              |
   |                       |                                                                                                                                                                                                                                |                       |
   |                       | Type: Container                                                                                                                                                                                                                |                       |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Grant                 | Indicates the container for the grantee and the grantee's logging permission.                                                                                                                                                  | Optional              |
   |                       |                                                                                                                                                                                                                                |                       |
   |                       | Type: Container                                                                                                                                                                                                                |                       |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Grantee               | Indicates the container for users granted logging permission.                                                                                                                                                                  | Optional              |
   |                       |                                                                                                                                                                                                                                |                       |
   |                       | Type: Container                                                                                                                                                                                                                |                       |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | ID                    | DomainId of the grantee, Indicates the globally unique ID.                                                                                                                                                                     | Optional              |
   |                       |                                                                                                                                                                                                                                |                       |
   |                       | Type: String                                                                                                                                                                                                                   |                       |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | DisplayName           | Indicates the name of the grantee. This element is not globally unique but a user ID corresponds to only one name.                                                                                                             | Optional              |
   |                       |                                                                                                                                                                                                                                |                       |
   |                       | Type: String                                                                                                                                                                                                                   |                       |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Permission            | Indicates the logging permission granted to the grantee for a bucket. The bucket owner is automatically granted the **FULL_CONTROL** permission when creating the bucket. Logging permission control access to different logs. | Optional              |
   |                       |                                                                                                                                                                                                                                |                       |
   |                       | Type: String                                                                                                                                                                                                                   |                       |
   |                       |                                                                                                                                                                                                                                |                       |
   |                       | Valid Values: FULL_CONTROL \| READ \| WRITE                                                                                                                                                                                    |                       |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | TargetBucket          | Specifies the target bucket where bucket logs are stored. In OBS, logs of multiple buckets can be stored in the same target bucket. In this case, you need to use different **TargetPrefix** to distinguish the logs.          | Optional              |
   |                       |                                                                                                                                                                                                                                |                       |
   |                       | Type: String                                                                                                                                                                                                                   |                       |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | TargetPrefix          | Specifies a prefix for keys of logs to be stored.                                                                                                                                                                              | Optional              |
   |                       |                                                                                                                                                                                                                                |                       |
   |                       | Type: String                                                                                                                                                                                                                   |                       |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | TargetGrants          | Indicates the container for granting information.                                                                                                                                                                              | Optional              |
   |                       |                                                                                                                                                                                                                                |                       |
   |                       | Type: Container                                                                                                                                                                                                                |                       |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

Error Responses
---------------

No special error responses are returned. For details about error responses, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`.

Sample Request
--------------

.. code-block:: text

   GET /?logging HTTP/1.1
    User-Agent: curl/7.19.0
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Wed, 25 Nov 2009 12:00:00 GMT
    Authorization: AWS UDSIAMSTUBTEST000002:IuWiXuyanEXDOKUMdUnyZ2J83sA=

Sample Response
---------------

.. code-block::

   HTTP/1.1 200 OK
    Server: OBS
    x-amz-request-id: 0000016594648286822DDF9487214C88
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    x-amz-id-2: 32AAAQAAEAABAAAQAAEAABAAAQAAEAABCSWVP7N5CZQGJzkZXBosuFJjC7XFsYQq
    Date: Wed, 25 Nov 2009 12:00:00 GMT
    Content_Length:277

    <?xml version="1.0" encoding="UTF-8"?>
    <BucketLoggingStatus xmlns="http://obs.example.com/doc/2006-03-01/">
    <LoggingEnabled>
    <TargetBucket>logging.bucket1</TargetBucket>
    <TargetPrefix>access_log</TargetPrefix>
    <TargetGrants>
    <Grant>
    <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="CanonicalUser">
    <ID>af258a3a0a1c2cd93011f75c1e031c043f47a25048490c8742f2f942464794e0</ID>
    <DisplayName>user</DisplayName>
    </Grantee>
    <Permission>FULL_CONTROL</Permission>
    </Grant>
    </TargetGrants>
    </LoggingEnabled>
    </BucketLoggingStatus>
