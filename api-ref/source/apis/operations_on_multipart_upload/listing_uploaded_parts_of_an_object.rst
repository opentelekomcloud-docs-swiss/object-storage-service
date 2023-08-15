:original_name: obs_04_0101.html

.. _obs_04_0101:

Listing Uploaded Parts of an Object
===================================

Functions
---------

You can perform this operation to query all parts associated to a multipart upload. The size of each part listed by this API is the same as the size of the part uploaded.

Request Syntax
--------------

.. code-block:: text

   GET /ObjectName?uploadId=uploadid&max-parts=max&part-number-marker=marker HTTP/1.1
   Host: bucketname.obs.region.example.com
   Date: date
   Authorization: auth

Request Parameters
------------------

This request uses parameters to specify which parts in a multipart upload will be listed. :ref:`Table 1 <obs_04_0101__table43496416>` describes the parameters.

.. _obs_04_0101__table43496416:

.. table:: **Table 1** Request parameters

   +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Parameter             | Description                                                                                                                              | Mandatory             |
   +=======================+==========================================================================================================================================+=======================+
   | uploadId              | Indicates a multipart upload ID.                                                                                                         | Yes                   |
   |                       |                                                                                                                                          |                       |
   |                       | Type: string                                                                                                                             |                       |
   |                       |                                                                                                                                          |                       |
   |                       | Default value: none                                                                                                                      |                       |
   +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | max-parts             | Specifies the maximum number of parts to be listed.                                                                                      | No                    |
   |                       |                                                                                                                                          |                       |
   |                       | Type: string                                                                                                                             |                       |
   |                       |                                                                                                                                          |                       |
   |                       | Default value: 1000.                                                                                                                     |                       |
   +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | part-number           | Indicates the part after which the part listing begins. OBS lists only parts with greater numbers than that specified by this parameter. | No                    |
   |                       |                                                                                                                                          |                       |
   | -marker               | Type: string                                                                                                                             |                       |
   |                       |                                                                                                                                          |                       |
   |                       | Default value: none                                                                                                                      |                       |
   +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

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
   Date: date
   Content-Length: length

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <ListPartsResult xmlns="http://obs.region.example.com/doc/2015-06-30/">
       <Bucket>BucketName</Bucket>
       <Key>object</Key>
       <UploadId>uploadid</UploadId>
       <Initiator>
           <ID>id</ID>
       </Initiator>
       <Owner>
           <ID>ownerid</ID>
       </Owner>
       <PartNumberMarker>partNmebermarker</PartNumberMarker>
       <NextPartNumberMarker>nextPartnumberMarker</NextPartNumberMarker>
       <MaxParts>maxParts</MaxParts>
       <IsTruncated>true</IsTruncated>
       <Part>
           <PartNumber>partNumber</PartNumber>
           <LastModified>modifiedDate</LastModified>
           <ETag>etag</ETag>
           <Size>size</Size>
       </Part>
   </ListPartsResult>

Response Headers
----------------

The response to the request uses common headers. For details, see :ref:`Table 1 <obs_04_0013__d0e686>`.

Response Elements
-----------------

This response uses elements to return information about uploaded parts. :ref:`Table 2 <obs_04_0101__table33229135>` describes the elements.

.. _obs_04_0101__table33229135:

