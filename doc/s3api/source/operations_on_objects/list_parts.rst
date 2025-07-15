:original_name: en-us_topic_0125560266.html

.. _en-us_topic_0125560266:

List Parts
==========

You can use this operation to query all parts associated to a multipart upload.

Request Syntax
--------------

.. code-block:: text

   GET /ObjectName?uploadId=uploadid&max-parts=max&part-number-marker=marker HTTP/1.1
    User-Agent: agent
    Host: bucketname.obs.example.com
    Accept: */*
    Date: date
    Authorization: auth

Request Parameters
------------------

This request uses parameters to specify associated parts to be listed. :ref:`Table 1 <en-us_topic_0125560266__table43496416>` describes the parameters.

.. _en-us_topic_0125560266__table43496416:

.. table:: **Table 1** Request parameters

   +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Parameter             | Description                                                                                                                                  | Remarks               |
   +=======================+==============================================================================================================================================+=======================+
   | uploadId              | Indicates the ID of the multipart upload whose parts are to be listed.                                                                       | Mandatory             |
   |                       |                                                                                                                                              |                       |
   |                       | Type: String                                                                                                                                 |                       |
   |                       |                                                                                                                                              |                       |
   |                       | Default value: None                                                                                                                          |                       |
   +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | max-parts             | Sets the maximum number of parts to be listed.                                                                                               | Optional              |
   |                       |                                                                                                                                              |                       |
   |                       | Type: String                                                                                                                                 |                       |
   |                       |                                                                                                                                              |                       |
   |                       | Default: 1000                                                                                                                                |                       |
   +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | part-number           | Specifies the part after which the part listing begins. The OBS lists only parts with greater numbers than that specified by this parameter. | Optional              |
   |                       |                                                                                                                                              |                       |
   | -marker               | Type: String                                                                                                                                 |                       |
   |                       |                                                                                                                                              |                       |
   |                       | Default: None                                                                                                                                |                       |
   +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

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
    x-amz-id-2: id
    x-amz-request-id: request id
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Date: date
    Content-Type: type
    Content-Length: length
    Connection: state
    Server: server

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <ListPartsResult xmlns="http://obs.example.com/doc/2015-06-30/">
    <Bucket>BucketName</Bucket>
    <Key>ObjectName </Key>
    <UploadId>uploadid</UploadId>
    <Initiator>
    <ID>initiatorid</ID>
    <DisplayName>displayname</DisplayName>
    </Initiator>
    <Owner>
    <ID>ownerid</ID>
    <DisplayName>ownername</DisplayName>
    </Owner>
    <StorageClass>STANDARD</StorageClass>
    <PartNumberMarker>partNmebermarker</PartNumberMarker>
    <NextPartNumberMarker>nextpartnumbermarker</NextPartNumberMarker>
    <MaxParts>2</MaxParts>
    <IsTruncated>true</IsTruncated>
    <Part>
    <PartNumber>partnumber</PartNumber>
    <LastModified>modifieddate</LastModified>
    <ETag>etag</ETag>
    <Size>etag</Size>
    </Part>
    ..
    </ListPartsResult>

Response Headers
----------------

This response uses common headers. For details about common response headers, see section :ref:`Common Response Headers <en-us_topic_0125560484>`.

Response Elements
-----------------

This response uses elements to provide details about the listed parts. :ref:`Table 2 <en-us_topic_0125560266__table33229135>` describes the elements.

.. _en-us_topic_0125560266__table33229135:

.. table:: **Table 2** Response elements

   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Element                           | Description                                                                                                                                                                                                                     |
   +===================================+=================================================================================================================================================================================================================================+
   | ListPartsResult                   | Container for the response                                                                                                                                                                                                      |
   |                                   |                                                                                                                                                                                                                                 |
   |                                   | Type: Container                                                                                                                                                                                                                 |
   |                                   |                                                                                                                                                                                                                                 |
   |                                   | Children: **Bucket**, **Key**, **UploadId**, **PartNumberMarker**, **NextPartNumberMarker**, **MaxParts**, **IsTruncated**, **Part**                                                                                            |
   |                                   |                                                                                                                                                                                                                                 |
   |                                   | Ancestor: None                                                                                                                                                                                                                  |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Bucket                            | Name of the bucket to which the multipart upload was initiated                                                                                                                                                                  |
   |                                   |                                                                                                                                                                                                                                 |
   |                                   | Type: String                                                                                                                                                                                                                    |
   |                                   |                                                                                                                                                                                                                                 |
   |                                   | Ancestor: **ListPartsResult**                                                                                                                                                                                                   |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Key                               | Key of the object for which the multipart upload was initiated                                                                                                                                                                  |
   |                                   |                                                                                                                                                                                                                                 |
   |                                   | Type: String                                                                                                                                                                                                                    |
   |                                   |                                                                                                                                                                                                                                 |
   |                                   | Ancestor: **ListPartsResult**                                                                                                                                                                                                   |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | UploadId                          | ID that identifies the multipart upload whose parts are listed                                                                                                                                                                  |
   |                                   |                                                                                                                                                                                                                                 |
   |                                   | Type: String                                                                                                                                                                                                                    |
   |                                   |                                                                                                                                                                                                                                 |
   |                                   | Ancestor: **ListPartsResult**                                                                                                                                                                                                   |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Initiator                         | Container element that identifies who initiated the multipart upload                                                                                                                                                            |
   |                                   |                                                                                                                                                                                                                                 |
   |                                   | Type: Container                                                                                                                                                                                                                 |
   |                                   |                                                                                                                                                                                                                                 |
   |                                   | Children: **ID**, **DisplayName**                                                                                                                                                                                               |
   |                                   |                                                                                                                                                                                                                                 |
   |                                   | Ancestor: **ListPartsResult**                                                                                                                                                                                                   |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Owner                             | Container element that identifies the object owner. This element is the same as **Initiator** and compatible with Amazon S3. In S3, if a multipart upload is initiated by an IAM user, **Initiator** may differ from **Owner**. |
   |                                   |                                                                                                                                                                                                                                 |
   |                                   | Children: **ID**, **DisplayName**                                                                                                                                                                                               |
   |                                   |                                                                                                                                                                                                                                 |
   |                                   | Ancestor: **ListPartsResult**                                                                                                                                                                                                   |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ID                                | DomainId of initiator or owner.                                                                                                                                                                                                 |
   |                                   |                                                                                                                                                                                                                                 |
   |                                   | Type: String                                                                                                                                                                                                                    |
   |                                   |                                                                                                                                                                                                                                 |
   |                                   | Ancestor: **Initiator** or **Owner**                                                                                                                                                                                            |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | DisplayName                       | Initiator name                                                                                                                                                                                                                  |
   |                                   |                                                                                                                                                                                                                                 |
   |                                   | Type: String                                                                                                                                                                                                                    |
   |                                   |                                                                                                                                                                                                                                 |
   |                                   | Ancestor: **Initiator** or **Owner**                                                                                                                                                                                            |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | StorageClass                      | Storage class.                                                                                                                                                                                                                  |
   |                                   |                                                                                                                                                                                                                                 |
   |                                   | Type: Enumeration                                                                                                                                                                                                               |
   |                                   |                                                                                                                                                                                                                                 |
   |                                   | Valid values: STANDARD \| STANDARD_IA \|GLACIER                                                                                                                                                                                 |
   |                                   |                                                                                                                                                                                                                                 |
   |                                   | Ancestor: ListPartsResult                                                                                                                                                                                                       |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | PartNumberMarker                  | Part number after which the part listing begins                                                                                                                                                                                 |
   |                                   |                                                                                                                                                                                                                                 |
   |                                   | Type: Integer                                                                                                                                                                                                                   |
   |                                   |                                                                                                                                                                                                                                 |
   |                                   | Ancestor: **ListPartsResult**                                                                                                                                                                                                   |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | NextPartNumber Marker             | Value of **PartNumberMarker** in a subsequent request after a part list is truncated.                                                                                                                                           |
   |                                   |                                                                                                                                                                                                                                 |
   |                                   | Type: Integer                                                                                                                                                                                                                   |
   |                                   |                                                                                                                                                                                                                                 |
   |                                   | Ancestor: **ListPartsResult**                                                                                                                                                                                                   |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | MaxParts                          | Maximum number of parts that are returned                                                                                                                                                                                       |
   |                                   |                                                                                                                                                                                                                                 |
   |                                   | Type: Integer                                                                                                                                                                                                                   |
   |                                   |                                                                                                                                                                                                                                 |
   |                                   | Ancestor: **ListPartsResult**                                                                                                                                                                                                   |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | IsTruncated                       | Indicates whether the returned part list is truncated. **true** indicates that the list was truncated and **false** indicates that the list was not truncated.                                                                  |
   |                                   |                                                                                                                                                                                                                                 |
   |                                   | Type: Boolean                                                                                                                                                                                                                   |
   |                                   |                                                                                                                                                                                                                                 |
   |                                   | Ancestor: **ListPartsResult**                                                                                                                                                                                                   |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Part                              | Container for elements related to a particular part                                                                                                                                                                             |
   |                                   |                                                                                                                                                                                                                                 |
   |                                   | Type: String                                                                                                                                                                                                                    |
   |                                   |                                                                                                                                                                                                                                 |
   |                                   | Children: **PartNumber**, **LastModified**, **ETag**, **Size**                                                                                                                                                                  |
   |                                   |                                                                                                                                                                                                                                 |
   |                                   | Ancestor: **ListPartsResult**                                                                                                                                                                                                   |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | PartNumber                        | Number that identifies a part                                                                                                                                                                                                   |
   |                                   |                                                                                                                                                                                                                                 |
   |                                   | Type: Integer                                                                                                                                                                                                                   |
   |                                   |                                                                                                                                                                                                                                 |
   |                                   | Ancestor: **ListPartsResult.Part**                                                                                                                                                                                              |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | LastModified                      | Date and time at which a part was uploaded                                                                                                                                                                                      |
   |                                   |                                                                                                                                                                                                                                 |
   |                                   | Type: Date                                                                                                                                                                                                                      |
   |                                   |                                                                                                                                                                                                                                 |
   |                                   | Ancestor: **ListPartsResult.Part**                                                                                                                                                                                              |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ETag                              | ETag of an uploaded part.                                                                                                                                                                                                       |
   |                                   |                                                                                                                                                                                                                                 |
   |                                   | Type: String                                                                                                                                                                                                                    |
   |                                   |                                                                                                                                                                                                                                 |
   |                                   | Ancestor: **ListPartsResult.Part**                                                                                                                                                                                              |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Size                              | Size of an uploaded part                                                                                                                                                                                                        |
   |                                   |                                                                                                                                                                                                                                 |
   |                                   | Type: Integer                                                                                                                                                                                                                   |
   |                                   |                                                                                                                                                                                                                                 |
   |                                   | Ancestor: **ListPartsResult.Part**                                                                                                                                                                                              |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Error Responses
---------------

-  If an AccessKey or signature is invalid, OBS returns status code **403 Forbidden** and error code **AccessDenied**.
-  If the requested bucket does not exist, OBS returns status code **404 Not Found** and error code **NoSuchBucket**.
-  If the requested multipart upload does not exist, OBS returns status code **404 Not Found** and error code **NoSuchUpload**.
-  If the requester does not have **READ** permission for the requested bucket, OBS returns status code **403 Forbidden** and error code **AccessDenied**.

For details about other error responses, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`.

Sample Request
--------------

.. code-block:: text

   GET /example-object?uploadId=XXBsb2FkIElEIGZvciBlbHZpbmcncyVcdS1tb3ZpZS5tMnRzEEEwbG9hZA&max-parts=2&part-number-marker=1 HTTP/1.1
    User-Agent: Jakarta Commons-HttpClient/3.1
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Mon, 1 Nov 2010 20:34:56 GMT
    Authorization: AWS AKIAIOSFODNN7EXAMPLE:0RQf4/cRonhpaBX5sCYVf1bNRuU=

Sample Response
---------------

.. code-block::

   HTTP/1.1 200 OK
    x-amz-id-2: Uuag1LuByRx9e6j5Onimru9pO4ZVKnJ2Qz7/C1NPcfTWAtRPfTaOFg==
    x-amz-request-id: 656c76696e6727732072657175657374
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Content-Type: application/xml
    Date: Mon, 1 Nov 2010 20:34:56 GMT
    Content-Length: 985
    Connection: keep-alive
    Server: OBS

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <ListPartsResult xmlns="http://obs.example.com/doc/2015-06-30/">
    <Bucket>example-bucket</Bucket>
    <Key>example-object</Key>
    <UploadId>XXBsb2FkIElEIGZvciBlbHZpbmcncyVcdS1tb3ZpZS5tMnRzEEEwbG9hZA</UploadId>
    <Initiator>
    <ID> 11116a31-17b5-4fb7-9df5-b288870f11xx</ID>
    <DisplayName>umat-user-11116a31-17b5-4fb7-9df5-b288870f11xx</DisplayName>
    </Initiator>
    <Owner>
    <ID>75aa57f09aa0c8caeab4f8c24e99d10f8e7faeebf76c078efc7c6caea54ba06a</ID>
    <DisplayName>someName</DisplayName>
    </Owner>
    <StorageClass>STANDARD</StorageClass>
    <PartNumberMarker>1</PartNumberMarker>
    <NextPartNumberMarker>3</NextPartNumberMarker>
    <MaxParts>2</MaxParts>
    <IsTruncated>true</IsTruncated>
    <Part>
    <PartNumber>2</PartNumber>
    <LastModified>2010-11-10T20:48:34.000Z</LastModified>
    <ETag>"7778aef83f66abc1fa1e8477f296d394"</ETag>
    <Size>10485760</Size>
    </Part>
    <Part>
    <PartNumber>3</PartNumber>
    <LastModified>2010-11-10T20:48:33.000Z</LastModified>
    <ETag>"aaaa18db4cc2f85cedef654fccc4a4x8"</ETag>
    <Size>10485760</Size>
    </Part>
    </ListPartsResult>
