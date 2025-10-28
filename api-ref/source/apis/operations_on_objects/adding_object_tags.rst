:original_name: obs_04_0172.html

.. _obs_04_0172:

Adding Object Tags
==================

Functions
---------

This operation adds or updates the tag information for an object. An object tag is a key-value pair.

If you do not specify a version ID in a request, make sure that you have the **PutObjectTagging** permission. If you do specify a version ID in a request, make sure that you have the **PutObjectTagging** and **PutObjectVersionTagging** permissions. By default, only the object owner can perform this operation. The object owner can grant this permission to others by using a bucket or user policy.

Tags are added to the current version of an object by default. You can use the **versionId** parameter to add tags to any other version. If the version you are adding tags to is a delete marker, OBS returns **404 Not Found**.

.. note::

   -  Tags cannot be set for files in parallel file systems.
   -  An object can have up to 10 tags.
   -  Tag key constraints:

      -  If there are multiple tags specified for an object, each tag key must be unique.
      -  A tag key must contain 1 to 36 characters and be case sensitive.
      -  A tag key cannot start or end with a space or contain the following characters: ``,/|<>=*\``

   -  Tag value constraints:

      -  A tag value can contain 0 to 43 characters and must be case sensitive.
      -  A tag value cannot contain the following characters: ``,/|<>=*\``

Request Syntax
--------------

.. code-block:: text

   PUT /objectname?tagging&versionId=versionid HTTP/1.1
   Host: bucketname.obs.region.example.com
   Date: date
   Authorization: authorization string
   Content-MD5: md5
   <?xml version="1.0" encoding="UTF-8">
   <Tagging>
       <TagSet>
           <Tag>
               <Key>Key</Key>
               <Value>Value</Value>
           </Tag>
        </TagSet>
   </Tagging>

Request Parameters
------------------

:ref:`Table 1 <obs_04_0172__table416285709507>` describes the parameters in the request.

.. _obs_04_0172__table416285709507:

.. table:: **Table 1** Request parameters

   +-----------------------+------------------------------------------------------------------------------------------------------+-----------------------+
   | Parameter             | Description                                                                                          | Mandatory             |
   +=======================+======================================================================================================+=======================+
   | tagging               | Indicates an object tagging request.                                                                 | Yes                   |
   |                       |                                                                                                      |                       |
   |                       | Type: string                                                                                         |                       |
   +-----------------------+------------------------------------------------------------------------------------------------------+-----------------------+
   | versionId             | ID of the object version that the tag will be added to. Its response header is **x-obs-version-id**. | No                    |
   |                       |                                                                                                      |                       |
   |                       | Type: string                                                                                         |                       |
   +-----------------------+------------------------------------------------------------------------------------------------------+-----------------------+

Request Headers
---------------

:ref:`Table 2 <obs_04_0172__table1385212317506>` describes the headers in the request.

.. _obs_04_0172__table1385212317506:

.. table:: **Table 2** Request headers

   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Header                | Description                                                                                                                                                                                                                               | Mandatory             |
   +=======================+===========================================================================================================================================================================================================================================+=======================+
   | Content-MD5           | Base64-encoded 128-bit MD5 digest of the message according to RFC 1864. You can also configure the Content-SHA256 header whose value is the Base64-encoded SHA-256 digest of the message. Configure either Content-MD5 or Content-SHA256. | Yes                   |
   |                       |                                                                                                                                                                                                                                           |                       |
   |                       | Type: string                                                                                                                                                                                                                              |                       |
   |                       |                                                                                                                                                                                                                                           |                       |
   |                       | Example: **n58IG6hfM7vqI4K0vnWpog==**                                                                                                                                                                                                     |                       |
   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

Request Elements
----------------

In this request body, you need to configure the object tags in XML. :ref:`Table 3 <obs_04_0172__table1181123018399>` describes the tag elements to be configured.

.. _obs_04_0172__table1181123018399:

