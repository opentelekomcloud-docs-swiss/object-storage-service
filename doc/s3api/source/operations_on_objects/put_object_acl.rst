:original_name: en-us_topic_0125560460.html

.. _en-us_topic_0125560460:

PUT Object acl
==============

You can use this operation to modify an object ACL.

OBS allows you to control access permission for objects. By default, only an object creator can access the object. However, the creator can set an access policy (such as a public access policy) to grant **READ** permission for the object to other users.

You can set an access control policy when uploading an object or send **PUT Object acl** or **GET Object acl** request to modify or obtain the object ACL.

Versioning
----------

By default, this operation modifies the ACL of an object of the latest version. You can specify **versionId** to modify the ACL of an object of the desired version.

Request Syntax
--------------

.. code-block:: text

   PUT /ObjectName?acl HTTP/1.1
    User-Agent: agent
    Host: bucketname.obs.example.com
    Accept: */*
    Date: date
    Authorization: authorization
    Content-Length: length
    Expect: expect

    <AccessControlPolicy>
    <Owner>
    <ID>ID</ID>
    <DisplayName>displayname</DisplayName>
    </Owner>
    <AccessControlList>
    <Grant>
    <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="CanonicalUser">grantee</Grantee>
    <Permission>permission</Permission>
    </Grant>
    </AccessControlList>
    </AccessControlPolicy>

Request Parameters
------------------

:ref:`Table 1 <en-us_topic_0125560460__table48052128>` describes the request parameter.

.. _en-us_topic_0125560460__table48052128:

.. table:: **Table 1** Request parameter

   +-----------------------+---------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Parameter             | Description                                                                                                               | Remarks               |
   +=======================+===========================================================================================================================+=======================+
   | versionId             | Indicates the version ID of an object. The ACL of the object with the version ID specified by this parameter is modified. | Optional              |
   |                       |                                                                                                                           |                       |
   |                       | Type: String                                                                                                              |                       |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------+-----------------------+

Request Headers
---------------

This request uses common headers. For details about common request headers, see section :ref:`Common Request Headers <en-us_topic_0125560462>`.

Request Elements
----------------

This request contains elements to specify the ACL. :ref:`Table 2 <en-us_topic_0125560460__table6365150>` describes the elements.

.. _en-us_topic_0125560460__table6365150:

.. table:: **Table 2** Request elements

   +-----------------------+-----------------------------------------+-----------------------+
   | Element               | Description                             | Remarks               |
   +=======================+=========================================+=======================+
   | ID                    | DomainId of the user.                   | Optional              |
   |                       |                                         |                       |
   |                       | Type: String                            |                       |
   +-----------------------+-----------------------------------------+-----------------------+
   | DisplayName           | Indicates the user name.                | Optional              |
   |                       |                                         |                       |
   |                       | Type: String                            |                       |
   +-----------------------+-----------------------------------------+-----------------------+
   | Permission            | Indicates the permission to be granted. | Optional              |
   |                       |                                         |                       |
   |                       | Type: Enumeration                       |                       |
   +-----------------------+-----------------------------------------+-----------------------+

Response Syntax
---------------

.. code-block::

   HTTP/1.1 status_code
    Server: Server Name
    x-amz-request-id: request id
    x-amz-id-2: id
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Date: date
    Content-Length: length

Response Headers
----------------

This response uses common headers. For details about common response headers, see section :ref:`Common Response Headers <en-us_topic_0125560484>`.

This response also uses one optional header, as described in :ref:`Table 3 <en-us_topic_0125560460__table40821806>`.

.. _en-us_topic_0125560460__table40821806:

.. table:: **Table 3** Optional response header

   +-----------------------------------+---------------------------------------------------------------+
   | Header                            | Description                                                   |
   +===================================+===============================================================+
   | x-amz-version-id                  | Indicates the version ID of the object whose ACL is modified. |
   |                                   |                                                               |
   |                                   | Type: String                                                  |
   +-----------------------------------+---------------------------------------------------------------+

Response Elements
-----------------

This response involves no elements.

Error Responses
---------------

No special error responses are returned. For details about error responses, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`.

Sample Request
--------------

.. code-block:: text

   PUT /test?acl HTTP/1.1
    User-Agent: Jakarta Commons-HttpClient/3.1
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Mon, 27 Sep 2010 02:00:40 GMT
    Authorization: AWS 04RZT432N80TGDF2Y2G2:vktmLfCDhy0XbJw2T2mhNM9PZ70=
    Content-Length: 916
    Expect: 100-continue

    <AccessControlPolicy>
    <Owner>
    <ID>bcaf1ffd86f41caff1a493dc2ad8c2c281e37522a640e161ca5fb16fd081034f</ID>
    <DisplayName>user</DisplayName>
    </Owner>
    <AccessControlList>
    <Grant>
    <Grantee xsi:type="CanonicalUser" xmlns:xsi="http:// www.w3.org/2001/XMLSchema-instance">            <ID>bcaf1ffd86f41caff1a493dc2ad8c2c281e37522a640e161ca5fb16fd081034f</ID>
    <DisplayName>user</DisplayName>
    </Grantee>
    <Permission>READ</Permission>
    </Grant>
    <Grant>
    <Grantee xsi:type="CanonicalUser" xmlns:xsi="http:// www.w3.org/2001/XMLSchema-instance">            <ID>bcaf1ffd86f41caff1a493dc8c2c281e37522a640e161ca5fb16fd081034f</ID>
    <DisplayName>user</DisplayName>
    </Grantee>
    <Permission>WRITE</Permission>
    </Grant>
    </AccessControlList>
    </AccessControlPolicy>

Sample Response
---------------

.. code-block::

   HTTP/1.1 200 OK
    Server: OBS
    x-amz-request-id: 5FBCAEB7BB9A1AD0FF1285553243654
    x-amz-id-2: NUZCQ0FFQjdCQjlBMUFEMEZGMTI4NTU1MzI0MzY1NEFBQUFBQUFBYmJiYmJiYmJD
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Date: Mon, 27 Sep 2010 02:07:23 GMT
    Content-Length: 0

Sample Request (Setting the ACL of an Object with Version ID Specified)
-----------------------------------------------------------------------

.. code-block:: text

   PUT /object?acl&versionId=AAABQ47OMnbc0vycq3gAAAANVURTRkha HTTP/1.1
    User-Agent: Jakarta Commons-HttpClient/3.1
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Tue, 14 Jan 2014 05:39:29 +0000
    Authorization: AWS C9590CEB8EC051BDEC9D:PrLaB1TR7ok53Oui4jImSpWbcik=
    Content-Length: 504
    Expect: 100-continue

    <AccessControlPolicy xmlns="http://obs.example.com/doc/2015-06-30/">
    <Owner>
    <ID>DCD2FC9CAB78000001438EC051BD0002</ID>
    <DisplayName>user</DisplayName>
    </Owner>
    <AccessControlList>
    <Grant>
    <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="CanonicalUser">
    <ID>DCD2FC9CAB78000001438EC051BD0002</ID>
    <DisplayName>user</DisplayName>
    </Grantee>
    <Permission>READ</Permission>
    </Grant>
    </AccessControlList>
    </AccessControlPolicy>

Sample Response (Setting the ACL of an Object with Version ID Specified)
------------------------------------------------------------------------

.. code-block::

   HTTP/1.1 200 OK
    Server: OBS
    x-amz-request-id: 5FBCAEB7BB9A1AD0FF1285553243654
    x-amz-id-2: NUZCQ0FFQjdCQjlBMUFEMEZGMTI4NTU1MzI0MzY1NEFBQUFBQUFBYmJiYmJiYmJD
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    x-amz-version-id: AAABQ47OMnbc0vycq3gAAAANVURTRkha
    Date: Mon, 27 Sep 2010 02:07:23 GMT
    Content-Length: 0
