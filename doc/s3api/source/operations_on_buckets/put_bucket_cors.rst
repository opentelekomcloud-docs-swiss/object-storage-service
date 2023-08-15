:original_name: en-us_topic_0125560238.html

.. _en-us_topic_0125560238:

PUT Bucket CORS
===============

You can use this operation to enable Cross-origin resource sharing (CORS) for specified buckets.

CORS is a standard mechanism proposed by the World Wide Web Consortium (W3C) that allows cross-origin requests from servers. For standard web page requests, the scripts and contents at one website cannot interact with those at another website due to the existence of the same origin policy (SOP).

OBS allows buckets to store static web resources. The buckets of OBS can serve as website resources if the buckets are properly used. For details, see section :ref:`PUT Bucket website <en-us_topic_0125560321>`. A website in OBS can respond to requests of another websites only after the CORS is properly configured.

Typical application scenarios are as follows:

-  With the support of the CORS, you can use JavaScript and HTML 5 to construct web applications and directly access the resources in OBS without the need to use proxy servers for transfer.
-  You can enable the dragging function of HTML 5 to directly upload files to OBS (with the upload progress displayed) or update OBS contents using web applications.
-  You can host external web pages, style sheets, and HTML 5 applications in different domains. Web fonts or pictures on OBS can be shared by multiple websites.

Only users granted the **s3:PutBucketCORS** permission can perform this operation. By default, only the bucket owner can perform this operation. The bucket owner can allow other users to perform this operation by granting them the permission. After the bucket CORS configuration is set, it will take effect within 2 minutes.

Request Syntax
--------------

