:original_name: obs_04_0086.html

.. _obs_04_0086:

Deleting Objects
================

Functions
---------

This operation can be used to batch delete some objects in a bucket. The deletion cannot be undone. After the operation is implemented, the returned information contains the implementation result of each object in the specified bucket. OBS deletes the objects synchronously. The deletion result of each object is returned to the request user.

Objects in batches can be deleted in **verbose** or **quiet** mode. With **verbose** mode, OBS returns results of successful and failed deletion in an XML response; with **quiet** mode, OBS only returns results of failed deletion in an XML response. OBS uses the **verbose** mode by default and you can specify the **quiet** mode in the request body.

For batch deletion, the request header must contain **Content-MD5** and **Content-Length**, so that the message body can be identified if network transmission error is detected at the server side.

Request Syntax
--------------

.. code-block:: text

   POST /?delete HTTP/1.1
   Host: bucketname.obs.region.example.com
   Date: date
   Authorization: authorization
   Content-MD5: MD5
   Content-Length: length

   <?xml version="1.0" encoding="UTF-8"?>
   <Delete>
       <Quiet>true</Quiet>
       <Object>
           <Key>Key</Key>
           <VersionId>VersionId</VersionId>
       </Object>
       <Object>
           <Key>Key</Key>
       </Object>
   </Delete>

Request Parameters
------------------

This request involves no parameters.

Request Headers
---------------

This request uses common headers. For details, see :ref:`Table 3 <obs_04_0007__table25197309>`.

Request Elements
----------------

This request uses elements to specify the list of objects to be deleted in a batch. :ref:`Table 1 <obs_04_0086__table42836777>` describes the elements.

.. _obs_04_0086__table42836777:

.. table:: **Table 1** Request elements

   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Element               | Description                                                                                                                                                                                   | Mandatory             |
   +=======================+===============================================================================================================================================================================================+=======================+
   | Quiet                 | Specifies the **quiet** mode. With the **quiet** mode, OBS only returns the list of objects that failed to be deleted. This element is valid when set to **true**. Otherwise, OBS ignores it. | No                    |
   |                       |                                                                                                                                                                                               |                       |
   |                       | Type: boolean                                                                                                                                                                                 |                       |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Delete                | List of objects to be deleted                                                                                                                                                                 | Yes                   |
   |                       |                                                                                                                                                                                               |                       |
   |                       | Type: XML                                                                                                                                                                                     |                       |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Object                | Names of objects to be deleted                                                                                                                                                                | Yes                   |
   |                       |                                                                                                                                                                                               |                       |
   |                       | Type: XML                                                                                                                                                                                     |                       |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Key                   | Key of the object to be deleted                                                                                                                                                               | Yes                   |
   |                       |                                                                                                                                                                                               |                       |
   |                       | Type: string                                                                                                                                                                                  |                       |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | VersionId             | Version ID of the object to be deleted                                                                                                                                                        | No                    |
   |                       |                                                                                                                                                                                               |                       |
   |                       | Type: string                                                                                                                                                                                  |                       |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

A maximum of 1,000 objects can be deleted at a time. If you send a request for deleting more than 1,000 objects, OBS returns an error message.

After concurrent tasks are assigned, OBS may encounter an internal error during cyclic deletion of multiple objects. In that case, the metadata still exists when the object index data is deleted, which means data inconsistency.

Response Syntax
---------------

::

   HTTP/1.1 status_code
   Date: date
   Content-Type: application/xml
   Content-Length: length

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <DeleteResult xmlns="http://obs.region.example.com/doc/2015-06-30/">
   <Deleted>
       <Key>Key</Key>
   </Deleted>
   <Error>
       <Key>Key</Key>
       <Code>ErrorCode</Code>
       <Message>Message</Message>
   </Error>
   </DeleteResult>

Response Headers
----------------

The response to the request uses common headers. For details, see :ref:`Table 1 <obs_04_0013__d0e686>`.

Response Elements
-----------------

This response uses elements to return results of deleted objects in a batch. :ref:`Table 2 <obs_04_0086__table56991560>` describes the elements.

.. _obs_04_0086__table56991560:

