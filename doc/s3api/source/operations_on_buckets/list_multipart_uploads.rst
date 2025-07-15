:original_name: en-us_topic_0125560292.html

.. _en-us_topic_0125560292:

List Multipart Uploads
======================

You can use this operation to query all in-progress multipart uploads that have been initiated but not been combined or aborted.

Request Syntax
--------------

.. code-block:: text

   GET /?uploads&max-uploads=max HTTP/1.1
    User-Agent: agent
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Mon, 1 Nov 2010 20:34:56 GMT
    Authorization: auth

Request Parameters
------------------

This request uses parameters to specify the query range for multipart uploads. :ref:`Table 1 <en-us_topic_0125560292__table25002124>` describes the parameters.

.. _en-us_topic_0125560292__table25002124:

.. table:: **Table 1** Request parameters

   +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Parameter             | Description                                                                                                                                                                                                                                                                                                                                                                | Remarks               |
   +=======================+============================================================================================================================================================================================================================================================================================================================================================================+=======================+
   | delimiter             | Character used to group object keys.                                                                                                                                                                                                                                                                                                                                       | Optional              |
   |                       |                                                                                                                                                                                                                                                                                                                                                                            |                       |
   |                       | All keys that contain the same string between **prefix**, if specified, and the first occurrence of the delimiter after **prefix** are grouped under a single result element **CommonPrefixes**. **CommonPrefix** contains no information about any multipart upload. It is only used for informing users of the following: multipart uploads are contained in this group. |                       |
   |                       |                                                                                                                                                                                                                                                                                                                                                                            |                       |
   |                       | Type: String                                                                                                                                                                                                                                                                                                                                                               |                       |
   +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | prefix                | Lists in-progress uploads only for those object keys that begin with the specified prefix.                                                                                                                                                                                                                                                                                 | Optional              |
   |                       |                                                                                                                                                                                                                                                                                                                                                                            |                       |
   |                       | Type: String                                                                                                                                                                                                                                                                                                                                                               |                       |
   +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | max-uploads           | Sets the maximum number (ranging from 1 to 1000) of multipart uploads to be returned in the response body. If the value is not in this range, 1000 is returned by default.                                                                                                                                                                                                 | Optional              |
   |                       |                                                                                                                                                                                                                                                                                                                                                                            |                       |
   |                       | Type: Integer                                                                                                                                                                                                                                                                                                                                                              |                       |
   +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | key-marker            | Indicates the multipart upload after which the listing begins.                                                                                                                                                                                                                                                                                                             | Optional              |
   |                       |                                                                                                                                                                                                                                                                                                                                                                            |                       |
   |                       | Type: String                                                                                                                                                                                                                                                                                                                                                               |                       |
   +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | upload-id-marker      | Indicates the multipart upload after which the listing begins. This parameter is used together with **key-marker**.                                                                                                                                                                                                                                                        | Optional              |
   |                       |                                                                                                                                                                                                                                                                                                                                                                            |                       |
   |                       | Type: String                                                                                                                                                                                                                                                                                                                                                               |                       |
   +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

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
    Server: OBS
    x-amz-request-id: request id
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    x-amz-id-2: id2
    Content-Length: length
    Date: date
    Connection: connect state

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <ListMultipartUploadsResult xmlns="http://obs.example.com/doc/2015-06-30/">
    <Bucket>bucket</Bucket>
    <KeyMarker></KeyMarker>
    <UploadIdMarker></UploadIdMarker>
    <NextKeyMarker>nextMarker</NextKeyMarker>
    <NextUploadIdMarker>idMarker</NextUploadIdMarker>
    <Delimiter></Delimiter>
    <Prefix></Prefix>
    <MaxUploads>maxUploads</MaxUploads>
    <IsTruncated>true</IsTruncated>
    <Upload>
    <Key>key</Key>
    <UploadId>uploadID</UploadId>
    <Initiator>
    <ID>id</ID>
    <DisplayName>name</DisplayName>
    </Initiator>
    <Owner>
    <ID>ownerID</ID>
    <DisplayName>OwnerDisplayName</DisplayName>
    </Owner>
    <StorageClass>STANDARD</StorageClass>
    <Initiated>initiatedDate</Initiated>
    </Upload>
    </ListMultipartUploadsResult>

Response Headers
----------------

This response uses common headers. For details about common response headers, see section :ref:`Common Response Headers <en-us_topic_0125560484>`.

Response Elements
-----------------

This response contains elements to provide details about the listed multipart uploads. :ref:`Table 2 <en-us_topic_0125560292__table36296664>` describes the elements.

.. _en-us_topic_0125560292__table36296664:

