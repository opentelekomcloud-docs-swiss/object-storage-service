:original_name: en-us_topic_0125560299.html

.. _en-us_topic_0125560299:

PUT Bucket logging
==================

This operation is used to control access to logs. You can use this operation to grant specific users permission to view or modify bucket logs.

This PUT operation uses the **logging** subresource to set the logging parameters of a bucket. In the current OBS version, only the bucket owner or users granted the **s3:PutBucketLogging** permission can view or modify the bucket logging parameters.

By default, logs are not created during bucket creation. The logs for a bucket are created after logging in enabled. To enable logging, configure the log management function in the **LoggingEnabled** request element. You can disable logging using an empty **BucketLoggingStatus** request element. To ensure log files are delivered correctly, the log delivery group must also have **WRITE** and **READ_ACP** permission for the target bucket which stores logging.

When configuring bucket log management, the owner of the source bucket can specify a target bucket to store logs. The owner of the source bucket can only deliver logs to any bucket of the owner. In the mean time, the target bucket and source bucket must reside in the same region. When uploading a log object, its storage class is set to Standard.

The traffic consumed by uploading bucket logs is not charged, but it will be reflected in the uplink traffic of the Cloud Eye service.

Request Syntax
--------------

.. code-block:: text

   PUT /?logging HTTP/1.1
    User-Agent: agent
    Host: bucketname.obs.example.com
    Accept: */*
    Date: date
    Authorization: signatureValue

   logging configuration

Request Parameters
------------------

This request involves no parameters.

Request Headers
---------------

This request uses common headers. For details about common request headers, see section :ref:`Common Request Headers <en-us_topic_0125560462>`.

Request Elements
----------------

.. table:: **Table 1** Request elements

   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Element               | Description                                                                                                                                                                                                                                                                                                                                                                                     | Remarks               |
   +=======================+=================================================================================================================================================================================================================================================================================================================================================================================================+=======================+
   | BucketLoggingStatus   | Indicates the container for logging status information.                                                                                                                                                                                                                                                                                                                                         | Mandatory             |
   |                       |                                                                                                                                                                                                                                                                                                                                                                                                 |                       |
   |                       | Type: Container                                                                                                                                                                                                                                                                                                                                                                                 |                       |
   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | LoggingEnabled        | Indicates the container for logging information. This element is present when you are enabling logging (and not present when you are disabling logging). You can add specific logging information in this element.                                                                                                                                                                              | Optional              |
   |                       |                                                                                                                                                                                                                                                                                                                                                                                                 |                       |
   |                       | Type: Container                                                                                                                                                                                                                                                                                                                                                                                 |                       |
   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Grant                 | Indicates the container for the grantee and the grantee's logging permission.                                                                                                                                                                                                                                                                                                                   | Optional              |
   |                       |                                                                                                                                                                                                                                                                                                                                                                                                 |                       |
   |                       | Type: Container                                                                                                                                                                                                                                                                                                                                                                                 |                       |
   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Grantee               | Indicates the container for users granted logging permission.                                                                                                                                                                                                                                                                                                                                   | Optional              |
   |                       |                                                                                                                                                                                                                                                                                                                                                                                                 |                       |
   |                       | Type: Container                                                                                                                                                                                                                                                                                                                                                                                 |                       |
   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | ID                    | DomainId of the grantee, Indicates the globally unique ID.                                                                                                                                                                                                                                                                                                                                      | Optional              |
   |                       |                                                                                                                                                                                                                                                                                                                                                                                                 |                       |
   |                       | Type: String                                                                                                                                                                                                                                                                                                                                                                                    |                       |
   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | DisplayName           | Indicates the name of the grantee. This element is not globally unique but a user ID corresponds to only one name.                                                                                                                                                                                                                                                                              | Optional              |
   |                       |                                                                                                                                                                                                                                                                                                                                                                                                 |                       |
   |                       | Type: String                                                                                                                                                                                                                                                                                                                                                                                    |                       |
   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Permission            | Indicates the logging permission granted to the grantee for a bucket. The bucket owner is automatically granted the **FULL_CONTROL** permission when creating the bucket. Logging permission control access to different logs.                                                                                                                                                                  | Optional              |
   |                       |                                                                                                                                                                                                                                                                                                                                                                                                 |                       |
   |                       | Type: String                                                                                                                                                                                                                                                                                                                                                                                    |                       |
   |                       |                                                                                                                                                                                                                                                                                                                                                                                                 |                       |
   |                       | Valid Values: FULL_CONTROL \| READ \| WRITE                                                                                                                                                                                                                                                                                                                                                     |                       |
   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | TargetBucket          | Specifies the target bucket where bucket logs are stored. You can only have your logs delivered to any bucket that you own. User groups that deliver logs to the target bucket must have the **WRITE** and **READ_ACP** permission. In OBS, logs of multiple buckets can be stored in the same target bucket. In this case, you need to use different **TargetPrefix** to distinguish the logs. | Mandatory             |
   |                       |                                                                                                                                                                                                                                                                                                                                                                                                 |                       |
   |                       | Type: String                                                                                                                                                                                                                                                                                                                                                                                    |                       |
   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | TargetPrefix          | Specifies a prefix for keys of logs to be stored.                                                                                                                                                                                                                                                                                                                                               | Mandatory             |
   |                       |                                                                                                                                                                                                                                                                                                                                                                                                 |                       |
   |                       | Type: String                                                                                                                                                                                                                                                                                                                                                                                    |                       |
   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | TargetGrants          | Indicates the container for granting information.                                                                                                                                                                                                                                                                                                                                               | Optional              |
   |                       |                                                                                                                                                                                                                                                                                                                                                                                                 |                       |
   |                       | Type: Container                                                                                                                                                                                                                                                                                                                                                                                 |                       |
   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

Response Syntax
---------------

.. code-block::

   HTTP/1.1 status_code
    Server: Server Name
    x-amz-request-id: request id
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    x-amz-id-2: id
    Date: date
    Content-Length: length

Response Headers
----------------

This response uses common headers. For details about common response headers, see section :ref:`Common Response Headers <en-us_topic_0125560484>`.

Response elements
-----------------

This response involves no elements.

Error Responses
---------------

No special error responses are returned. For details about error responses, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`.

Sample Requests
---------------

Configure the ACL for the target bucket to which logs are delivered

.. code-block:: text

   PUT /?acl HTTP/1.1
   User-Agent: Jakarta Commons-HttpClient/3.1
   Host: bucketname.obs.example.com
   Accept-Encoding: gzip,deflate
   Date: Mon, 27 Sep 2010 01:37:17 GMT
   Authorization: AWS 04RZT432N80TGDF2Y2G2:9uNLINAQ7IOIrD9OnCpDfY2R6nU=
   Content-Length: 598

   <AccessControlPolicy xmlns="http://obs.example.com/doc/2006-03-01/">
   <Owner>
   <ID>0022A1B8CD8B00000145870549B10002</ID>
   <DisplayName>huangjiang112</DisplayName>
   </Owner>
   <AccessControlList>
   <Grant>
   <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="CanonicalUser">
   <ID>0022A1B8CD8B00000145870549B10002</ID>
   <DisplayName>user</DisplayName>
   </Grantee>
   <Permission>FULL_CONTROL</Permission>
   </Grant>
   <Grant>
   <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="Group">
   <URI>http://acs.amazonaws.com/groups/s3/LogDelivery</URI>
   </Grantee>
   <Permission>FULL_CONTROL</Permission>
   </Grant>
   </AccessControlList>
   </AccessControlPolicy>

Configure logging for the source bucket

.. code-block:: text

   PUT /?logging HTTP/1.1
    User-Agent: curl/7.19.0
    Host: bucketname.obs.example.com
    Accept: */*
    Date: date
    Authorization: signatureValue
    Content-Length: 649

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

Sample Responses
----------------

Set Acl Response

.. code-block::

   HTTP/1.1 200 OK
   x-amz-request-id: 7B6DFC9BC71DD58B061285551605709
   x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
   x-amz-id-2: N0I2REZDOUJDNzFERDU4QjA2MTI4NTU1MTYwNTcwOUFBQUFBQUFBYmJiYmJiYmJD
   Content-Type: text/xml
   Date: Mon, 27 Sep 2010 01:40:03 GMT
   Content-Length: 0

Put Logging Response

.. code-block::

   HTTP/1.1 200 OK
    Server: OBS
    x-amz-request-id: 7B6DFC9BC71DD58B061285551605709
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    x-amz-id-2: N0I2REZDOUJDNzFERDU4QjA2MTI4NTU1MTYwNTcwOUFBQUFBQUFBYmJiYmJiYmJD
    Date: Mon, 27 Sep 2010 01:40:03 GMT
    Content-Length: 0