.. table:: **Table 2** Response elements

   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Element                           | Description                                                                                                                                                                                                     |
   +===================================+=================================================================================================================================================================================================================+
   | DeleteResult                      | Root node of batch deletion responses                                                                                                                                                                           |
   |                                   |                                                                                                                                                                                                                 |
   |                                   | Type: container                                                                                                                                                                                                 |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Deleted                           | Container for results of successful deletion                                                                                                                                                                    |
   |                                   |                                                                                                                                                                                                                 |
   |                                   | Type: container                                                                                                                                                                                                 |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Error                             | Container for results of failed deletion                                                                                                                                                                        |
   |                                   |                                                                                                                                                                                                                 |
   |                                   | Type: container                                                                                                                                                                                                 |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Key                               | Object names in a deletion result                                                                                                                                                                               |
   |                                   |                                                                                                                                                                                                                 |
   |                                   | Type: string                                                                                                                                                                                                    |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Code                              | Error code of a deletion failure                                                                                                                                                                                |
   |                                   |                                                                                                                                                                                                                 |
   |                                   | Type: string                                                                                                                                                                                                    |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Message                           | Error message of a deletion failure                                                                                                                                                                             |
   |                                   |                                                                                                                                                                                                                 |
   |                                   | Type: string                                                                                                                                                                                                    |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | VersionId                         | Version IDs of objects to be deleted                                                                                                                                                                            |
   |                                   |                                                                                                                                                                                                                 |
   |                                   | Type: string                                                                                                                                                                                                    |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | DeleteMarker                      | If this element is specified, **true** will be returned when you create or delete a deletion marker in the requested bucket with versioning enabled.                                                            |
   |                                   |                                                                                                                                                                                                                 |
   |                                   | Type: boolean                                                                                                                                                                                                   |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | DeleteMarkerVersionId             | Indicates the version ID of the deletion marker deleted or created by the request.                                                                                                                              |
   |                                   |                                                                                                                                                                                                                 |
   |                                   | If the request either creates or deletes a deletion marker, OBS returns this element in response with the version ID of the deletion marker. This element will be returned in either of the following cases:    |
   |                                   |                                                                                                                                                                                                                 |
   |                                   | -  You send a versionless request, that is, you specify only the object name but not the version ID. In this case, the UDS creates a deletion marker and returns its version ID in the response.                |
   |                                   | -  You send a request with versions, that is, you specify object keys and version IDs that identify deletion markers. In this case, OBS deletes the deletion marker and returns its version ID in the response. |
   |                                   |                                                                                                                                                                                                                 |
   |                                   | Type: boolean                                                                                                                                                                                                   |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Error Responses
---------------

1. If the resolution result of an XML request contains more than 1000 objects, OBS returns **400 Bad Request**.

2. If the object key in an XML request is invalid (for example, containing more than 1024 characters), OBS returns **400 Bad Request**.

3. If the request header does not contain Content-MD5, OBS returns **400 Bad Request**.

Other errors are included in :ref:`Table 2 <obs_04_0115__d0e843>`.

Sample Request
--------------

.. code-block:: text

   POST /test333?delete HTTP/1.1
   User-Agent: curl/7.29.0
   Host: 127.0.0.1
   Accept: */*
   Date: WED, 01 Jul 2015 04:34:21 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:8sjZWJlWmYmYnK5JqXaFFQ+vHEg=
   Content-MD5: ZPzz8L+hdRJ6qCqYbU/pCw==
   Content-Length: 188

   <?xml version="1.0" encoding="utf-8"?>
   <Delete>
     <Quiet>true</Quiet>
     <Object>
       <Key>obja02</Key>
     </Object>
     <Object>
       <Key>obja02</Key>
     </Object>
   </Delete>

Sample Response
---------------

::

   HTTP/1.1 200 OK
   Server: OBS
   x-obs-request-id: 8DF400000163D3FE4CE80340D30B0542
   x-obs-id-2: 32AAAQAAEAABAAAQAAEAABAAAQAAEAABCRhY0FBWRm6qjOE1ACBZwS+0KYlPBq0f
   Content-Type: application/xml
   Date: WED, 01 Jul 2015 04:34:21 GMT
   Content-Length: 120

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <DeleteResult xmlns="http://obs.example.com/doc/2015-06-30/"/>