.. table:: **Table 2** Response elements

   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Element                           | Description                                                                                                                                                                                                                     | Remarks               |
   +===================================+=================================================================================================================================================================================================================================+=======================+
   | ListMultipartUploads Result       | Container for the response                                                                                                                                                                                                      | Mandatory             |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Type: Container                                                                                                                                                                                                                 |                       |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Children: **Bucket**, **KeyMarker**, **UploadIdMarker**, **NextKeyMarker**, **NextUploadIdMarker**, **Delimiter**, **Prefix**, **MaxUploads**, **IsTruncated**, **Upload**, and **CommonPrefixes**                              |                       |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Ancestor: None                                                                                                                                                                                                                  |                       |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Bucket                            | Name of the bucket to which the multipart upload was initiated                                                                                                                                                                  | Mandatory             |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Type: String                                                                                                                                                                                                                    |                       |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Ancestor: **ListMultipartUploadsResult**                                                                                                                                                                                        |                       |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | KeyMarker                         | Object keys at or after which the multipart upload listing begins                                                                                                                                                               | Mandatory             |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Type: String                                                                                                                                                                                                                    |                       |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Ancestor: **ListMultipartUploadsResult**                                                                                                                                                                                        |                       |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | UploadIdMarker                    | Upload ID after which the multipart upload listing begins                                                                                                                                                                       | Mandatory             |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Type: String                                                                                                                                                                                                                    |                       |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Ancestor: **ListMultipartUploadsResult**                                                                                                                                                                                        |                       |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | NextKeyMarker                     | Value of **KeyMarker** in a subsequent request after a multipart upload list is truncated                                                                                                                                       | Mandatory             |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Type: String                                                                                                                                                                                                                    |                       |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Ancestor: **ListMultipartUploadsResult**                                                                                                                                                                                        |                       |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | NextUploadIdMarker                | Value of **UploadMarker** in a subsequent request after a multipart upload list is truncated                                                                                                                                    | Mandatory             |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Type: String                                                                                                                                                                                                                    |                       |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Ancestor: **ListMultipartUploadsResult**                                                                                                                                                                                        |                       |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | MaxUploads                        | Maximum of multipart uploads to be returned in the response                                                                                                                                                                     | Mandatory             |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Type: Integer                                                                                                                                                                                                                   |                       |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Ancestor: **ListMultipartUploadsResult**                                                                                                                                                                                        |                       |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | IsTruncated                       | Indicates whether the returned list of multipart uploads is truncated. **true** indicates that the list was truncated and **false** indicates that the list was not truncated.                                                  | Mandatory             |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Type: Boolean                                                                                                                                                                                                                   |                       |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Ancestor: **ListMultipartUploadsResult**                                                                                                                                                                                        |                       |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Upload                            | Container for elements related to a specific multipart upload                                                                                                                                                                   | Mandatory             |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Type: Container                                                                                                                                                                                                                 |                       |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Children: **Key**, **UploadId**, **InitiatorOwner**, **StorageClass**, **Initiated**                                                                                                                                            |                       |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Ancestor: **ListMultipartUploadsResult**                                                                                                                                                                                        |                       |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Key                               | Key of the object for which the multipart upload was initiated                                                                                                                                                                  | Mandatory             |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Type: String                                                                                                                                                                                                                    |                       |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Ancestor: **Upload**                                                                                                                                                                                                            |                       |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | UploadId                          | ID of the multipart upload                                                                                                                                                                                                      | Mandatory             |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Type: String                                                                                                                                                                                                                    |                       |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Ancestor: **Upload**                                                                                                                                                                                                            |                       |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Initiator                         | Container element that identifies who initiated the multipart upload                                                                                                                                                            | Mandatory             |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Children: **ID**, **DisplayName**                                                                                                                                                                                               |                       |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Type: Container                                                                                                                                                                                                                 |                       |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Ancestor: **Upload**                                                                                                                                                                                                            |                       |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | ID                                | DomainId of the user.                                                                                                                                                                                                           | Mandatory             |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Type: String                                                                                                                                                                                                                    |                       |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Ancestor: **Initiator**, **Owner**                                                                                                                                                                                              |                       |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | DisplayName                       | Initiator name                                                                                                                                                                                                                  | Mandatory             |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Type: String                                                                                                                                                                                                                    |                       |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Ancestor: **Initiator**, **Owner**                                                                                                                                                                                              |                       |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Owner                             | Container element that identifies the object owner. This element is the same as **Initiator** and compatible with Amazon S3. In S3, if a multipart upload is initiated by an IAM user, **Initiator** may differ from **Owner**. | Mandatory             |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Type: Container                                                                                                                                                                                                                 |                       |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Children: **ID**, **DisplayName**                                                                                                                                                                                               |                       |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Ancestor: **Upload**                                                                                                                                                                                                            |                       |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | StorageClass                      | Type of storage that will be used for storing objects after the multipart upload is complete.                                                                                                                                   | Mandatory             |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Type: Enumeration                                                                                                                                                                                                               |                       |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Ancestor: **Upload**                                                                                                                                                                                                            |                       |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Initiated                         | Date and time at which the multipart upload was initiated                                                                                                                                                                       | Mandatory             |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Type: Date                                                                                                                                                                                                                      |                       |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Ancestor: **Upload**                                                                                                                                                                                                            |                       |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | ListMultipartUploadsResult.Prefix | Contains the prefix specified in the request.                                                                                                                                                                                   | Mandatory             |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Type: String                                                                                                                                                                                                                    |                       |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Ancestor: **ListMultipartUploadsResult**                                                                                                                                                                                        |                       |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Delimiter                         | Contains the delimiter specified in the request.                                                                                                                                                                                | Mandatory             |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Type: String                                                                                                                                                                                                                    |                       |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Ancestor: **ListMultipartUploadsResult**                                                                                                                                                                                        |                       |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | CommonPrefixes                    | If you specify a delimiter in the request, the result returns each distinct key prefix containing the delimiter in a **CommonPrefixes** element.                                                                                | Mandatory             |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Type: Container                                                                                                                                                                                                                 |                       |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Ancestor: **ListMultipartUploadsResult**                                                                                                                                                                                        |                       |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | CommonPrefixes. Prefix            | Prefix contained in a **CommonPrefix** element                                                                                                                                                                                  | Mandatory             |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Type: String                                                                                                                                                                                                                    |                       |
   |                                   |                                                                                                                                                                                                                                 |                       |
   |                                   | Ancestor: **CommonPrefixes**                                                                                                                                                                                                    |                       |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

