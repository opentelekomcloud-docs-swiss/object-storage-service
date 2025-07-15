:original_name: en-us_topic_0125560255.html

.. _en-us_topic_0125560255:

Request Responses
=================

OBS returns an HTTP response after receiving and processing a request. A response contains a status line, response headers, and an optional response body.

Response Syntax
---------------

.. code-block::

   Status Line: HTTP-Version Status-Code Reason-Phrase
    Response Headers
    <Conditional Response Body>

Status Line
-----------

The first line of an HTTP response is a status line consisting of space-separated elements. :ref:`Table 1 <en-us_topic_0125560255__table47156901>` describes the elements in a status line.

.. _en-us_topic_0125560255__table47156901:

.. table:: **Table 1** Status line elements

   +---------------+----------------------------------------------------------------------------------+
   | Element       | Description                                                                      |
   +===============+==================================================================================+
   | HTTP-Version  | Indicates an HTTP version. OBS uses HTTP 1.1.                                    |
   +---------------+----------------------------------------------------------------------------------+
   | Status-Code   | Indicates a status code. This element describes the state of a response.         |
   +---------------+----------------------------------------------------------------------------------+
   | Reason-Phrase | Indicates a reason phrase. This element describes a status code in a short text. |
   +---------------+----------------------------------------------------------------------------------+

A status code consists of three digits. The first digit defines the type of a status code. Status codes are classified into five types based on request states, as described in :ref:`Table 2 <en-us_topic_0125560255__table46218860>`.

.. _en-us_topic_0125560255__table46218860:

.. table:: **Table 2** OBS status codes

   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | Status Code                       | Description                                                                                                                                      |
   +===================================+==================================================================================================================================================+
   | 1\ *xx*                           | Indicates that a request sent by a client has been received and is being processed by the server.                                                |
   |                                   |                                                                                                                                                  |
   |                                   | This status code is returned to inform the client must wait before the request is successfully processed.                                        |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | 2\ *xx*                           | Indicates that a request has been received, understood, and accepted.                                                                            |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | 3\ *xx*                           | Indicates that a request can be successfully processed only after being redirected.                                                              |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | 4\ *xx*                           | Indicates that a request fails to be processed due to client error. For example, a request sent by a client is invalid or uses incorrect syntax. |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | 5\ *xx*                           | Indicates that a request fails to be processed due to client error.                                                                              |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+

1\ *xx* status codes indicate a provisional response. :ref:`Table 3 <en-us_topic_0125560255__table66448310>` describes all 1\ *xx* status codes.

.. _en-us_topic_0125560255__table66448310:

.. table:: **Table 3** 1\ *xx* status codes

   +-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Status Code           | Description                                                                                                                                                   | Returned After        |
   +=======================+===============================================================================================================================================================+=======================+
   | 100 Continue          | Indicates that the initial part of the request has been received and has not yet been rejected by the server and the client should continue with its request. | -  PUT Object         |
   |                       |                                                                                                                                                               | -  POST Object        |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

2\ *xx* status codes indicate that a request has been successfully processed by the server. :ref:`Table 4 <en-us_topic_0125560255__table22235105164842>` describes all 2\ *xx* status codes.

.. _en-us_topic_0125560255__table22235105164842:

