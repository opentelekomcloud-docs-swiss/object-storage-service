:original_name: en-us_topic_0125560468.html

.. _en-us_topic_0125560468:

PUT Bucket acl
==============

OBS allows you to control access permission for buckets. By default, only the creator of a bucket has **READ** and **WRITE** permission for the bucket. The creator can also set other access permission. For example, the creator can set a public-read access policy to grant READ permission to other users.

You can set an access control policy when creating a bucket, and modify or obtain the bucket access control list (ACL) using the **PUT Bucket acl** and **GET Bucket acl** operations.

Request Syntax
--------------

.. code-block:: text

   PUT /?acl HTTP/1.1
    User-Agent: agent
    Host: bucketname.obs.example.com
    Date: date
    Authorization: authorization
    Content-Length: length

    <AccessControlPolicy>
    <Owner>
    <ID>ID</ID>
    <DisplayName>displayname</DisplayName>
    </Owner>
    <AccessControlList>
    <Grant>
    <Grantee>grantee</Grantee>
    <Permission>permission</Permission>
    </Grant>
    </AccessControlList>
    </AccessControlPolicy>

Request Parameters
------------------

This request involves no parameters.

Request Headers
---------------

You can set the ACL of a bucket to a predefined ACL, also called a canned ACL. Each canned ACL has a predefined set of grantees and permission.

Optional header **x-amz-acl** is used in this request to specify canned ACLs. :ref:`Table 1 <en-us_topic_0125560468__table37355450>` describes the optional header.

.. _en-us_topic_0125560468__table37355450:

.. table:: **Table 1** Optional header for specifying canned ACLs

   +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | Header                | Description                                                                                                                                                                        | Remarks                                                                          |
   +=======================+====================================================================================================================================================================================+==================================================================================+
   | x-amz-acl             | Indicates the canned ACL applied to a bucket.                                                                                                                                      | Optional                                                                         |
   |                       |                                                                                                                                                                                    |                                                                                  |
   |                       | Type: String                                                                                                                                                                       |                                                                                  |
   |                       |                                                                                                                                                                                    |                                                                                  |
   |                       | Valid values: **private\| public-read\| public-read-write|authenticated-read|bucket-owner-read|bucket-owner-full-control|log-delivery-write**                                      |                                                                                  |
   +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | x-amz-security-token  | Header field used to identify the request of a federated user. When the federal authentication function is enabled, users sending such requests are identified as federated users. | Optional. This parameter must be carried in the request sent by federated users. |
   |                       |                                                                                                                                                                                    |                                                                                  |
   |                       | Type: string                                                                                                                                                                       |                                                                                  |
   +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+

Request Elements
----------------

This request uses elements to specify an ACL. :ref:`Table 2 <en-us_topic_0125560468__table41811761>` describes the elements.

.. _en-us_topic_0125560468__table41811761:

.. table:: **Table 2** Request elements

   +-----------------------+-----------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Element               | Description                                                                                                           | Remarks               |
   +=======================+=======================================================================================================================+=======================+
   | Owner                 | Indicates the bucket owner. This element consists of **ID** and **DisplayName**.                                      | Optional              |
   |                       |                                                                                                                       |                       |
   |                       | Type: XML                                                                                                             |                       |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------+-----------------------+
   | ID                    | Indicates the DomainId of a grantee.                                                                                  | Optional              |
   |                       |                                                                                                                       |                       |
   |                       | Type: String                                                                                                          |                       |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------+-----------------------+
   | DisplayName           | Indicates the name of the grantee.                                                                                    | Optional              |
   |                       |                                                                                                                       |                       |
   |                       | Type: String                                                                                                          |                       |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Grant                 | Container for the grantee and its permission.                                                                         | Optional              |
   |                       |                                                                                                                       |                       |
   |                       | Type: XML                                                                                                             |                       |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Grantee               | Container for the details about the grantee. For details, see :ref:`Table 1 <en-us_topic_0125560406__table49181932>`. | Optional              |
   |                       |                                                                                                                       |                       |
   |                       | Type: XML                                                                                                             |                       |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Permission            | Indicates the permission to be granted. For details, see :ref:`Table 2 <en-us_topic_0125560406__table39984204>`.      | Optional              |
   |                       |                                                                                                                       |                       |
   |                       | Type: Enumeration                                                                                                     |                       |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------+-----------------------+
   | AccessControlList     | Indicates the ACL. This element consists of **Grant**, **Grantee**, and **Permission**.                               | Optional              |
   |                       |                                                                                                                       |                       |
   |                       | Type: XML                                                                                                             |                       |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------+-----------------------+

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

Response Elements
-----------------

This response involves no elements.

Error Responses
---------------

No special error responses are returned. For details about error responses, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`.

Sample Request for Setting the Bucket ACL
-----------------------------------------

.. code-block:: text

   PUT /?acl HTTP/1.1
    User-Agent: Jakarta Commons-HttpClient/3.1
    Host: bucketname.obs.example.com
    Accept-Encoding: gzip,deflate
    Date: Mon, 27 Sep 2010 01:37:17 GMT
    Authorization: AWS 04RZT432N80TGDF2Y2G2:9uNLINAQ7IOIrD9OnCpDfY2R6nU=
    Content-Length: 598

    <AccessControlPolicy>
    <Owner>
    <ID>bcaf1ffd86f41caff1a493dc2ad8c2c2</ID>
    <DisplayName>user</DisplayName>
    </Owner>
    <AccessControlList>
    <Grant>
    <Grantee xsi:type="CanonicalUser" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <ID>bcaf1ffd86f41caff1a493dc2ad8c2c2</ID>
    <DisplayName>user</DisplayName>
    </Grantee>
    <Permission>READ</Permission>
    </Grant>
    </AccessControlList>
    </AccessControlPolicy>

Sample Response for Setting the Bucket ACL
------------------------------------------

.. code-block::

   HTTP/1.1 200 OK
    Server: OBS
    x-amz-request-id: 7B6DFC9BC71DD58B061285551605709
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    x-amz-id-2: N0I2REZDOUJDNzFERDU4QjA2MTI4NTU1MTYwNTcwOUFBQUFBQUFBYmJiYmJiYmJD
    Date: Mon, 27 Sep 2010 01:40:03 GMT
    Content-Length: 0

Sample Request for Setting the Bucket ACL Using Headers
-------------------------------------------------------

.. code-block:: text

   PUT /?acl HTTP/1.1
   User-Agent: curl/7.19.0
   Host: bucketname.obs.example.com
   Accept: */*
   Date: Mon, 27 Sep 2010 01:37:17 GMT
   Authorization: AWS 04RZT432N80TGDF2Y2G2:9uNLINAQ7IOIrD9OnCpDfY2R6nU=
   x-amz-acl: private

Sample Response for Setting the Bucket ACL Using Headers
--------------------------------------------------------

.. code-block::

   HTTP/1.1 200 OK
    Server: OBS
    x-amz-request-id: 7B6DFC9BC71DD58B061285551605709
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    x-amz-id-2: N0I2REZDOUJDNzFERDU4QjA2MTI4NTU1MTYwNTcwOUFBQUFBQUFBYmJiYmJiYmJD
    Content-Type: application/xml
    Date: Mon, 27 Sep 2010 01:40:03 GMT
    Content-Length: 526