.. table:: **Table 2** Response elements

   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Element                           | Description                                                                                                                                                              |
   +===================================+==========================================================================================================================================================================+
   | ListPartsResult                   | Indicates the container for responses to List Parts requests.                                                                                                            |
   |                                   |                                                                                                                                                                          |
   |                                   | Type: container                                                                                                                                                          |
   |                                   |                                                                                                                                                                          |
   |                                   | Children: Bucket, Key, UploadId, PartNumberMarker, NextPartNumberMarker, MaxParts, IsTruncated, Part                                                                     |
   |                                   |                                                                                                                                                                          |
   |                                   | Ancestor: none                                                                                                                                                           |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Bucket                            | Indicates a bucket name.                                                                                                                                                 |
   |                                   |                                                                                                                                                                          |
   |                                   | Type: string                                                                                                                                                             |
   |                                   |                                                                                                                                                                          |
   |                                   | Ancestor: ListPartsResult                                                                                                                                                |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Key                               | Indicates an object name.                                                                                                                                                |
   |                                   |                                                                                                                                                                          |
   |                                   | Type: string                                                                                                                                                             |
   |                                   |                                                                                                                                                                          |
   |                                   | Ancestor: ListPartsResult                                                                                                                                                |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | UploadId                          | Indicates the ID of a multipart upload.                                                                                                                                  |
   |                                   |                                                                                                                                                                          |
   |                                   | Type: string                                                                                                                                                             |
   |                                   |                                                                                                                                                                          |
   |                                   | Ancestor: ListPartsResult                                                                                                                                                |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Initiator                         | Indicates the initiator of a multipart upload.                                                                                                                           |
   |                                   |                                                                                                                                                                          |
   |                                   | Type: container                                                                                                                                                          |
   |                                   |                                                                                                                                                                          |
   |                                   | Indicates the subnode ID.                                                                                                                                                |
   |                                   |                                                                                                                                                                          |
   |                                   | Ancestor: ListPartsResult                                                                                                                                                |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Owner                             | The value of this parameter is the same as that of **Initiator**.                                                                                                        |
   |                                   |                                                                                                                                                                          |
   |                                   | Type: container                                                                                                                                                          |
   |                                   |                                                                                                                                                                          |
   |                                   | Children: ID                                                                                                                                                             |
   |                                   |                                                                                                                                                                          |
   |                                   | Ancestor: ListPartsResult                                                                                                                                                |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ID                                | ID of the domain to which the owner belongs                                                                                                                              |
   |                                   |                                                                                                                                                                          |
   |                                   | Type: string                                                                                                                                                             |
   |                                   |                                                                                                                                                                          |
   |                                   | Ancestor: Initiator or Owner                                                                                                                                             |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | PartNumberMarker                  | Part number after which listing parts begins.                                                                                                                            |
   |                                   |                                                                                                                                                                          |
   |                                   | Type: integer                                                                                                                                                            |
   |                                   |                                                                                                                                                                          |
   |                                   | Ancestor: ListPartsResult                                                                                                                                                |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | NextPartNumberMarker              | Indicates the value of **PartNumberMarker** in the next request when the returned result is incomplete.                                                                  |
   |                                   |                                                                                                                                                                          |
   |                                   | Type: integer                                                                                                                                                            |
   |                                   |                                                                                                                                                                          |
   |                                   | Ancestor: ListPartsResult                                                                                                                                                |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | MaxParts                          | Maximum number of parts returned in a response                                                                                                                           |
   |                                   |                                                                                                                                                                          |
   |                                   | Type: integer                                                                                                                                                            |
   |                                   |                                                                                                                                                                          |
   |                                   | Ancestor: ListPartsResult                                                                                                                                                |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | IsTruncated                       | Indicates whether the returned part list is truncated. The value **true** indicates that the list was truncated and **false** indicates that the list was not truncated. |
   |                                   |                                                                                                                                                                          |
   |                                   | Type: boolean                                                                                                                                                            |
   |                                   |                                                                                                                                                                          |
   |                                   | Ancestor: **ListPartsResult**                                                                                                                                            |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Part                              | Indicates the container for elements related to a particular part.                                                                                                       |
   |                                   |                                                                                                                                                                          |
   |                                   | Type: string                                                                                                                                                             |
   |                                   |                                                                                                                                                                          |
   |                                   | Children: PartNumber, LastModified, ETag, Size                                                                                                                           |
   |                                   |                                                                                                                                                                          |
   |                                   | Ancestor: ListPartsResult                                                                                                                                                |
   |                                   |                                                                                                                                                                          |
   |                                   | **PartNumber** identifies a part.                                                                                                                                        |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | PartNumber                        | Number of an uploaded part                                                                                                                                               |
   |                                   |                                                                                                                                                                          |
   |                                   | Type: integer                                                                                                                                                            |
   |                                   |                                                                                                                                                                          |
   |                                   | Ancestor: ListPartsResult.Part                                                                                                                                           |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | LastModified                      | Indicates the date and time a part was uploaded.                                                                                                                         |
   |                                   |                                                                                                                                                                          |
   |                                   | Type: date                                                                                                                                                               |
   |                                   |                                                                                                                                                                          |
   |                                   | Ancestor: ListPartsResult.Part                                                                                                                                           |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ETag                              | ETag value of the uploaded parts. It is the unique identifier of the part content and is used to verify data consistency during the combination of parts.                |
   |                                   |                                                                                                                                                                          |
   |                                   | Type: string                                                                                                                                                             |
   |                                   |                                                                                                                                                                          |
   |                                   | Ancestor: ListPartsResult.Part                                                                                                                                           |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Size                              | Indicates the size of an uploaded part.                                                                                                                                  |
   |                                   |                                                                                                                                                                          |
   |                                   | Type: integer                                                                                                                                                            |
   |                                   |                                                                                                                                                                          |
   |                                   | Ancestor: ListPartsResult.Part                                                                                                                                           |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Error Responses
