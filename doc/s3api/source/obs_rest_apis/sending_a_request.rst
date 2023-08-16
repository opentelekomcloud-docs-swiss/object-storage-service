:original_name: en-us_topic_0125560363.html

.. _en-us_topic_0125560363:

Sending a Request
=================

OBS is based on a standard request and response model. A request sent to OBS must comply with HTTP 1.1 and headers of a request must contain OBS-defined parameters, for example, authentication fields.

Requests can be sent to OBS using multiple HTTP methods such as **GET**, **PUT**, **POST**, **DELETE**, and **HEAD**. You can send a **GET**, **PUT**, **POST**, **DELETE**, or **HEAD** request to read, create, update, delete, or obtain a resource. :ref:`Table 1 <en-us_topic_0125560363__table55931017>` describes the request methods supported by OBS REST APIs.

.. _en-us_topic_0125560363__table55931017:

.. table:: **Table 1** HTTP request methods supported by OBS REST APIs

   +--------+-----------------------------------------------------------------------------------------------------------------------------------------+
   | Method | Description                                                                                                                             |
   +========+=========================================================================================================================================+
   | GET    | Requests that the server returns a specific resource, for example, a bucket list or object.                                             |
   +--------+-----------------------------------------------------------------------------------------------------------------------------------------+
   | PUT    | Requests that the server creates a specific resource, for example, a bucket or object.                                                  |
   +--------+-----------------------------------------------------------------------------------------------------------------------------------------+
   | POST   | Requests that the server performs specific operations on a specific resource, for example, initiating or completing a multipart upload. |
   +--------+-----------------------------------------------------------------------------------------------------------------------------------------+
   | DELETE | Requests that the server deletes a specific resource, for example, an object.                                                           |
   +--------+-----------------------------------------------------------------------------------------------------------------------------------------+
   | HEAD   | Requests that the server returns the metadata of a specific resource, for example, object metadata.                                     |
   +--------+-----------------------------------------------------------------------------------------------------------------------------------------+

Request Headers
---------------

Parameters must be specified in the headers of requests sent to OBS using OBS REST APIs. For details about headers common to OBS REST requests, see section :ref:`Common Request Headers <en-us_topic_0125560462>`.
