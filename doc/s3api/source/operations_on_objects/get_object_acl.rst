:original_name: en-us_topic_0125560291.html

.. _en-us_topic_0125560291:

GET Object acl
==============

You can use this operation to view the ACL of an object, as long as you have **READ_ACP** permission for the object.

Versioning
----------

By default, the ACL of the object of the latest version is obtained. If the version ID of the object is a deletion mark, **404** is returned. You can specify **versionId** to obtain the ACL of an object of the desired version.

Request Syntax
--------------

.. code-block:: text

   GET /ObjectName?acl HTTP/1.1
    User-Agent: agent
    Host: bucketname.obs.example.com
    Accept: */*
    Date: date
    Authorization: authorization

Request Parameters
------------------

This request uses parameters to specify the object ACL to be obtained. :ref:`Table 1 <en-us_topic_0125560291__table22962068>` describes the parameters.

.. _en-us_topic_0125560291__table22962068:

.. table:: **Table 1** Request parameter

   +-----------------------+---------------------------------------------------+-----------------------+
   | Parameter             | Description                                       | Remarks               |
   +=======================+===================================================+=======================+
   | acl                   | Indicates that the object ACL to be obtained.     | Mandatory             |
   |                       |                                                   |                       |
   |                       | Type: String                                      |                       |
   +-----------------------+---------------------------------------------------+-----------------------+
   | versionId             | Indicates the version ID of the specified object. | Optional              |
   |                       |                                                   |                       |
   |                       | Type: String                                      |                       |
   +-----------------------+---------------------------------------------------+-----------------------+

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
    Server: bucketname.obs.example.com
    x-amz-request-id: request id
    x-amz-id-2: id
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Date: date
    Content-Length: length
    Content-Type: type

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

This response also uses one optional header, as described in :ref:`Table 2 <en-us_topic_0125560291__table14642465>`.

.. _en-us_topic_0125560291__table14642465:

.. table:: **Table 2** Optional response header

   +-----------------------------------+---------------------------------------------------+
   | Header                            | Description                                       |
   +===================================+===================================================+
   | x-amz-version-id                  | Indicates the version ID of the specified object. |
   |                                   |                                                   |
   |                                   | Valid values: String                              |
   |                                   |                                                   |
   |                                   | Default: None                                     |
   +-----------------------------------+---------------------------------------------------+

Response Elements
-----------------

This response contains elements to specify the returned object ACL. :ref:`Table 3 <en-us_topic_0125560291__table23161487>` describes the elements.

.. _en-us_topic_0125560291__table23161487:

.. table:: **Table 3** Response elements

   +-----------------------------------+------------------------------------------------------------------------------------+
   | Element                           | Description                                                                        |
   +===================================+====================================================================================+
   | DisplayName                       | Indicates the user name.                                                           |
   |                                   |                                                                                    |
   |                                   | Type: String                                                                       |
   +-----------------------------------+------------------------------------------------------------------------------------+
   | ID                                | DomainId of the user.                                                              |
   |                                   |                                                                                    |
   |                                   | Type: String                                                                       |
   +-----------------------------------+------------------------------------------------------------------------------------+
   | AccessControlList                 | Indicates the ACL that records all users who have permission to access the bucket. |
   |                                   |                                                                                    |
   |                                   | Type: XML                                                                          |
   +-----------------------------------+------------------------------------------------------------------------------------+
   | Grant                             | Container for the grantee and its permission.                                      |
   |                                   |                                                                                    |
   |                                   | Type: XML                                                                          |
   +-----------------------------------+------------------------------------------------------------------------------------+
   | Grantee                           | Container for the details about the grantee.                                       |
   |                                   |                                                                                    |
   |                                   | Type: XML                                                                          |
   +-----------------------------------+------------------------------------------------------------------------------------+
   | Permission                        | Indicates the grantee's permission for an object.                                  |
   |                                   |                                                                                    |
   |                                   | Type: String                                                                       |
   +-----------------------------------+------------------------------------------------------------------------------------+

Error Responses
---------------

No special error responses are returned. For details about error responses, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`.

Sample Request
--------------

.. code-block:: text

   GET /test?acl HTTP/1.1
    User-Agent: Jakarta Commons-HttpClient/3.1
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Mon, 27 Sep 2010 01:51:25 GMT
    Authorization:  AWS 04RZT432N80TGDF2Y2G2:pkRtbbpzetVSUoTralXIkRLWsCQ=

Sample Response
---------------

.. code-block::

   HTTP/1.1 200 OK
    Server: OBS
    x-amz-request-id: 5FBCAEB7BB9A1AD0FF1285552415340
    x-amz-id-2: NUZCQ0FFQjdCQjlBMUFEMEZGMTI4NTU1MjQxNTM0MEFBQUFBQUFBYmJiYmJiYmJD
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Content-Type: application/xml
    Date: Mon, 27 Sep 2010 01:53:35 GMT
    Content-Length: 560

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <AccessControlPolicy xmlns="http://obs.example.com/doc/2015-06-30/">
    <Owner>
    <ID>bcaf1ffd86f41caff1a493dc2ad8c2c281e37522a640e161ca5fb16fd081034f</ID>
    <DisplayName>apple</DisplayName>
    </Owner>
    <AccessControlList>
    <Grant>
    <Grantee xmlns:xsi="http:// www.w3.org/2001/XMLSchema-instance" xsi:type="CanonicalUser">            <ID>bcaf1ffd86f41caff1a493dc2ad8c2c281e37522a640e161ca5fb16fd081034f</ID>
    <DisplayName>apple</DisplayName>
    </Grantee>
    <Permission>FULL_CONTROL</Permission>
    </Grant>
    </AccessControlList>
    </AccessControlPolicy>

Sample Request (Getting the ACL of an Object with Version ID Specified)
-----------------------------------------------------------------------

.. code-block:: text

   GET /object?acl&versionId=AAABQ4-glIvc0vycq3gAAAAVVURTRkha HTTP/1.1
    User-Agent: Jakarta Commons-HttpClient/3.1
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Tue, 14 Jan 2014 07:32:21 +0000
    Authorization: AWS C9590CEB8EC051BDEC9D:IsCyQSOY8rbyp8E6W/ftU6GFcGg=

Sample Response (Getting the ACL of an Object with Version ID Specified)
------------------------------------------------------------------------

.. code-block::

   HTTP/1.1 200 OK
    Server: OBS
    x-amz-request-id: DCD2FC9CAB78000001438FAA5667BFF4
    x-amz-id-2: 5R2cHP9X7aa+ukdrBQEVgW688/0yEpB+0wgUE7J3QdBLAi9NmHAfeCudmlwgxhk4
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Content-Type: application/xml
    x-amz-version-id: AAABQ4-glIvc0vycq3gAAAAVVURTRkha
    Date: Tue, 14 Jan 2014 07:32:21 GMT
    Content-Length: 494
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
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
    <Permission>FULL_CONTROL</Permission>
    </Grant>
    </AccessControlList>
    </AccessControlPolicy>
