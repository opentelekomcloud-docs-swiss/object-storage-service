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

This request contains no message parameters.

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

This response contains elements to detail bucket tag configuration. :ref:`Table 1 <obs_04_0050__table1181123018399>` describes the elements.

.. _obs_04_0050__table1181123018399:

.. table:: **Table 1** Bucket tag configuration elements

   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------+
   | Header                | Type                  | Description                                                                                              |
   +=======================+=======================+==========================================================================================================+
   | Tagging               | XML                   | **Definition**:                                                                                          |
   |                       |                       |                                                                                                          |
   |                       |                       | Parent element of TagSet and Tag.                                                                        |
   |                       |                       |                                                                                                          |
   |                       |                       | **Constraints**:                                                                                         |
   |                       |                       |                                                                                                          |
   |                       |                       | None                                                                                                     |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------+
   | TagSet                | XML                   | **Definition**:                                                                                          |
   |                       |                       |                                                                                                          |
   |                       |                       | Parent element of Tag. Parent: Tagging                                                                   |
   |                       |                       |                                                                                                          |
   |                       |                       | **Constraints**:                                                                                         |
   |                       |                       |                                                                                                          |
   |                       |                       | A maximum of 20 tags can be set for a bucket. That means a TagSet can contain a maximum of 20 Tag nodes. |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------+
   | Tag                   | XML                   | **Definition**:                                                                                          |
   |                       |                       |                                                                                                          |
   |                       |                       | Information element of Tag Parent: TagSet                                                                |
   |                       |                       |                                                                                                          |
   |                       |                       | **Constraints**:                                                                                         |
   |                       |                       |                                                                                                          |
   |                       |                       | A maximum of 20 tags can be set for a bucket. That means a TagSet can contain a maximum of 20 Tag nodes. |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------+
   | Key                   | String                | **Definition**:                                                                                          |
   |                       |                       |                                                                                                          |
   |                       |                       | Name of a tag. Parent: Tag                                                                               |
   |                       |                       |                                                                                                          |
   |                       |                       | **Constraints**:                                                                                         |
   |                       |                       |                                                                                                          |
   |                       |                       | -  A tag key can contain a maximum of 36 characters.                                                     |
   |                       |                       | -  A tag key cannot start or end with a space or contain the following characters: ``,/|<>=*\``          |
   |                       |                       |                                                                                                          |
   |                       |                       | **Range**:                                                                                               |
   |                       |                       |                                                                                                          |
   |                       |                       | A string between 1 and 36 characters long.                                                               |
   |                       |                       |                                                                                                          |
   |                       |                       | **Default value**:                                                                                       |
   |                       |                       |                                                                                                          |
   |                       |                       | None                                                                                                     |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------+
   | Value                 | String                | **Definition**:                                                                                          |
   |                       |                       |                                                                                                          |
   |                       |                       | Tag value. Parent: Tag                                                                                   |
   |                       |                       |                                                                                                          |
   |                       |                       | **Constraints**:                                                                                         |
   |                       |                       |                                                                                                          |
   |                       |                       | -  A tag value can contain a maximum of 43 characters.                                                   |
   |                       |                       | -  A tag value cannot contain the following characters: ``,/|<>=*\``                                     |
   |                       |                       |                                                                                                          |
   |                       |                       | **Range**:                                                                                               |
   |                       |                       |                                                                                                          |
   |                       |                       | A string of 0 (included) to 43 (excluded) characters.                                                    |
   |                       |                       |                                                                                                          |
   |                       |                       | **Default value**:                                                                                       |
   |                       |                       |                                                                                                          |
   |                       |                       | None                                                                                                     |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------+

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
         <Value>TagSetValue1</Value>
       </Tag>
     </TagSet>
   </Tagging>