.. table:: **Table 4** 2xx status codes

   +-----------------------+--------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------+
   | Status Code           | Description                                                                                | Returned After                                                                                                                  |
   +=======================+============================================================================================+=================================================================================================================================+
   | 200 OK                | Indicates that the server has accepted a request.                                          | -  PUT Bucket                                                                                                                   |
   |                       |                                                                                            | -  HEAD Bucket                                                                                                                  |
   |                       |                                                                                            | -  GET Bucket (List Objects)                                                                                                    |
   |                       |                                                                                            | -  PUT Object                                                                                                                   |
   |                       |                                                                                            | -  GET Object                                                                                                                   |
   |                       |                                                                                            | -  HEAD Object                                                                                                                  |
   |                       |                                                                                            | -  Operations on the ACL (such as **GET Object acl**, **PUT Object acl**, **PUT Bucket acl**, and **GET Bucket acl**)           |
   |                       |                                                                                            | -  **POST** operations (Status code **200** is specified to be returned.)                                                       |
   |                       |                                                                                            | -  Restore cold objects (The object has been restored before and the expiry date has been updated.)                             |
   +-----------------------+--------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------+
   | 201 Created           | Indicates that a request response contains an XML file recording response details.         | -  **POST** operations (Status code **201** is specified to be returned.)                                                       |
   +-----------------------+--------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------+
   | 202 Accepted          | Indicates that a command for restoring a cold object is successfully delivered.            | The cold objects are not restored before the storage objects restore. After the cold objects are restored, **202** is returned. |
   +-----------------------+--------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------+
   | 204 No Content        | Indicates that the server has processed a request successfully and no content is returned. | -  **DELETE** Object                                                                                                            |
   |                       |                                                                                            | -  **DELETE** Bucket                                                                                                            |
   |                       |                                                                                            | -  **POST** operations (No status codes are specified to be returned.)                                                          |
   |                       |                                                                                            | -  **POST** operations (Status code **204** is specified to be returned.)                                                       |
   |                       |                                                                                            | -  **POST** operations (The status code specified to be returned is invalid.)                                                   |
   +-----------------------+--------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------+
   | 206 Partial Content   | Succeeded in downloading some of the objects.                                              | The message is returned after the objects with the **Range** header are successfully downloaded.                                |
   +-----------------------+--------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------+

3\ *xx* status codes indicate that a request can be successfully processed only after being redirected. :ref:`Table 5 <en-us_topic_0125560255__table20089767165948>` describes all 3\ *xx* status codes.

.. _en-us_topic_0125560255__table20089767165948:

.. table:: **Table 5** 3\ *xx* status codes

   +-----------------------+---------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------+
   | Status Code           | Description                                                                                       | Returned After                                                           |
   +=======================+===================================================================================================+==========================================================================+
   | 303 See Other         | Indicates that a client can use another URI to obtain a specific object.                          | -  **POST** operations (Redirection parameters in requests are valid.)   |
   +-----------------------+---------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------+
   | 304 Not Modified      | Indicates that the requested resource in a **GET** request is not modified at the specified time. | -  Obtaining a resource that is not modified at the specified time       |
   +-----------------------+---------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------+
   | 307 Moved Temporarily | Indicates that a request has been redirected.                                                     | -  A request is redirected after it fails to be processed by the server. |
   +-----------------------+---------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------+

4\ *xx* status codes indicate that a request fails to be processed due to a client error. When 4\ *xx* status codes are returned (except response to a *HEAD* request), the server must contain an error message with an error explanation. 4\ *xx* status codes apply to all request methods. :ref:`Table 6 <en-us_topic_0125560255__table61163879>` describes all 4\ *xx* status codes.

.. _en-us_topic_0125560255__table61163879:

.. table:: **Table 6** 4\ *xx* status codes

   +---------------------+-----------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+
   | Status Code         | Description                                                           | Returned After                                                                                  |
   +=====================+=======================================================================+=================================================================================================+
   | 400 Bad Request     | Indicates that the syntax of a request is incorrect.                  | A request in incorrect syntax or containing incorrect parameters is sent.                       |
   +---------------------+-----------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+
   | 403 Forbidden       | Indicates that a request fails to be authenticated.                   | The requested user does not exist or authentication information in a sent request is incorrect. |
   +---------------------+-----------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+
   | 404 Not Found       | Indicates that the requested resource does not exist.                 | The requested resource (such as a bucket or an object) does not exist.                          |
   +---------------------+-----------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+
   | 411 Length Required | Indicates that the **Content-Length** header is missing in a request. | A request containing no **Content-Length** header is sent.                                      |
   +---------------------+-----------------------------------------------------------------------+-------------------------------------------------------------------------------------------------+

5\ *xx* status codes indicate that a request fails to be processed due to a client error. A 5\ *xx* status code is returned together with a response body containing error details. 5\ *xx* status codes can be returned after requests using all HTTP methods (except HEAD) are sent. :ref:`Table 7 <en-us_topic_0125560255__table16341824>` describes all 5\ *xx* status codes.

.. _en-us_topic_0125560255__table16341824:

.. table:: **Table 7** 5\ *xx* status codes

   +-------------------------+-----------------------------------------------+----------------------------------------------------------------------+
   | Status Code             | Description                                   | Returned After                                                       |
   +=========================+===============================================+======================================================================+
   | 500 Internal Error      | Indicates that an error occurs on the server. | An error occurs on the server.                                       |
   +-------------------------+-----------------------------------------------+----------------------------------------------------------------------+
   | 503 Service Unavailable | Indicates that the server is overloaded.      | The server realizes that it is processing too many requests at once. |
   +-------------------------+-----------------------------------------------+----------------------------------------------------------------------+

Response Headers
----------------

Response headers are included in responses to provide additional information about servers and requested resources. :ref:`Table 8 <en-us_topic_0125560255__table53316885>` lists the response headers.

.. _en-us_topic_0125560255__table53316885:

.. table:: **Table 8** Response headers

   +------------------+------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
   | Header           | Description                                                                                                                        | Applicable To                                                                                                     |
   +==================+====================================================================================================================================+===================================================================================================================+
   | Content-Length   | Indicates the length of a response body.                                                                                           | All responses                                                                                                     |
   +------------------+------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
   | Date             | Indicates the date when a request response is returned.                                                                            | All responses                                                                                                     |
   +------------------+------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
   | x-amz-request-id | Indicates the unique identifier for an OBS request.                                                                                | All responses                                                                                                     |
   +------------------+------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
   | x-amz-id-2       | Indicates a special token that helps OBS troubleshoot faults.                                                                      | All responses                                                                                                     |
   +------------------+------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
   | x-reserved       | Indicates the copyright.                                                                                                           | All responses                                                                                                     |
   +------------------+------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
   | ETag             | Indicates the hash value of an object. The entity tag (ETag) only reflects changes to the contents of an object, not its metadata. | Responses returned after **PUT Object**, **GET Object**, and **HEAD Object** requests are successfully processed. |
   +------------------+------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
   | Last-Modified    | Indicates the date and time at which the last modification to an object is recorded.                                               | Responses returned after **GET Object** and **HEAD Object** requests are successfully processed.                  |
   +------------------+------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
   | Location         | Indicates the URI of an object.                                                                                                    | Responses returned after a **POST Object** request is successfully processed.                                     |
   +------------------+------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------+

Response Body
-------------

A response body is included in a request response under the following conditions:

-  Obtaining object content

   If a requested object is not blank, the response body is the content of the object.

-  Obtaining the ACL of a bucket or object

   The response body is the ACL of the requested bucket or object in the XML format.

-  Client error

   The response body describes the client error in detail in the XML format so that the user can perform further operations. For details, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`.

-  Server error

   The response body contains error details in the XML format.

Error Response
--------------

An error response is returned if a request is incorrect, permission is incorrect, or the requested bucket or object is not found. An error response contains error details in the XML format. The following is an example error response returned after the requested object is not found:

.. code-block::

   <Error>
    <Code>NoSuchBucket</Code>
    <Message>The specified bucket does not exist</Message>
    <RequestId>FDBD2D47937FBD89F71285474962843</RequestId>
    <HostId>RkRCRDJENDc5MzdGQkQ4OUY3MTI4NTQ3NDk2Mjg0M0FB
    QUFBQUFBYmJiYmJiYmJD</HostId>
     ……
   </Error>

:ref:`Table 9 <en-us_topic_0125560255__table127440>` describes the common elements contained in an error response.

.. _en-us_topic_0125560255__table127440:

.. table:: **Table 9** Error response elements

   ========= ==============================================================
   Element   Description
   ========= ==============================================================
   Code      A character string that uniquely identifies an error.
   Error     Container for all error elements in the XML response body.
   Message   Error details that help you read and understand an error.
   RequestId The unique ID of the request whose error response is returned.
   HostId    ID of the server that returns an error response.
   ========= ==============================================================

The preceding elements are commonly found in error responses in the XML format. To facilitate error diagnosis, most error responses also contain other elements to describe error details. For example, if the MD5 value calculated by OBS is inconsistent with that specified in a request for uploading an object, OBS returns an error response that contains both the calculated MD5 value and the user-defined MD5 value.
