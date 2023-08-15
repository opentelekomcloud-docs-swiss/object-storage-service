:original_name: en-us_topic_0125560307.html

.. _en-us_topic_0125560307:

Error Responses Syntax
======================

Error Response Headers
----------------------

In an error response, header information contains:

-  Content-Type: application/xml
-  HTTP status code 3\ *xx*, 4\ *xx*, or 5\ *xx*. For details, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`.

Error Response Body
-------------------

The response body contains several elements that provide error details. The following is an example error response containing all common elements in REST error responses:

.. code-block::

   <?xml version="1.0" encoding="UTF-8"?>
    <Error>
    <Code>NoSuchKey</Code>
    <Message>The resource you requested does not exist</Message>
    <Resource>/example-bucket/object</Resource>
    <RequestId>001B21A61C6C0000013402C4616D5285</RequestId>
    <HostId>RkRCRDJENDc5MzdGQkQ4OUY3MTI4NTQ3NDk2Mjg0M0FB
    QUFBQUFBYmJiYmJiYmJD</HostId>
    </Error>

Error Response Elements
-----------------------

:ref:`Table 1 <en-us_topic_0125560307__table5435182>` describes REST response elements.

.. _en-us_topic_0125560307__table5435182:

.. table:: **Table 1** Error response elements

   +-----------+----------------------------------------------------------------------------------------------------------------------------------------+
   | Element   | Description                                                                                                                            |
   +===========+========================================================================================================================================+
   | Error     | Container of all error elements.                                                                                                       |
   +-----------+----------------------------------------------------------------------------------------------------------------------------------------+
   | Code      | A string that uniquely identifies an error. For details about error codes, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`. |
   +-----------+----------------------------------------------------------------------------------------------------------------------------------------+
   | Message   | Error details in the XML format. For details about error codes, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`.            |
   +-----------+----------------------------------------------------------------------------------------------------------------------------------------+
   | RequestId | ID of the request whose error response is returned. The ID is used for locating internal errors.                                       |
   +-----------+----------------------------------------------------------------------------------------------------------------------------------------+
   | HostId    | ID of the server that returns an error response.                                                                                       |
   +-----------+----------------------------------------------------------------------------------------------------------------------------------------+
   | Resource  | The requested resource such as a bucket or object.                                                                                     |
   +-----------+----------------------------------------------------------------------------------------------------------------------------------------+

.. note::

   Many error responses contain additional structured data, which can be easily read and understood during error diagnosis.