.. code-block:: text

   PUT /?cors HTTP/1.1
    Host: bucketname.obs.example.com
    User-Agent: agent
    Accept: */*
    Date: date
    Authorization: authorization
    Content-MD5: MD5
    Content-Length: length
    Expect: expect

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

This request involves no parameters.

Request Headers
---------------

:ref:`Table 1 <en-us_topic_0125560238__table52047770>` lists the request header.

.. _en-us_topic_0125560238__table52047770:

.. table:: **Table 1** CORS request header

   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | Header                | Description                                                                                                                                                                                                                                                                 | Remarks                                                                          |
   +=======================+=============================================================================================================================================================================================================================================================================+==================================================================================+
   | Content-MD5           | The MD5 digest string of the message body is calculated according to the RFC 1864 standard. That is, calculate the 128-bit binary array (the message header data encrypted with MD5) first, and then use Base 64 encoding to convert the binary data to a character string. | Mandatory                                                                        |
   |                       |                                                                                                                                                                                                                                                                             |                                                                                  |
   |                       | Type: String                                                                                                                                                                                                                                                                |                                                                                  |
   |                       |                                                                                                                                                                                                                                                                             |                                                                                  |
   |                       | Example: n58IG6hfM7vqI4K0vnWpog==                                                                                                                                                                                                                                           |                                                                                  |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | x-amz-security-token  | Header field used to identify the request of a federated user. When the federal authentication function is enabled, users sending such requests are identified as federated users.                                                                                          | Optional. This parameter must be carried in the request sent by federated users. |
   |                       |                                                                                                                                                                                                                                                                             |                                                                                  |
   |                       | Type: string                                                                                                                                                                                                                                                                |                                                                                  |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+

Request Elements
----------------

In this request, you must configure the CORS of buckets in the request body. The configuration information is uploaded in the XML format. :ref:`Table 2 <en-us_topic_0125560238__table65776751>` lists the CORS configuration elements.

.. _en-us_topic_0125560238__table65776751:

.. table:: **Table 2** CORS configuration elements

   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Element               | Description                                                                                                                                                                                                                                                                                                           | Remarks               |
   +=======================+=======================================================================================================================================================================================================================================================================================================================+=======================+
   | CORSConfiguration     | Indicates the **CORSRules** root node. The maximum size is 64 KB.                                                                                                                                                                                                                                                     | Mandatory             |
   |                       |                                                                                                                                                                                                                                                                                                                       |                       |
   |                       | Type: Container                                                                                                                                                                                                                                                                                                       |                       |
   |                       |                                                                                                                                                                                                                                                                                                                       |                       |
   |                       | Ancestor: None                                                                                                                                                                                                                                                                                                        |                       |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | CORSRule              | Indicates a CORS rule. **CORSConfiguration** can contain a maximum of 100 rules.                                                                                                                                                                                                                                      | Mandatory             |
   |                       |                                                                                                                                                                                                                                                                                                                       |                       |
   |                       | Type: Container                                                                                                                                                                                                                                                                                                       |                       |
   |                       |                                                                                                                                                                                                                                                                                                                       |                       |
   |                       | Ancestor: **CORSConfiguration**                                                                                                                                                                                                                                                                                       |                       |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | ID                    | Indicates the unique identifier of a rule. The value can contain a maximum of 255 characters.                                                                                                                                                                                                                         | Optional              |
   |                       |                                                                                                                                                                                                                                                                                                                       |                       |
   |                       | Type: String                                                                                                                                                                                                                                                                                                          |                       |
   |                       |                                                                                                                                                                                                                                                                                                                       |                       |
   |                       | Ancestor: Rule                                                                                                                                                                                                                                                                                                        |                       |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | AllowedMethod         | Indicates a method that is allowed by a CORS rule.                                                                                                                                                                                                                                                                    | Mandatory             |
   |                       |                                                                                                                                                                                                                                                                                                                       |                       |
   |                       | Type: String                                                                                                                                                                                                                                                                                                          |                       |
   |                       |                                                                                                                                                                                                                                                                                                                       |                       |
   |                       | Valid values: **GET**, **PUT**, **HEAD**, **POST**, and **DELETE**                                                                                                                                                                                                                                                    |                       |
   |                       |                                                                                                                                                                                                                                                                                                                       |                       |
   |                       | Ancestor: Rule                                                                                                                                                                                                                                                                                                        |                       |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | AllowedOrigin         | Indicates an origin that is allowed by a CORS rule. It is a character string and can contain a wildcard (``*``). Each **AllowedOrigin** can only contain one wildcard (``*``).                                                                                                                                        | Mandatory             |
   |                       |                                                                                                                                                                                                                                                                                                                       |                       |
   |                       | Type: String                                                                                                                                                                                                                                                                                                          |                       |
   |                       |                                                                                                                                                                                                                                                                                                                       |                       |
   |                       | Ancestor: Rule                                                                                                                                                                                                                                                                                                        |                       |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | AllowedHeader         | Indicates an allowed header (**Access-Control-Request-Headers**) in a CORS request. If a request contains **Access-Control-Request-Headers**, only a CORS request that matches the configuration of **AllowedHeader** is considered as a valid request. Each **AllowedHeader** can only contain one wildcard (``*``). | Optional              |
   |                       |                                                                                                                                                                                                                                                                                                                       |                       |
   |                       | Type: String                                                                                                                                                                                                                                                                                                          |                       |
   |                       |                                                                                                                                                                                                                                                                                                                       |                       |
   |                       | Ancestor: Rule                                                                                                                                                                                                                                                                                                        |                       |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | MaxAgeSeconds         | Indicates the response time of the CORS that can be cached by a server. It is expressed in seconds.                                                                                                                                                                                                                   | Optional              |
   |                       |                                                                                                                                                                                                                                                                                                                       |                       |
   |                       | Each **CORSRule** can contain only one **MaxAgeSeconds**. It can be set to a negative value.                                                                                                                                                                                                                          |                       |
   |                       |                                                                                                                                                                                                                                                                                                                       |                       |
   |                       | Type: Integer                                                                                                                                                                                                                                                                                                         |                       |
   |                       |                                                                                                                                                                                                                                                                                                                       |                       |
   |                       | Ancestor: Rule                                                                                                                                                                                                                                                                                                        |                       |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | ExposeHeader          | Indicates a supplemented header in CORS responses. The header provides additional information for servers. It cannot contain spaces.                                                                                                                                                                                  | Optional              |
   |                       |                                                                                                                                                                                                                                                                                                                       |                       |
   |                       | Type: String                                                                                                                                                                                                                                                                                                          |                       |
   |                       |                                                                                                                                                                                                                                                                                                                       |                       |
   |                       | Ancestor: Rule                                                                                                                                                                                                                                                                                                        |                       |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

Response Syntax
---------------

.. code-block::

   HTTP/1.1 status_code
    Server: Server Name
    x-amz-request-id: request id
    x-amz-id-2: id
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Date: date
    Content-Length: 0

Response Headers
----------------

This response uses common headers. For details about common response headers, see section :ref:`Common Response Headers <en-us_topic_0125560484>`.

Response Elements
-----------------

This response involves no elements.

Error Responses
---------------

No special error responses are returned. For details about error responses, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`.

Sample Request
--------------

.. code-block:: text

   PUT /?cors HTTP/1.1
    User-Agent: curl/7.19.0 (x86_64-suse-linux-gnu) libcurl/7.19.0 OpenSSL/0.9.8{ zlib/1.2.3 libidn/1.10
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Tue, 28 Apr 2015 08:56:07 +0000
    Authorization:  AWS D13E0C94E722DD69423C:QhHpU6Amg/2r6wIYdU3RXIx7Tlc=
    Content-MD5: x3R4DBZgOrwsI6DwztrQCg==
    Content-Length: 468
   <CORSConfiguration>
      <CORSRule>
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

Sample Response
---------------

.. code-block::

   HTTP/1.1 200 OK
    Server: OBS
    x-amz-request-id: C2D2F581B3C5AF6C6698322AB56836F6
    x-amz-id-2: lDGZAj4h+A33eYauDCTsPvFSHzBXEtZon6Eg1idIZl18/2/odotyqJUJ/lTh80uA
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Date: Tue, 28 Apr 2015 08:56:07 GMT
    Content-Length: 0
