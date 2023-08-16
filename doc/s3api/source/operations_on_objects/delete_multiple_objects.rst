:original_name: en-us_topic_0125560366.html

.. _en-us_topic_0125560366:

DELETE Multiple Objects
=======================

You can use this operation to delete multiple objects from a bucket in batches.

Deleted objects cannot be restored or accessed using **LIST** or **GET**. The OBS deletes multiple objects simultaneously and returns the deletion result of each object.

The **DELETE Multiple Objects** operation supports two modes for response: verbose and quiet.

In verbose mode, the returned response includes the deletion result of each requested object in an XML file.

In quiet mode, the returned response includes only results of objects failed to be deleted. The OBS uses verbose mode by default and you can specify quiet mode in the request body.

A **DELETE Multiple Objects** request must contain headers **Content-MD5** and **Content-Length** to detect network errors.

Request Syntax
--------------

.. code-block:: text

   POST /?delete HTTP/1.1
    User-Agent: agent
    Host: bucketname.obs.example.com
    Accept: */*
    Date: date
    Authorization: Signature
    Content-MD5: MD5
    Content-Length: length
    Expect: expect

    <?xml version="1.0" encoding="UTF-8"?>
    <Delete>
    <Quiet>true</Quiet>
    <Object>
    <Key>Key1</Key>
    </Object>
    <Object>
    <Key>Key2</Key>
    </Object>
    </Delete>

Request Parameters
------------------

This request involves no parameters.

Request Headers
---------------

This request uses common headers. For details about common request headers, see section :ref:`Common Request Headers <en-us_topic_0125560462>`.

Request Elements
----------------

This request uses elements to specify the list of objects to be deleted in batches. :ref:`Table 1 <en-us_topic_0125560366__table42836777>` describes the elements.

.. _en-us_topic_0125560366__table42836777:

.. table:: **Table 1** Request elements

   +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Element               | Description                                                                                                                                              | Remarks               |
   +=======================+==========================================================================================================================================================+=======================+
   | Quiet                 | Indicates the element to enable quite mode for the request. If the element is specified, OBS returns only the list of objects that failed to be deleted. | Optional              |
   |                       |                                                                                                                                                          |                       |
   |                       | This element is only valid when its value is **true**. Otherwise, OBS ignores it.                                                                        |                       |
   |                       |                                                                                                                                                          |                       |
   |                       | Type: Boolean                                                                                                                                            |                       |
   +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Delete                | Indicates the list of objects to be deleted.                                                                                                             | Mandatory             |
   |                       |                                                                                                                                                          |                       |
   |                       | Type: XML                                                                                                                                                |                       |
   +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Object                | Indicates an object to be deleted.                                                                                                                       | Mandatory             |
   |                       |                                                                                                                                                          |                       |
   |                       | Type: XML                                                                                                                                                |                       |
   +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Key                   | Indicates the key of an object to be deleted.                                                                                                            | Mandatory             |
   |                       |                                                                                                                                                          |                       |
   |                       | Type: String                                                                                                                                             |                       |
   +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | VersionId             | Indicates the version ID of an object to be deleted.                                                                                                     | Optional              |
   |                       |                                                                                                                                                          |                       |
   |                       | Type: String                                                                                                                                             |                       |
   +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

.. important::

   Request constraints:

   This request can delete a maximum of 1000 objects at a time. If you send the request to delete more than 1000 objects, OBS returns an error response.

   After receiving the request, OBS deletes objects simultaneously in a circular manner. During this process, OBS may encounter an internal error. For example, data inconsistency may occur because the metadata of an object still exists after the object's index data is deleted.

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
    Server: server

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <DeleteResult xmlns="http://obs.example.com/doc/2015-06-30/">
    <Deleted>
    <Key>Key1</Key>
    </Deleted>
    <Error>
    <Key>Key2</Key>
    <Code>InternalError</Code>
    <Message>Internal Error</Message>
    </Error>
    </DeleteResult>

Response Headers
----------------

This response uses common headers. For details about common response headers, see section :ref:`Common Response Headers <en-us_topic_0125560484>`.

Response Elements
-----------------

This response contains elements to return results of object deletion. :ref:`Table 2 <en-us_topic_0125560366__table56991560>` describes the elements.

.. _en-us_topic_0125560366__table56991560:

.. table:: **Table 2** Response elements

   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Element               | Description                                                                                                                                                                                                                               | Remarks               |
   +=======================+===========================================================================================================================================================================================================================================+=======================+
   | DeleteResult          | Indicates the container for the response.                                                                                                                                                                                                 | Mandatory             |
   |                       |                                                                                                                                                                                                                                           |                       |
   |                       | Type: Container                                                                                                                                                                                                                           |                       |
   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Deleted               | Indicates the container element for a successful deletion.                                                                                                                                                                                | Mandatory             |
   |                       |                                                                                                                                                                                                                                           |                       |
   |                       | Type: Container                                                                                                                                                                                                                           |                       |
   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Error                 | Indicates the container for a failed deletion.                                                                                                                                                                                            | Mandatory             |
   |                       |                                                                                                                                                                                                                                           |                       |
   |                       | Type: Container                                                                                                                                                                                                                           |                       |
   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Key                   | Indicates the key of a deleted object.                                                                                                                                                                                                    | Mandatory             |
   |                       |                                                                                                                                                                                                                                           |                       |
   |                       | Type: String                                                                                                                                                                                                                              |                       |
   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Code                  | Indicates the status code for a failed deletion.                                                                                                                                                                                          | Mandatory             |
   |                       |                                                                                                                                                                                                                                           |                       |
   |                       | Type: String                                                                                                                                                                                                                              |                       |
   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Message               | Indicates the error details about a failed deletion.                                                                                                                                                                                      | Mandatory             |
   |                       |                                                                                                                                                                                                                                           |                       |
   |                       | Type: String                                                                                                                                                                                                                              |                       |
   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | VersionId             | Indicates the version ID of an object to be deleted.                                                                                                                                                                                      | Optional              |
   |                       |                                                                                                                                                                                                                                           |                       |
   |                       | Type: String                                                                                                                                                                                                                              |                       |
   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | DeleteMarker          | If this element is specified, **true** will be returned when you create or delete a deletion mark in the requested bucket with versioning enabled.                                                                                        | Optional              |
   |                       |                                                                                                                                                                                                                                           |                       |
   |                       | Type: Boolean                                                                                                                                                                                                                             |                       |
   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | DeleteMarkerVersionId | Indicates the version ID of the deletion marker deleted or created by the request.                                                                                                                                                        | Optional              |
   |                       |                                                                                                                                                                                                                                           |                       |
   |                       | If the **DELETE multiple objects** request either creates or deletes a deletion marker, OBS returns this element in response with the version ID of the deletion marker. This element will be returned in either of the following cases:  |                       |
   |                       |                                                                                                                                                                                                                                           |                       |
   |                       | -  You send a non-version **DELETE multiple object** request, that is, you specify only object key but not the version ID. In this case, OBS creates a deletion marker and returns its version ID in the response.                        |                       |
   |                       | -  You send a version **DELETE multiple objects** request, that is, you specify an object key and a version ID that identifies a deletion marker. In this case, OBS deletes a deletion marker and returns its version ID in the response. |                       |
   |                       |                                                                                                                                                                                                                                           |                       |
   |                       | Type: Boolean                                                                                                                                                                                                                             |                       |
   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

Error Responses
---------------

#. If more than 1000 objects are requested, OBS returns status code **400 Bad Request**.
#. If an object key is invalid (for example, the object key contains 1024 characters), OBS returns status code **400 Bad Request**.
#. If the **Content-MD5** header does not exist, OBS returns status code **400 Bad Request**.
#. If bucket metadata does not exist, OBS returns status code **404 Not Found** and error code **NoSuchBucket**.
#. If the requester does not have **WRITE** permission for the requested bucket, OBS returns status code **403 Forbidden** and prompt message **AccessDenied**.

For details about other error responses, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`.

Sample Request
--------------

.. code-block:: text

   POST /?delete HTTP/1.1
    User-Agent: Jakarta Commons-HttpClient/3.1
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Tue, 14 Jan 2014 12:10:09 +0000
    Authorization: AWS BF6C09F302931425E9A7:wQ1Tp3rD7kaUCsYfPKxOIN7NoSA=
    Content-MD5: 367CB63A2F283044981285491015079
    Content-Length: 135
    Expect: 100-continue

    <?xml version="1.0" encoding="UTF-8"?>
    <Delete>
    <Quiet>true</Quiet>
    <Object>
    <Key>Key1</Key>
    </Object>
    <Object>
    <Key>Key2</Key>
    </Object>
    </Delete>

Sample Response
---------------

.. code-block::

   HTTP/1.1 200 OK
    x-amz-id-2: Weag1LuByRx9e6j5Onimru9pO4ZVKnJ2Qz7/C1NPcfTWAtRPfTaOFg==
    x-amz-request-id: 996c76696e6727732072657175657374
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Date: Mon, 1 Nov 2010 20:34:56 GMT
    Content-Type: application/xml
    Content-Length: 10485760
    Server: OBS

    <?xml version="1.0" encoding="UTF-8"?>
    <DeleteResult xmlns="http://obs.example.com/doc/2015-06-30/">
    <Deleted>
    <Key>Key1</Key>
    </Deleted>
    <Error>
    <Key>Key2</Key>
    <Code>InternalError</Code>
    <Message>Internal Error</Message>
    </Error>
    </DeleteResult>

Sample Request (Deleting an Object with No Version ID Specified form a Bucket with Versioning Enabled)
------------------------------------------------------------------------------------------------------

.. code-block:: text

   POST /?delete HTTP/1.1
    User-Agent: Jakarta Commons-HttpClient/3.1
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Tue, 14 Jan 2014 12:10:09 +0000
    Authorization: AWS C9590CEB8EC051BDEC9D:HLq5AmI/Zlz1PPsXdk6pIHuNaCM=
    Content-MD5: uj2BQLIgDcegTcWHwEGoiA==
    Content-Length: 64
    Expect: 100-continue

    <Delete>
    <Object>
    <Key>object</Key>
    </Object>
    </Delete>

Sample Response (Deleting an Object with No Version ID Specified form a Bucket with Versioning Enabled)
-------------------------------------------------------------------------------------------------------

.. code-block::

   HTTP/1.1 200 OK
    Server: OBS
    x-amz-request-id: DCD2FC9CAB780000014390A8AA7D4763
    x-amz-id-2: iFIiPx4egtz5ToRcIIkVZ5Nz8F+zUCis6JKhuQysA4gxLIt+EgPMTMuO08beG7sd
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Content-Type: application/xml
    Date: Tue, 14 Jan 2014 12:10:09 GMT
    Content-Length: 280

    <DeleteResult xmlns="http://obs.example.com/doc/2015-06-30/">
    <Deleted>
    <Key>object</Key>
    <DeleteMarker>true</DeleteMarker>
    <DeleteMarkerVersionId>AAABQ5Coqqzc0vycq3gAAAAZVURTRkha</DeleteMarkerVersionId>
    </Deleted>
    </DeleteResult>

Sample Request (Deleting an Object with Version ID Specified from a Bucket)
---------------------------------------------------------------------------

.. code-block:: text

   POST /example?delete HTTP/1.1
    User-Agent: Jakarta Commons-HttpClient/3.1
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Tue, 14 Jan 2014 12:19:57 +0000
    Authorization: AWS C9590CEB8EC051BDEC9D:eTmW0xEkSYrfqOSjZUV7zS+Ap5Y=
    Content-MD5: YDYt+eVo7S5tnBHaHOylGA==
    Content-Length: 124
    Expect: 100-continue

    <Delete>
    <Object>
    <Key>object</Key>
    <VersionId>AAABQ4-glIvc0vycq3gAAAAVVURTRkha</VersionId>
    </Object>
    </Delete>

Sample Response (Deleting an Object with Version ID Specified from a Bucket)
----------------------------------------------------------------------------

.. code-block::

   HTTP/1.1 200 OK
    Server: OBS
    x-amz-request-id: DCD2FC9CAB780000014390B1A5974C2C
    x-amz-id-2: x9Vt2FIjXLjyu38NHeHG+IIYQIQKQjZrEDSHOElJMvEb/SUfY5k54C/uX8GfGUFz
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Content-Type: application/xml
    Date: Tue, 14 Jan 2014 12:19:58 GMT
    Content-Length: 223

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <DeleteResult xmlns="http://obs.example.com/doc/2015-06-30/">
    <Deleted>
    <Key>object</Key>
    <VersionId>AAABQ4-glIvc0vycq3gAAAAVVURTRkha</VersionId>
    </Deleted>
    </DeleteResult>

Sample Request (Deleting a Deletion Mark in a Bucket with Version ID Specified)
-------------------------------------------------------------------------------

.. code-block:: text

   POST /example?delete HTTP/1.1
    User-Agent: Jakarta Commons-HttpClient/3.1
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Wed, 15 Jan 2014 02:03:40 +0000
    Authorization: AWS C9590CEB8EC051BDEC9D:N/UdjEab/8H5Llgw1HUpTd21wc4=
    Content-MD5: n9LlSFB87vGiGDqDKLXPLA==
    Content-Length: 124
    Expect: 100-continue

    <Delete>
    <Object>
    <Key>object</Key>
    <VersionId>AAABQ49lNT_c0vycq3gAAAAOVURTRkha</VersionId>
    </Object>
    </Delete>

Sample Response (Deleting a Deletion Mark in a Bucket with Version ID Specified)
--------------------------------------------------------------------------------

.. code-block::

   HTTP/1.1 200 OK
    Server: OBS
    x-amz-request-id: DCD2FC9CAB780000014393A3C5CEDE66
    x-amz-id-2: N9UP5OvD4BwlQAfyqow6TLWq7HIsG8As4bP/CCNFjcp1Ab8Cc4JAFPm0bjV9WrTg
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Content-Type: application/xml
    Date: Wed, 15 Jan 2014 02:03:40 GMT
    Content-Length: 335

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <DeleteResult xmlns="http://obs.example.com/doc/2015-06-30/">
    <Deleted>
    <Key>object</Key>
    <VersionId>AAABQ49lNT_c0vycq3gAAAAOVURTRkha</VersionId>
    <DeleteMarker>true</DeleteMarker>
    <DeleteMarkerVersionId>AAABQ49lNT_c0vycq3gAAAAOVURTRkha</DeleteMarkerVersionId>
    </Deleted>
    </DeleteResult>
