:original_name: obs_04_0074.html

.. _obs_04_0074:

Configuring Bucket CORS
=======================

Functions
---------

Cross-origin resource sharing (CORS) is a standard mechanism proposed by World Wide Web Consortium (W3C) and allows cross-origin requests from clients. For standard web page requests, the scripts and contents at one website cannot interact with those at another website due to the existence of the Same Origin Policy (SOP).

OBS allows buckets to store static web resources. The buckets of OBS can serve as website resources if the buckets are properly used (for details, see :ref:`Configuring Static Website Hosting for a Bucket <obs_04_0071>`). A website in OBS can respond to requests of another websites only after CORS is properly configured.

Typical application scenarios are as follows:

-  With the support of CORS, you can use JavaScript and HTML5 to construct web applications and directly access the resources in OBS without the need to use proxy servers for transfer.
-  You can enable the dragging function of HTML 5 to directly upload files to the OBS (with the upload progress displayed) or update the OBS contents using web applications.
-  Hosts external web pages, style sheets, and HTML 5 applications in different origins. Web fonts or pictures on OBS can be shared by multiple websites.

To perform this operation, you must have the **PutBucketCORS** permission. By default, only the bucket owner can perform this operation. The bucket owner can grant the permission to other users by configuring the bucket policy or user policy.

Request Syntax
--------------

.. code-block:: text

   PUT /?cors HTTP/1.1
   Host: bucketname.obs.region.example.com
   Content-Length: length
   Date: date
   Authorization: authorization
   Content-MD5: MD5
   <?xml version="1.0" encoding="UTF-8"?>
   <CORSConfiguration>
       <CORSRule>
           <ID>id</ID>
           <AllowedMethod>method</AllowedMethod>
           <AllowedOrigin>origin</AllowedOrigin>
           <AllowedHeader>header</AllowedHeader>
           <MaxAgeSeconds>seconds</MaxAgeSeconds>
           <ExposeHeader>header</ExposeHeader>
       </CORSRule>
   </CORSConfiguration>

Request Parameters
------------------

This request contains no parameters.

Request Headers
---------------

This request uses common headers and CORS request headers. For details, see :ref:`Table 3 <obs_04_0007__table25197309>` and :ref:`Table 1 <obs_04_0074__table15021581161521>`.

.. _obs_04_0074__table15021581161521:

.. table:: **Table 1** CORS request header

   +-----------------------+------------------------------------------------------------------------+-----------------------+
   | Header                | Description                                                            | Mandatory             |
   +=======================+========================================================================+=======================+
   | Content-MD5           | Base64-encoded 128-bit MD5 digest of the message according to RFC 1864 | Yes                   |
   |                       |                                                                        |                       |
   |                       | Type: string                                                           |                       |
   |                       |                                                                        |                       |
   |                       | Example: **n58IG6hfM7vqI4K0vnWpog==**                                  |                       |
   +-----------------------+------------------------------------------------------------------------+-----------------------+

Request Elements
----------------

In this request body, you must configure the CORS rules for a bucket in XML format. :ref:`Table 2 <obs_04_0074__table35453405161544>` describes the specific configuration elements.

.. _obs_04_0074__table35453405161544:

