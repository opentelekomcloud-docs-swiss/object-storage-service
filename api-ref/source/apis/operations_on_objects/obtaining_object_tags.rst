:original_name: obs_04_0164.html

.. _obs_04_0164:

Obtaining Object Tags
=====================

Functions
---------

This operation returns tags of an object.

If you do not specify a version ID in a request, make sure that you have the **GetObjectTagging** permission. If you do specify a version ID in a request, make sure that you have the **GetObjectTagging** and **GetObjectVersionTagging** permissions. By default, only the object owner can perform this operation. The object owner can grant this permission to others by using a bucket or user policy.

OBS returns the tags of the current object version by default. You can use the **versionId** parameter to retrieve tags of any other version. If the version you are retrieving tags from is a delete marker, OBS returns **404 Not Found**.

.. note::

   Tags are not supported for files in parallel file systems.

Request Syntax
--------------

.. code-block:: text

   GET /objectname?tagging&versionId=versionid HTTP/1.1
   Host: bucketname.obs.region.example.com
   Date: date
   Authorization: authorization string

Request Parameters
------------------

:ref:`Table 1 <obs_04_0164__table416285709507>` describes the parameters in the request.

.. _obs_04_0164__table416285709507:

.. table:: **Table 1** Request parameters

   +-----------------------+---------------------------------------------------------------------------------------------+-----------------------+
   | Parameter             | Description                                                                                 | Mandatory (Yes/No)    |
   +=======================+=============================================================================================+=======================+
   | tagging               | Indicates an object tag request.                                                            | Yes                   |
   |                       |                                                                                             |                       |
   |                       | Type: string                                                                                |                       |
   +-----------------------+---------------------------------------------------------------------------------------------+-----------------------+
   | versionId             | ID of the tagged object version. Its corresponding response header is **x-obs-version-id**. | No                    |
   |                       |                                                                                             |                       |
   |                       | Type: string                                                                                |                       |
   +-----------------------+---------------------------------------------------------------------------------------------+-----------------------+

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
   x-obs-version-id: version id
   Content-Type: application/xml
   Content-Length: length
   Date: date
   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <Tagging xmlns="http://obs.region.example.com/doc/2015-06-30/">
       <TagSet>
           <Tag>
               <Key>key</Key>
               <Value>value</Value>
           </Tag>
       </TagSet>
   </Tagging>

Response Headers
----------------

This response uses common headers. For details, see :ref:`Table 1 <obs_04_0013__d0e686>`.

Response Elements
-----------------

For more information about the object tag elements returned in the response, see :ref:`Table 3 <obs_04_0172__table1181123018399>`.

Error Responses
---------------

In addition to common error codes, this API also returns others. :ref:`Table 2 <obs_04_0164__table1488314173514>` lists the common errors and possible causes.

.. _obs_04_0164__table1488314173514:

.. table:: **Table 2** Error codes of obtaining object tags

   +--------------+---------------------------------------------------+------------------+
   | Error Code   | Description                                       | HTTP Status Code |
   +==============+===================================================+==================+
   | NoSuchTagSet | No tags were configured for the specified object. | 404              |
   +--------------+---------------------------------------------------+------------------+

Sample Request
--------------

.. code-block:: text

   GET /objectname?tagging&versionId=G001018455096CE600005306000000DD HTTP/1.1
   User-Agent: curl/7.29.0
   Host: bucketname.obs.region.example.com
   Accept: */*
   Date: Wed, 27 Jun 2018 13:25:44 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:H1INcyc5i0XlHqYTfuzkPxLZUPM=

Sample Response
---------------

::

   HTTP/1.1 200 OK
   x-obs-request-id: 0002B7532E0000015BEB35330C5884X1
   x-obs-id-2: s12w20LYNQqSb7moq4ibgJwmQRSmVQV+rFBqplOGYkXUpXeS/nOmbkyD+E35K79j
   x-obs-version-id: G001018455096CE600005306000000DD
   Content-Type: application/xml
   Date: Wed, 27 Jun 2018 13:25:44 GMT
   Content-Length: 441

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <Tagging xmlns="http://obs.region.example.com/doc/2015-06-30/">
     <TagSet>
       <Tag>
         <Key>TagName1</Key>
         <Value>TagSetValue1</Value>
       </Tag>
     </TagSet>
   </Tagging>
