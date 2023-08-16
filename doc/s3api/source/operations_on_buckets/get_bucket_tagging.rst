:original_name: en-us_topic_0125560249.html

.. _en-us_topic_0125560249:

GET Bucket tagging
==================

This implementation of the **GET** operation uses the **tagging** subresource to return the tag set associated with the bucket. However, searching for buckets by tag is not supported.

Only users granted the **s3:GetBucketTagging** permission can perform this operation. By default, the permission is granted to the bucket owner only. However, it can be granted to other users by configuring the bucket policy.

Request Syntax
--------------

.. code-block:: text

   GET /?tagging HTTP/1.1
   User-Agent: agent
   Host: bucketname.obs.example.com
   Accept: */*
   Date: date
   Authorization: authorization string

Request Parameters
------------------

This request contains no parameter.

Request Headers
---------------

This request uses common headers. For details about common request headers, see section :ref:`Common Request Headers <en-us_topic_0125560462>`.

Request Elements
----------------

This request contains no element.

Response Syntax
---------------

.. code-block::

   HTTP/1.1 200 OK
   Server: Server Name
   x-amz-request-id: request id
   x-amz-id-2: id
   x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
   Content-Type: application/xml
   Content-Length: 0
   Date: date
   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>

   <Tagging xmlns="http://obs.example.com/doc/2015-06-30/">
       <TagSet>
           <Tag>
               <Key>TagNameJJ1</Key>
               <Value>tytttasceettt</Value>
           </Tag>
       </TagSet>
   </Tagging>

Response Headers
----------------

This response uses common headers. For details about common response headers, see section :ref:`Common Response Headers <en-us_topic_0125560484>`.

Response Elements
-----------------

This response contains elements to detail bucket lifecycle configuration. The following table describes the elements.

.. table:: **Table 1** Elements to be configured for bucket tags

   +-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Element               | Description                                                                                                                                                                                                               | Mandatory or Not      |
   +=======================+===========================================================================================================================================================================================================================+=======================+
   | Tagging               | Container for the **TagSet** and **Tag** elements                                                                                                                                                                         | Yes                   |
   |                       |                                                                                                                                                                                                                           |                       |
   |                       | Type: Container                                                                                                                                                                                                           |                       |
   |                       |                                                                                                                                                                                                                           |                       |
   |                       | Ancestor: None                                                                                                                                                                                                            |                       |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | TagSet                | Container for a set of tags                                                                                                                                                                                               | Yes                   |
   |                       |                                                                                                                                                                                                                           |                       |
   |                       | Type: Container                                                                                                                                                                                                           |                       |
   |                       |                                                                                                                                                                                                                           |                       |
   |                       | Ancestor: Tagging                                                                                                                                                                                                         |                       |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Tag                   | Container for tag information                                                                                                                                                                                             | Yes                   |
   |                       |                                                                                                                                                                                                                           |                       |
   |                       | Type: Container. Each bucket supports a maximum of 20 tags.                                                                                                                                                               |                       |
   |                       |                                                                                                                                                                                                                           |                       |
   |                       | Ancestor: TagSet                                                                                                                                                                                                          |                       |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Key                   | Name of the tag                                                                                                                                                                                                           | Yes                   |
   |                       |                                                                                                                                                                                                                           |                       |
   |                       | Type: String. It can contain a maximum of 36 characters, including A to Z, a to z, 0 to 9, hyphens (-), underscores (_), and Unicode(\\u4E00-\\u9FFF). In the same bucket, the key of a tag must be unique.               |                       |
   |                       |                                                                                                                                                                                                                           |                       |
   |                       | Ancestor: Tag                                                                                                                                                                                                             |                       |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Value                 | Value of the tag                                                                                                                                                                                                          | Yes                   |
   |                       |                                                                                                                                                                                                                           |                       |
   |                       | Type: String. It can contain a maximum of 43 characters, including A to Z, a to z, 0 to 9, hyphens (-), underscores (_), periods (.), and Unicode(\\u4E00-\\u9FFF). Note that periods (.) can be used for this parameter. |                       |
   |                       |                                                                                                                                                                                                                           |                       |
   |                       | Ancestor: Tag                                                                                                                                                                                                             |                       |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

Error Responses
---------------

Except for common error responses, special error responses are also returned. The following table lists error responses and possible causes.

.. table:: **Table 2** Error responses and possible causes

   +--------------+----------------------------------------------------+------------------+
   | Error Code   | Possible Cause                                     | HTTP Status Code |
   +==============+====================================================+==================+
   | NoSuchTagSet | The specified bucket is not configured with a tag. | 404 Not Found    |
   +--------------+----------------------------------------------------+------------------+

Sample Request
--------------

.. code-block:: text

   GET /?tagging HTTP/1.1
   User-Agent: curl/7.19.7 (x86_64-suse-linux-gnu) libcurl/7.19.7 OpenSSL/0.9.8j zlib/1.2.7 libidn/1.10
   Host: bucketname.obs.example.com
   Accept: */*
   Date: Tue, 09 May 2017 03:17:07 +0000
   Authorization: authorization string

Sample Response
---------------

.. code-block::

   HTTP/1.1 200 OK
   Server: OBS
   x-amz-request-id: 0002B7532E0000015BEB35330C5884X1
   x-amz-id-2: s12w20LYNQqSb7moq4ibgJwmQRSmVQV+rFBqplOGYkXUpXeS/nOmbkyD+E35K79j
   x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
   Content-Type: application/xml
   Date: Tue, 09 May 2017 03:16:23 GMT
   Content-Length: 441
   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <Tagging xmlns="http://obs.example.com/doc/2015-06-30/">
       <TagSet>
           <Tag>
               <Key>TagNameJJ1</Key>
               <Value>tytttasceettt</Value>
           </Tag>
       </TagSet>
   </Tagging>
