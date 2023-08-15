:original_name: en-us_topic_0125560314.html

.. _en-us_topic_0125560314:

GET Bucket acl
==============

After being granted **READ_ACP** or **FULL_CONTROL** permission for a bucket, you can obtain its ACL.

Request Syntax
--------------

.. code-block:: text

   GET /?acl HTTP/1.1
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
    <AccessControlPolicy xmlns="http://obs.example.com/doc/2015-06-30/">
    <Owner>
    <ID>id</ID>
    <DisplayName>name</DisplayName>
    </Owner>
    <AccessControlList>
    <Grant>
    <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="CanonicalUser">
    <ID>id</ID>
    <DisplayName>name</DisplayName>
    </Grantee>
    <Permission>permission</Permission>
    </Grant>
    </AccessControlList>
    </AccessControlPolicy>

Response Headers
----------------

This response uses common headers. For details about common response headers, see section :ref:`Common Response Headers <en-us_topic_0125560484>`.

Response Elements
-----------------

This response contains elements to provide details about a bucket ACL. :ref:`Table 1 <en-us_topic_0125560314__table46938871>` describes the elements.

.. _en-us_topic_0125560314__table46938871:

.. table:: **Table 1** Response elements

   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------+
   | Element                           | Description                                                                                                            |
   +===================================+========================================================================================================================+
   | Owner                             | Indicates the bucket owner.                                                                                            |
   |                                   |                                                                                                                        |
   |                                   | Type: XML                                                                                                              |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------+
   | ID                                | DomainId of the user.                                                                                                  |
   |                                   |                                                                                                                        |
   |                                   | Type: String                                                                                                           |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------+
   | DisplayName                       | Indicates the user name.                                                                                               |
   |                                   |                                                                                                                        |
   |                                   | Type: String                                                                                                           |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------+
   | AccessControlList                 | Indicates the ACL that records all users who have permission to access the bucket and permission granted to the users. |
   |                                   |                                                                                                                        |
   |                                   | Type: XML                                                                                                              |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------+
   | Grant                             | Container for the grantee and its permission.                                                                          |
   |                                   |                                                                                                                        |
   |                                   | Type: XML                                                                                                              |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------+
   | Grantee                           | Container for the details about the grantee.                                                                           |
   |                                   |                                                                                                                        |
   |                                   | Type: XML                                                                                                              |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------+
   | Permission                        | Indicates the grantee's permission for a bucket.                                                                       |
   |                                   |                                                                                                                        |
   |                                   | Type: String                                                                                                           |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------+

Error Responses
---------------

No special errors are returned. For details about error responses, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`.

Sample Request
--------------

.. code-block:: text

   GET /?acl HTTP/1.1
    User-Agent: Jakarta Commons-HttpClient/3.1
    Host: bucketname.obs.example.com
    Accept-Encoding: gzip,deflate
    Date: Mon, 27 Sep 2010 01:22:05 GMT
    Authorization: AWS 04RZT432N80TGDF2Y2G2:FAcC4bDx0izVL9lEH521v01in/Y=

Sample Response
---------------

.. code-block::

   HTTP/1.1 200 OK
    Server: OBS
    x-amz-request-id: 7B6DFC9BC71DD58B061285550689635
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    x-amz-id-2: N0I2REZDOUJDNzFERDU4QjA2MTI4NTU1MDY4OTYzNUFBQUFBQUFBYmJiYmJiYmJD
    Content-Type: application/xml
    Date: Mon, 27 Sep 2010 01:24:47 GMT
    Content-Length: 560

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <AccessControlPolicy xmlns="http://obs.example.com/doc/2015-06-30/">
    <Owner>
    <ID>bcaf1ffd86f41caff1a493dc2ad8c2c281e37522a640e161ca5fb16fd081034f</ID>
    <DisplayName>apple</DisplayName>
    </Owner>
    <AccessControlList>
    <Grant>
    <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="CanonicalUser">            <ID>bcaf1ffd86f41caff1a493dc2ad881e37540e161ca5fb16fd081034f</ID>
    <DisplayName>apple</DisplayName>
    </Grantee>
    <Permission>FULL_CONTROL</Permission>
    </Grant>
    </AccessControlList>
    </AccessControlPolicy>