.. table:: **Table 2** CORS configuration elements

   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Element               | Description                                                                                                                                                                                                                                                                                                                                                                                               | Mandatory             |
   +=======================+===========================================================================================================================================================================================================================================================================================================================================================================================================+=======================+
   | CORSConfiguration     | Root node of **CORSRule** and its capacity cannot exceed 64 KB.                                                                                                                                                                                                                                                                                                                                           | Yes                   |
   |                       |                                                                                                                                                                                                                                                                                                                                                                                                           |                       |
   |                       | Type: container                                                                                                                                                                                                                                                                                                                                                                                           |                       |
   |                       |                                                                                                                                                                                                                                                                                                                                                                                                           |                       |
   |                       | Parent: none                                                                                                                                                                                                                                                                                                                                                                                              |                       |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | CORSRule              | CORS rules. **CORSConfiguration** can contain a maximum of 100 rules.                                                                                                                                                                                                                                                                                                                                     | Yes                   |
   |                       |                                                                                                                                                                                                                                                                                                                                                                                                           |                       |
   |                       | Type: container                                                                                                                                                                                                                                                                                                                                                                                           |                       |
   |                       |                                                                                                                                                                                                                                                                                                                                                                                                           |                       |
   |                       | Parent: CORSConfiguration                                                                                                                                                                                                                                                                                                                                                                                 |                       |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | ID                    | Unique identifier of a rule. The value can contain a maximum of 255 characters.                                                                                                                                                                                                                                                                                                                           | No                    |
   |                       |                                                                                                                                                                                                                                                                                                                                                                                                           |                       |
   |                       | Type: string                                                                                                                                                                                                                                                                                                                                                                                              |                       |
   |                       |                                                                                                                                                                                                                                                                                                                                                                                                           |                       |
   |                       | Parent: CORSRule                                                                                                                                                                                                                                                                                                                                                                                          |                       |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | AllowedMethod         | Method allowed by a CORS rule                                                                                                                                                                                                                                                                                                                                                                             | Yes                   |
   |                       |                                                                                                                                                                                                                                                                                                                                                                                                           |                       |
   |                       | Type: string                                                                                                                                                                                                                                                                                                                                                                                              |                       |
   |                       |                                                                                                                                                                                                                                                                                                                                                                                                           |                       |
   |                       | Value options: **GET**, **PUT**, **HEAD**, **POST**, **DELETE**                                                                                                                                                                                                                                                                                                                                           |                       |
   |                       |                                                                                                                                                                                                                                                                                                                                                                                                           |                       |
   |                       | Parent: CORSRule                                                                                                                                                                                                                                                                                                                                                                                          |                       |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | AllowedOrigin         | Origins that are allowed in the CORS rule. Only English domain names are supported for configuring origins, and regular expressions can be used for matching origins. Each **AllowedOrigin** allows one wildcard character (``*``) at most.                                                                                                                                                               | Yes                   |
   |                       |                                                                                                                                                                                                                                                                                                                                                                                                           |                       |
   |                       | Type: string                                                                                                                                                                                                                                                                                                                                                                                              |                       |
   |                       |                                                                                                                                                                                                                                                                                                                                                                                                           |                       |
   |                       | Parent: CORSRule                                                                                                                                                                                                                                                                                                                                                                                          |                       |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | AllowedHeader         | Headers that are allowed in a PutBucketCORS request via the **Access-Control-Request-Headers** header. If a CORS request contains **Access-Control-Request-Headers**, this request is considered valid only when it matches the configuration of **AllowedHeader**. The match is based on regular expressions. Each **AllowedHeader** can contain at most one wildcard (``*``) and cannot contain spaces. | No                    |
   |                       |                                                                                                                                                                                                                                                                                                                                                                                                           |                       |
   |                       | Type: string                                                                                                                                                                                                                                                                                                                                                                                              |                       |
   |                       |                                                                                                                                                                                                                                                                                                                                                                                                           |                       |
   |                       | Parent: CORSRule                                                                                                                                                                                                                                                                                                                                                                                          |                       |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | MaxAgeSeconds         | The time in seconds that the client can cache CORS responses.                                                                                                                                                                                                                                                                                                                                             | No                    |
   |                       |                                                                                                                                                                                                                                                                                                                                                                                                           |                       |
   |                       | Each CORSRule can contain only one MaxAgeSeconds. It can be set to a negative value.                                                                                                                                                                                                                                                                                                                      |                       |
   |                       |                                                                                                                                                                                                                                                                                                                                                                                                           |                       |
   |                       | Type: integer                                                                                                                                                                                                                                                                                                                                                                                             |                       |
   |                       |                                                                                                                                                                                                                                                                                                                                                                                                           |                       |
   |                       | Parent: CORSRule                                                                                                                                                                                                                                                                                                                                                                                          |                       |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | ExposeHeader          | An additional header in CORS responses. The header provides additional information for clients. It cannot contain spaces.                                                                                                                                                                                                                                                                                 | No                    |
   |                       |                                                                                                                                                                                                                                                                                                                                                                                                           |                       |
   |                       | Type: string                                                                                                                                                                                                                                                                                                                                                                                              |                       |
   |                       |                                                                                                                                                                                                                                                                                                                                                                                                           |                       |
   |                       | Parent: CORSRule                                                                                                                                                                                                                                                                                                                                                                                          |                       |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

Response Syntax
---------------

::

   HTTP/1.1 status_code

   Date: date
   Content-Length: length

Response Headers
----------------

The response to the request uses common headers. For details, see :ref:`Table 1 <obs_04_0013__d0e686>`.

Response Elements
-----------------

This response contains no elements.

Error Responses
---------------

No special error responses are returned. For details about error responses, see :ref:`Table 2 <obs_04_0115__d0e843>`.

Sample Request
--------------

.. code-block:: text

   PUT /?cors HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: WED, 01 Jul 2015 03:51:52 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:lq7BGoqE9yyhdEwE6KojJ7ysVxU=
   Content-MD5: NGLzvw81f/A2C9PiGO0aZQ==
   Content-Length: 617

   <?xml version="1.0" encoding="utf-8"?>
   <CORSConfiguration>
     <CORSRule>
       <AllowedMethod>POST</AllowedMethod>
       <AllowedMethod>GET</AllowedMethod>
       <AllowedMethod>HEAD</AllowedMethod>
       <AllowedMethod>PUT</AllowedMethod>
       <AllowedMethod>DELETE</AllowedMethod>
       <AllowedOrigin>www.example.com</AllowedOrigin>
       <AllowedHeader>AllowedHeader_1</AllowedHeader>
       <AllowedHeader>AllowedHeader_2</AllowedHeader>
       <MaxAgeSeconds>100</MaxAgeSeconds>
       <ExposeHeader>ExposeHeader_1</ExposeHeader>
       <ExposeHeader>ExposeHeader_2</ExposeHeader>
     </CORSRule>
   </CORSConfiguration>

Sample Response
---------------

::

   HTTP/1.1 100 Continue
   HTTP/1.1 200 OK
   Server: OBS
   x-obs-request-id: BF26000001643627112BD03512FC94A4
   x-obs-id-2: 32AAAQAAEAABSAAgAAEAABAAAQAAEAABCSYi6wLC4bkrvuS9sqnlRjxK2a5Fe3ry
   Date: WED, 01 Jul 2015 03:51:52 GMT
   Content-Length: 0
