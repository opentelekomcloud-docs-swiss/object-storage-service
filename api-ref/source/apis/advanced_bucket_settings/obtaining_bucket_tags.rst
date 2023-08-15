:original_name: obs_04_0050.html

.. _obs_04_0050:

Obtaining Bucket Tags
=====================

Functions
---------

This operation obtains information about tags of a bucket.

To perform this operation, you must have the **GetBucketTagging** permission. By default, only the bucket owner can obtain the tags of a bucket. The bucket owner can allow other users to perform this operation by setting a bucket policy or granting them the permission.

Request Syntax
--------------

.. code-block:: text

   GET /?tagging HTTP/1.1
   Host: bucketname.obs.region.example.com
   Date: date
   Authorization: authorization string

Request Parameters
------------------

This request contains no parameter.

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
   x-obs-request-id: request id
   x-obs-id-2: id
   Content-Type: application/xml
   Content-Length: length
   Date: date
   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <Tagging xmlns="http://obs.example.com/doc/2015-06-30/">
       <TagSet>
           <Tag>
               <Key>key</Key>
               <Value>value</Value>
           </Tag>
       </TagSet>
   </Tagging>

Response Headers
----------------

The response to the request uses common headers. For details, see :ref:`Table 1 <obs_04_0013__d0e686>`.

Response Elements
-----------------

This response contains elements to detail bucket tag configuration. :ref:`Table 1 <obs_04_0050__table1881863118318>` describes the elements.

.. _obs_04_0050__table1881863118318:

.. table:: **Table 1** Elements for configuring bucket tags

   +-----------------------------------+-----------------------------------+
   | Element                           | Description                       |
   +===================================+===================================+
   | Tagging                           | Element of the tag set and tag.   |
   |                                   |                                   |
   |                                   | Type: element                     |
   |                                   |                                   |
   |                                   | Ancestor: none                    |
   +-----------------------------------+-----------------------------------+
   | TagSet                            | Element of the tag set.           |
   |                                   |                                   |
   |                                   | Type: element                     |
   |                                   |                                   |
   |                                   | Ancestor: Tagging                 |
   +-----------------------------------+-----------------------------------+
   | Tag                               | Element of the tag information.   |
   |                                   |                                   |
   |                                   | Type: element                     |
   |                                   |                                   |
   |                                   | Ancestor: TagSet                  |
   +-----------------------------------+-----------------------------------+
   | Key                               | Tag name.                         |
   |                                   |                                   |
   |                                   | Type: string                      |
   |                                   |                                   |
   |                                   | Ancestor: Tag                     |
   +-----------------------------------+-----------------------------------+
   | Value                             | Tag value.                        |
   |                                   |                                   |
   |                                   | Type: string                      |
   |                                   |                                   |
   |                                   | Ancestor: Tag                     |
   +-----------------------------------+-----------------------------------+

Error Responses
---------------

In addition to common error codes, this API also returns other error codes. The following table lists common errors and possible causes. For details, see :ref:`Table 2 <obs_04_0050__table1488314173514>`.

.. _obs_04_0050__table1488314173514:

.. table:: **Table 2** Bucket tag configuration errors

   +--------------+----------------------------------------------+------------------+
   | Error Code   | Description                                  | HTTP Status Code |
   +==============+==============================================+==================+
   | NoSuchTagSet | The specified bucket does not have any tags. | 404 Not Found    |
   +--------------+----------------------------------------------+------------------+

Sample Request
--------------

.. code-block:: text

   GET /?tagging HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: Wed, 27 Jun 2018 13:25:44 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:H1INcyc5i0XlHqYTfuzkPxLZUPM=

Sample Response
---------------

::

   HTTP/1.1 200 OK
   x-obs-request-id: 0002B7532E0000015BEB35330C5884X1
   x-obs-id-2: s12w20LYNQqSb7moq4ibgJwmQRSmVQV+rFBqplOGYkXUpXeS/nOmbkyD+E35K79j
   Content-Type: application/xml
   Date: Wed, 27 Jun 2018 13:25:44 GMT
   Content-Length: 441

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <Tagging xmlns="http://obs.example.com/doc/2015-06-30/">
     <TagSet>
       <Tag>
         <Key>TagName1</Key>
         <Value>TageSetVaule1</Value>
       </Tag>
     </TagSet>
   </Tagging>