Error Responses
---------------

#. If an AK or signature is invalid, OBS returns status code **403 Forbidden** and error code **AccessDenied**.
#. If the requested bucket does not exist, OBS returns status code **404 Not Found** and error code **NoSuchBucket**.
#. If the requester does not have **READ** permission for the requested bucket, OBS returns status code **403 Forbidden** and error code **AccessDenied**.
#. If the value of **maxUploads** is a non-integer or smaller than 0, OBS returns status code **400 Bad Request**.

For details about other error responses, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`.

Sample Request
--------------

.. code-block:: text

   GET /?uploads&max-uploads=3 HTTP/1.1
    User-Agent: curl/7.19.0
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Mon, 1 Nov 2010 20:34:56 GMT
    Authorization: AWS AKIAIOSFODNN7EXAMPLE:0RQf4/cRonhpaBX5sCYVf1bNRuU=

Sample Response
---------------

.. code-block::

   HTTP/1.1 200 OK
    Server: OBS
    x-amz-request-id: 656c76696e6727732072657175657374
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    x-amz-id-2: Uuag1LuByRx9e6j5Onimru9pO4ZVKnJ2Qz7/C1NPcfTWAtRPfTaOFg==
    Date: Mon, 1 Nov 2010 20:34:56 GMT
    Content-Length: 1330
    Connection: keep-alive

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <ListMultipartUploadsResult xmlns="http://obs.example.com/doc/2015-06-30/">
    <Bucket>bucket</Bucket>
    <KeyMarker></KeyMarker>
    <UploadIdMarker></UploadIdMarker>
    <NextKeyMarker>my-movie.m2ts</NextKeyMarker>
    <NextUploadIdMarker>YW55gd2h5IGVsdmluZydzIHVwbG9hZCBmYWlsZWQ</NextUploadIdMarker>
    <Delimiter></Delimiter>
    <Prefix></Prefix>
    <MaxUploads>3</MaxUploads>
    <IsTruncated>true</IsTruncated>
    <Upload>
    <Key>my-divisor</Key>
    <UploadId>XMgbGlrZSBlbHZpbmcncyBub3QgaGF2aW5nIG11Y2ggbHVjaw</UploadId>
    <Initiator>
    <ID>b1d16700c70b0b05597d7acd6a3f92be</ID>
    <DisplayName>InitiatorDisplayName</DisplayName>
    </Initiator>
    <Owner>
    <ID>75aa57f09aa0c8caeab4f84e99d10f8e</ID>
    <DisplayName>OwnerDisplayName</DisplayName>
    </Owner>
    <StorageClass>STANDARD</StorageClass>
    <Initiated>2010-11-10T20:48:33.000Z</Initiated>
    </Upload>
    <Upload>
    <Key>my-movie.m2ts</Key>
    <UploadId>VXBsb2FkIElEIGZvciBlbHZpbmcncyBteS1tb3ZpZS5tMnRzIHVwbG9hZA</UploadId>
    <Initiator>
    <ID>b1d16700c70b0b05597d7acd6a3f92be</ID>
    <DisplayName>InitiatorDisplayName</DisplayName>
    </Initiator>
    <Owner>
    <ID>b1d16700c70b0b05597d7acd6a3f92be</ID>
    <DisplayName>InitiatorDisplayName</DisplayName>
    </Owner>
    <StorageClass>STANDARD</StorageClass>
    <Initiated>2010-11-10T20:48:33.000Z</Initiated>
    </Upload>
    <Upload>
    <Key>my-movie.m2ts</Key>
    <UploadId>YW55IGlkZWEgd2h5IGVsdmluZydzIHVwbG9hZCBmYWlsZWQ</UploadId>
    <Initiator>
    <ID>75aa57f09aa0c8caeab4f84e99d10f8e</ID>
    <DisplayName>OwnerDisplayName</DisplayName>
    </Initiator>
    <Owner>
    <ID>b1d16700c70b0b05597d7acd6a3f92be</ID>
    <DisplayName>InitiatorDisplayName</DisplayName>
    </Owner>
    <StorageClass>STANDARD</StorageClass>
    <Initiated>2010-11-10T20:49:33.000Z</Initiated>
    </Upload>
    </ListMultipartUploadsResult>