.. table:: **Table 3** Object tag elements

   +-----------------------+-------------------------------------------------------------------------------------------------+-----------------------+
   | Header                | Description                                                                                     | Mandatory             |
   +=======================+=================================================================================================+=======================+
   | Tagging               | Root element for TagSet and Tag                                                                 | Yes                   |
   |                       |                                                                                                 |                       |
   |                       | Type: container                                                                                 |                       |
   |                       |                                                                                                 |                       |
   |                       | Parent: none                                                                                    |                       |
   +-----------------------+-------------------------------------------------------------------------------------------------+-----------------------+
   | TagSet                | A collection for a set of tags.                                                                 | Yes                   |
   |                       |                                                                                                 |                       |
   |                       | Type: container                                                                                 |                       |
   |                       |                                                                                                 |                       |
   |                       | Parent: Tagging                                                                                 |                       |
   +-----------------------+-------------------------------------------------------------------------------------------------+-----------------------+
   | Tag                   | Information element of Tag                                                                      | Yes                   |
   |                       |                                                                                                 |                       |
   |                       | Type: container                                                                                 |                       |
   |                       |                                                                                                 |                       |
   |                       | Parent: TagSet                                                                                  |                       |
   +-----------------------+-------------------------------------------------------------------------------------------------+-----------------------+
   | Key                   | Tag name                                                                                        | Yes                   |
   |                       |                                                                                                 |                       |
   |                       | Type: string                                                                                    |                       |
   |                       |                                                                                                 |                       |
   |                       | Parent: Tag                                                                                     |                       |
   |                       |                                                                                                 |                       |
   |                       | Tag key constraints:                                                                            |                       |
   |                       |                                                                                                 |                       |
   |                       | -  If there are multiple tags specified for an object, each tag key must be unique.             |                       |
   |                       | -  A tag key must contain 1 to 36 characters and be case sensitive.                             |                       |
   |                       | -  A tag key cannot start or end with a space or contain the following characters: ``,/|<>=*\`` |                       |
   +-----------------------+-------------------------------------------------------------------------------------------------+-----------------------+
   | Value                 | Tag value                                                                                       | Yes                   |
   |                       |                                                                                                 |                       |
   |                       | Type: string                                                                                    |                       |
   |                       |                                                                                                 |                       |
   |                       | Parent: Tag                                                                                     |                       |
   |                       |                                                                                                 |                       |
   |                       | Tag value constraints:                                                                          |                       |
   |                       |                                                                                                 |                       |
   |                       | -  A tag value can contain 0 to 43 characters and must be case sensitive.                       |                       |
   |                       | -  A tag value cannot contain the following characters: ``,/|<>=*\``                            |                       |
   +-----------------------+-------------------------------------------------------------------------------------------------+-----------------------+

Response Syntax
---------------

::

   HTTP/1.1 status_code
   x-obs-request-id: request id
   x-obs-id-2: id
   Content-Length: length
   Date: date

Response Headers
----------------

This response uses common headers. For details, see :ref:`Table 1 <obs_04_0013__d0e686>`.

Response Elements
-----------------

This response contains no elements.

Error Responses
---------------

In addition to common error codes, this API also returns others. :ref:`Table 4 <obs_04_0172__table12876123320500>` lists the common errors and possible causes.

.. _obs_04_0172__table12876123320500:

.. table:: **Table 4** Error codes of object tagging

   +------------------+------------------------------------------------------------------------+------------------+
   | Error Code       | Description                                                            | HTTP Status Code |
   +==================+========================================================================+==================+
   | InvalidTag       | The provided object tag was invalid.                                   | 400              |
   +------------------+------------------------------------------------------------------------+------------------+
   | BadRequest       | The number of object tags exceeded the upper limit.                    | 400              |
   +------------------+------------------------------------------------------------------------+------------------+
   | MalformedXML     | The XML file was malformed.                                            | 400              |
   +------------------+------------------------------------------------------------------------+------------------+
   | EntityTooLarge   | The request body was too long.                                         | 400              |
   +------------------+------------------------------------------------------------------------+------------------+
   | AccessDenied     | No permission to configure object tags.                                | 403              |
   +------------------+------------------------------------------------------------------------+------------------+
   | MethodNotAllowed | Method not allowed, because the corresponding feature was not enabled. | 405              |
   +------------------+------------------------------------------------------------------------+------------------+

Sample Request
--------------

.. code-block:: text

   PUT /objectname?tagging&versionId=G001018455096CE600005306000000DD HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: Wed, 27 Jun 2018 13:22:50 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:Pf1ZyGvVYg2BzOjokZ/BAeR1mEQ=
   Content-MD5: MnAEvkfQIGnBpchOE2U6Og==
   Content-Length: 182
   <Tagging xmlns="http://obs.region.example.com/doc/2015-06-30/">
     <TagSet>
       <Tag>
         <Key>TagName1</Key>
         <Value>TagSetValue1</Value>
       </Tag>
     </TagSet>
   </Tagging>

Sample Response
---------------

::

   HTTP/1.1 200 OK
   Server: OBS
   x-obs-request-id: BF26000001643FEBA09B1ED46932CD07
   x-obs-id-2: 32AAAQAAEAABSAAgAAEAABAAAQAAEAABCSEZp87iEirC6DggPB5cN49pSvHBWClg
   Date: Wed, 27 Jun 2018 13:22:50 GMT
