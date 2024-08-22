:original_name: obs_04_0075.html

.. _obs_04_0075:

Obtaining the CORS Configuration of a Bucket
============================================

Functions
---------

You can perform this operation to obtain CORS configuration information about a specified bucket.

To perform this operation, you must have the **GetBucketCORS** permission. By default, only the bucket owner can perform this operation. The bucket owner can grant the permission to other users by configuring the bucket policy or user policy.

Request Syntax
--------------

.. code-block:: text

   GET /?cors HTTP/1.1
   Host: bucketname.obs.region.example.com
   Date: date
   Authorization: authorization

Request Parameters
------------------

This request contains no message parameters.

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
   Content-Type:  application/xml
   Date: date
   Content-Length: length

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <CORSConfiguration xmlns="http://obs.region.example.com/doc/2015-06-30/">
       <CORSRule>
           ...
       </CORSRule>
   </CORSConfiguration>

Response Headers
----------------

The response to the request uses common headers. For details, see :ref:`Table 1 <obs_04_0013__d0e686>`.

Response Elements
-----------------

This response contains elements to detail the configuration. :ref:`Table 1 <obs_04_0075__table2259502317110>` describes the elements.

.. _obs_04_0075__table2259502317110:

.. table:: **Table 1** CORS configuration elements

   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Element                           | Description                                                                                                                                                                                                                                                                                                                                                                 |
   +===================================+=============================================================================================================================================================================================================================================================================================================================================================================+
   | CORSConfiguration                 | Root node of **CORSRules** and its capacity cannot exceed 64 KB.                                                                                                                                                                                                                                                                                                            |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                             |
   |                                   | Type: container                                                                                                                                                                                                                                                                                                                                                             |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                             |
   |                                   | Parent: none                                                                                                                                                                                                                                                                                                                                                                |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | CORSRule                          | CORS rule. CORSConfiguration can contain a maximum of 100 rules.                                                                                                                                                                                                                                                                                                            |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                             |
   |                                   | Type: container                                                                                                                                                                                                                                                                                                                                                             |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                             |
   |                                   | Parent: CORSConfiguration                                                                                                                                                                                                                                                                                                                                                   |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ID                                | Unique identifier of a rule. The value can contain a maximum of 255 characters.                                                                                                                                                                                                                                                                                             |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                             |
   |                                   | Type: string                                                                                                                                                                                                                                                                                                                                                                |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                             |
   |                                   | Parent: CORSRule                                                                                                                                                                                                                                                                                                                                                            |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | AllowedMethod                     | Method allowed by a CORS rule.                                                                                                                                                                                                                                                                                                                                              |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                             |
   |                                   | Type: string                                                                                                                                                                                                                                                                                                                                                                |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                             |
   |                                   | Value options: **GET**, **PUT**, **HEAD**, **POST**, **DELETE**                                                                                                                                                                                                                                                                                                             |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                             |
   |                                   | Parent: CORSRule                                                                                                                                                                                                                                                                                                                                                            |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | AllowedOrigin                     | Indicates an origin that is allowed by a CORS rule. It is a character string and can contain a wildcard (``*``), and allows one wildcard character (``*``) at most.                                                                                                                                                                                                         |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                             |
   |                                   | Type: string                                                                                                                                                                                                                                                                                                                                                                |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                             |
   |                                   | Parent: CORSRule                                                                                                                                                                                                                                                                                                                                                            |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | AllowedHeader                     | Indicates which headers are allowed in a PUT Bucket CORS request via the **Access-Control-Request-Headers** header. If a request contains **Access-Control-Request- Headers**, only a CORS request that matches the configuration of AllowedHeader is considered as a valid request. Each AllowedHeader can contain at most one wildcard (``*``) and cannot contain spaces. |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                             |
   |                                   | Type: string                                                                                                                                                                                                                                                                                                                                                                |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                             |
   |                                   | Parent: CORSRule                                                                                                                                                                                                                                                                                                                                                            |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | MaxAgeSeconds                     | Response time of CORS that can be cached by a client. It is expressed in seconds.                                                                                                                                                                                                                                                                                           |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                             |
   |                                   | Each CORSRule can contain only one MaxAgeSeconds. It can be set to a negative value.                                                                                                                                                                                                                                                                                        |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                             |
   |                                   | Type: integer                                                                                                                                                                                                                                                                                                                                                               |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                             |
   |                                   | Parent: CORSRule                                                                                                                                                                                                                                                                                                                                                            |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ExposeHeader                      | Indicates a supplemented header in CORS responses. The header provides additional information for clients. It cannot contain spaces.                                                                                                                                                                                                                                        |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                             |
   |                                   | Type: string                                                                                                                                                                                                                                                                                                                                                                |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                             |
   |                                   | Parent: CORSRule                                                                                                                                                                                                                                                                                                                                                            |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Error Responses
---------------

:ref:`Table 2 <obs_04_0075__table2262289217914>` describes possible special errors in this request.

.. _obs_04_0075__table2262289217914:

.. table:: **Table 2** Special error

   +-------------------------+------------------------------------------------------------------+------------------+
   | Error Code              | Description                                                      | HTTP Status Code |
   +=========================+==================================================================+==================+
   | NoSuchCORSConfiguration | Indicates that the CORS configuration of buckets does not exist. | 404 Not Found    |
   +-------------------------+------------------------------------------------------------------+------------------+

For other errors, see :ref:`Table 2 <obs_04_0115__d0e843>`.

Sample Request
--------------

.. code-block:: text

   GET /?cors HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: WED, 01 Jul 2015 03:54:36 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:WJGghTrPQQXRuCx5go1fHyE+Wwg=

Sample Response
---------------

::

   HTTP/1.1 200 OK
   Server: OBS
   x-obs-request-id: BF2600000164363593F10738B80CACBE
   x-obs-id-2: 32AAAQAAEAABAAAQAAEAABAAAQAAEAABCSpngvwC5TskcLGh7Fz5KRmCFIayuY8p
   Content-Type: application/xml
   Date: WED, 01 Jul 2015 03:54:36 GMT
   Content-Length: 825

   <?xml version="1.0" encoding="utf-8"?>
   <CORSConfiguration xmlns="http://obs.region.example.com/doc/2015-06-30/">
     <CORSRule>
       <ID>783fc6652cf246c096ea836694f71855</ID>
       <AllowedMethod>POST</AllowedMethod>
       <AllowedMethod>GET</AllowedMethod>
       <AllowedMethod>HEAD</AllowedMethod>
       <AllowedMethod>PUT</AllowedMethod>
       <AllowedMethod>DELETE</AllowedMethod>

       <AllowedOrigin>obs.example.com</AllowedOrigin>
       <AllowedOrigin>www.example.com</AllowedOrigin>
       <AllowedHeader>AllowedHeader_1</AllowedHeader>
       <AllowedHeader>AllowedHeader_2</AllowedHeader>
       <MaxAgeSeconds>100</MaxAgeSeconds>
       <ExposeHeader>ExposeHeader_1</ExposeHeader>
       <ExposeHeader>ExposeHeader_2</ExposeHeader>
     </CORSRule>
   </CORSConfiguration>
