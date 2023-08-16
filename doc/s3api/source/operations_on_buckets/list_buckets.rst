:original_name: en-us_topic_0125560308.html

.. _en-us_topic_0125560308:

List Buckets
============

You can obtain the list of created buckets.

Request Syntax
--------------

.. code-block:: text

   GET / HTTP/1.1
   User-Agent: agent
   Host: obs.example.com
   Accept: */*
   Date: date
   Authorization: authorization

Request Parameters
------------------

This request involves no parameters.

Request Headers
---------------

The operation request header is the same as that of a common request. For details, see section :ref:`Common Request Headers <en-us_topic_0125560462>`.

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
   x-amz-id-2: id2
   Content-Type: type
   Date: date
   Content-Length: length

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <ListAllMyBucketsResult xmlns="http://obs.example.com/doc/2015-06-30/">
       <Owner>
           <ID>id</ID>
           <DisplayName>name</DisplayName>
       </Owner>
       <Buckets>
           <Bucket>
               <Name>bucketName</Name>
               <CreationDate>date</CreationDate>
               <BucketType>buckettype</BucketType>
           </Bucket>
           ...
       </Buckets>
   </ListAllMyBucketsResult>

Response Headers
----------------

This response uses common headers. For details about common response headers, see section :ref:`Common Response Headers <en-us_topic_0125560484>`.

Response Elements
-----------------

This response contains a bucket list in the XML format. :ref:`Table 1 <en-us_topic_0125560308__table12491043>` describes the elements in this response.

.. _en-us_topic_0125560308__table12491043:

.. table:: **Table 1** Response elements

   +-----------------------------------+------------------------------------------------------------------------------------------------+
   | Element                           | Description                                                                                    |
   +===================================+================================================================================================+
   | ListAllMyBucketsResult            | Indicates the bucket list.                                                                     |
   |                                   |                                                                                                |
   |                                   | Type: XML                                                                                      |
   +-----------------------------------+------------------------------------------------------------------------------------------------+
   | Owner                             | Indicates the user information such as the user ID and user name or domain ID and domain name. |
   |                                   |                                                                                                |
   |                                   | Type: XML                                                                                      |
   +-----------------------------------+------------------------------------------------------------------------------------------------+
   | ID                                | Indicates the user ID or Domain ID.                                                            |
   |                                   |                                                                                                |
   |                                   | Type: String                                                                                   |
   +-----------------------------------+------------------------------------------------------------------------------------------------+
   | DisplayName                       | Indicates the user name.                                                                       |
   |                                   |                                                                                                |
   |                                   | Type: String                                                                                   |
   +-----------------------------------+------------------------------------------------------------------------------------------------+
   | Buckets                           | Indicates the buckets that a user owns.                                                        |
   |                                   |                                                                                                |
   |                                   | Type: XML                                                                                      |
   +-----------------------------------+------------------------------------------------------------------------------------------------+
   | Bucket                            | Indicates details about a bucket.                                                              |
   |                                   |                                                                                                |
   |                                   | Type: XML                                                                                      |
   +-----------------------------------+------------------------------------------------------------------------------------------------+
   | Name                              | Indicates the bucket name.                                                                     |
   |                                   |                                                                                                |
   |                                   | Type: String                                                                                   |
   +-----------------------------------+------------------------------------------------------------------------------------------------+
   | CreationDate                      | Indicates the date on which a bucket was created.                                              |
   |                                   |                                                                                                |
   |                                   | Type: String                                                                                   |
   +-----------------------------------+------------------------------------------------------------------------------------------------+
   | BucketType                        | Indicates the bucket type.                                                                     |
   |                                   |                                                                                                |
   |                                   | Type: String                                                                                   |
   |                                   |                                                                                                |
   |                                   | Value:                                                                                         |
   |                                   |                                                                                                |
   |                                   | -  OBJECT: indicates an object bucket.                                                         |
   +-----------------------------------+------------------------------------------------------------------------------------------------+

Error Responses
---------------

No special error responses are returned. For details about error responses, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`.

Sample Request
--------------

.. code-block:: text

   GET / HTTP/1.1
   User-Agent: Jakarta Commons-HttpClient/3.1
   Host: obs.example.com
   Accept: */*
   Date: Sun, 26 Sep 2010 08:24:46 GMT
   Authorization: AWS 04RZT432N80TGDF2Y2G2:ZyEGq367GyGGyItzr5egJOjaqiM=

Sample Response
---------------

.. code-block::

   HTTP/1.1 200 OK
   Server: OBS
   x-amz-request-id: 9D3CC717E561E4D37A1285489689346
   x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
   x-amz-id-2: OUQzQ0M3MTdFNTYxRTREMzdBMTI4NTQ4OTY4OTM0NkFBQUFBQUFBYmJiYmJiYmJD
   Content-Type: application/xml
   Date: Sun, 26 Sep 2010 08:28:06 GMT
   Content-Length: 485

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <ListAllMyBucketsResult xmlns="http://obs.example.com/doc/2015-06-30/">
       <Owner>
           <ID>bcaf1ffd86f41caff1a493dc2ad8c2c281e37522a640e161ca5fb16fd081034f</ID>
           <DisplayName>user01</DisplayName>
       </Owner>
       <Buckets>
           <Bucket>
               <Name>bucket01</Name>
               <CreationDate>2010-09-26T03:10:23.211Z</CreationDate>
               <BucketType>OBJECT</BucketType>
           </Bucket>
           <Bucket>
               <Name>bucket02</Name>
               <CreationDate>2010-09-20T12:05:46.187Z</CreationDate>
               <BucketType>OBJECT</BucketType>
           </Bucket>
           <Bucket>
               <Name>bucket03</Name>
               <CreationDate>2010-09-26T08:25:13.059Z</CreationDate>
               <BucketType>OBJECT</BucketType>
           </Bucket>
       </Buckets>
   </ListAllMyBucketsResult>
