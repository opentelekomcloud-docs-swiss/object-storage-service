:original_name: en-us_topic_0125560402.html

.. _en-us_topic_0125560402:

Abort Multipart Upload
======================

You can use this operation to abort a multipart upload. After the request is sent, parts associated to the multipart upload cannot be uploaded or listed.

Request Syntax
--------------

.. code-block:: text

   DELETE /ObjectName?uploadId=uplaodID HTTP/1.1
    User-Agent: agent
    Host: bucketname.obs.example.com
    Accept: */*
    Date: date
    Authorization: auth

Request Parameters
------------------

This request uses one parameter to specify the ID of the multipart upload to be completed. :ref:`Table 1 <en-us_topic_0125560402__table46411854>` describes the parameter.

.. _en-us_topic_0125560402__table46411854:

.. table:: **Table 1** Request parameter

   +-----------------------+---------------------------------------------------------+-----------------------+
   | Parameter             | Description                                             | Remarks               |
   +=======================+=========================================================+=======================+
   | uploadId              | Indicates the ID of the multipart upload to be aborted. | Mandatory             |
   |                       |                                                         |                       |
   |                       | Type: String                                            |                       |
   +-----------------------+---------------------------------------------------------+-----------------------+

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
    Server: server

Response Headers
----------------

This response uses common headers. For details about common response headers, see section :ref:`Common Response Headers <en-us_topic_0125560484>`.

Response Elements
-----------------

This response involves no elements.

Error Responses
---------------

-  If an AK or signature is invalid, OBS returns status code **403 Forbidden** and error code **AccessDenied**.
-  If the requested bucket does not exist, OBS returns status code **404 Not Found** and error code **NoSuchBucket**.
-  If the requester is neither the initiator of a multipart upload nor the bucket owner, OBS returns status code **403 Forbidden** and error code **AccessDenied**.
-  If the operation succeeded, OBS returns status code **204 No Content**.

For details about other error responses, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`.

Sample Request
--------------

.. code-block:: text

   DELETE /example-object?uploadId=VXBsb2FkIElEIGZvciBlbHZpbmcncyBteS1tb3ZpZS5tMnRzIHVwbG9hZ HTTP/1.1
    User-Agent: Jakarta Commons-HttpClient/3.1
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Mon, 1 Nov 2010 20:34:56 GMT
    Authorization: AWS AKIAIOSFODNN7EXAMPLE:0RQf3/cRonhpaBX5sCYVf1bNRuU=

Sample Response
---------------

.. code-block::

   HTTP/1.1 204 No Content
    x-amz-id-2: Weag1LuByRx9e6j5Onimru9pO4ZVKnJ2Qz7/C1NPcfTWAtRPfTaOFg==
    x-amz-request-id: 996c76696e6727732072657175657374
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Date: Mon, 1 Nov 2010 20:34:56 GMT
    Server: OBS