---------------

#. If the AK or signature is invalid, OBS returns **403 Forbidden** and the error code is **AccessDenied**.
#. If the requested bucket does not exist, OBS returns **404 Forbidden** and the error code is **NoSuchBucket**.
#. If the requested multipart upload task does not exist, OBS returns **404 Not Found** and the error code is **NoSuchUpload**.
#. OBS determines whether the use's domain ID has the read permission for the specified bucket. If the user does not have the permission, OBS returns **403 Forbidden** and the error code is **AccessDenied**.

For other errors, see :ref:`Table 2 <obs_04_0115__d0e843>`.

Sample Request
--------------

.. code-block:: text

   GET /object02?uploadId=00000163D40171ED8DF4050919BD02B8 HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: WED, 01 Jul 2015 05:20:35 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:xkABdSrBPrz5yqzuZdJnK5oL/yU=

Sample Response
---------------

::

   HTTP/1.1 200 OK
   Server: OBS
   x-obs-request-id: 8DF400000163D40C099A04EF4DD1BDD9
   x-obs-id-2: 32AAAQAAEAABAAAQAAEAABAAAQAAEAABCSK71fr+hDnzB0JBvQC1B9+S12AWxC41
   Content-Type: application/xml
   Date: WED, 01 Jul 2015 05:20:35 GMT
   Content-Length: 888

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <ListPartsResult xmlns="http://obs.example.com/doc/2015-06-30/">
     <Bucket>test333</Bucket>
     <Key>obj2</Key>
     <UploadId>00000163D40171ED8DF4050919BD02B8</UploadId>
     <Initiator>
       <ID>domainID/domainiddomainiddomainiddo000008:userID/useriduseriduseriduseridus000008</ID>
     </Initiator>
     <Owner>
       <ID>domainiddomainiddomainiddo000008</ID>
     </Owner>
     <PartNumberMarker>0</PartNumberMarker>
     <NextPartNumberMarker>2</NextPartNumberMarker>
     <MaxParts>1000</MaxParts>
     <IsTruncated>false</IsTruncated>
     <Part>
       <PartNumber>1</PartNumber>
       <LastModified>2018-06-06T07:39:32.522Z</LastModified>
       <ETag>"b026324c6904b2a9cb4b88d6d61c81d1"</ETag>
       <Size>2058462721</Size>
     </Part>
     <Part>
       <PartNumber>2</PartNumber>
       <LastModified>2018-06-06T07:41:03.344Z</LastModified>
       <ETag>"3b46eaf02d3b6b1206078bb86a7b7013"</ETag>
       <Size>4572</Size>
     </Part>
   </ListPartsResult>
