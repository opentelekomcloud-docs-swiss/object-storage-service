:original_name: en-us_topic_0125560310.html

.. _en-us_topic_0125560310:

V4 Common Request
=================

A V4 common request is in the following format:

.. code-block::

   Authorization: AWS4-HMAC-SHA256 Credential=AKIAIOSFODNN7EXAMPLE/20150524/region-1/s3/aws4_request,SignedHeaders=host;range;x-amz-date,Signature=fe5f80f77d5fa3beca038a248ff027d0445342fe2855ddc963176630326f1024

.. table:: **Table 1** Request parameters

   +----------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                                                                  | Description                                                                                                                                                                                                   |
   +============================================================================+===============================================================================================================================================================================================================+
   | Authorization                                                              | Indicates signature information.                                                                                                                                                                              |
   +----------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | AWS4-HMAC-SHA256                                                           | Indicates the hash algorithm used by signatures. It is a fixed value.                                                                                                                                         |
   +----------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Credential=AKIAIOSFODNN7EXAMPLE/20150524/region-1/s3/aws4_request          | Indicates the AK and Signing Key information used to calculate the signature.                                                                                                                                 |
   |                                                                            |                                                                                                                                                                                                               |
   |                                                                            | AKIAIOSFODNN7EXAMPLE: AK of the user that sends a request.                                                                                                                                                    |
   |                                                                            |                                                                                                                                                                                                               |
   |                                                                            | 20150524: start time for calculating the Signing Key. After 7 days, the signature that is calculated by using the Signing Key is invalid. The definition of Signing Key is in the later part of the document. |
   |                                                                            |                                                                                                                                                                                                               |
   |                                                                            | region-1: Indicates the region information about the request.                                                                                                                                                 |
   |                                                                            |                                                                                                                                                                                                               |
   |                                                                            | s3: Indicates the service that is required.                                                                                                                                                                   |
   |                                                                            |                                                                                                                                                                                                               |
   |                                                                            | aws4_request: Indicates a fixed value.                                                                                                                                                                        |
   +----------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | SignedHeaders=host;range;x-amz-date                                        | SignedHeaders: Indicates the HTTP request headers that are used for signature calculation.                                                                                                                    |
   |                                                                            |                                                                                                                                                                                                               |
   |                                                                            | .. warning::                                                                                                                                                                                                  |
   |                                                                            |                                                                                                                                                                                                               |
   |                                                                            |    If headers contain *gzip*, *no-cache*, *chunked*, *identity*, *keep-alive*, *bytes*, and *close*, please use lowercase letters. Otherwise, you will receive a **SignatureDoesNotMatch** error response.    |
   +----------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Signature=fe5f80f77d5fa3beca038a248ff027d0445342fe2855ddc963176630326f1024 | The signature value of this request is **fe5f80f77d5fa3beca038a248ff027d0445342fe2855ddc963176630326f1024**.                                                                                                  |
   +----------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

:ref:`Figure 1 <en-us_topic_0125560310__fig15907824205112>` shows the signature computing process in V4 authentication mode.

.. _en-us_topic_0125560310__fig15907824205112:

.. figure:: /_static/images/en-us_image_0125560271.png
   :alt: **Figure 1** Signature calculation process in V4 authentication mode

   **Figure 1** Signature calculation process in V4 authentication mode

The signature computing process in V4 authentication mode is detailed in the following steps:

#. Generate StringToSign.

   StringToSign of a common V4 request is in the following format:

   .. code-block::

      "AWS4-HMAC-SHA256" + \n" + TimeStampISO8601Format + "\n" + <Scope> + "\n" +Hex(SHA256Hash(<CanonicalRequest>))

   Example:

   .. code-block::

      AWS4-HMAC-SHA256 20150524T000000Z 20150524/region-1/s3/aws4_request 9e0e90d9c76de8fa5b200d8c849cd5b8dc7a3be3951ddb7f6a76b4158342019d

   :ref:`Table 2 <en-us_topic_0125560310__table63418753102033>` lists parameters of Canonical Request.

   .. _en-us_topic_0125560310__table63418753102033:

   .. table:: **Table 2** Parameters of Canonical Request

      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                                                                                                                                                                                        |
      +===================================+====================================================================================================================================================================================================================================================================================================================================================================================================+
      | HTTP Method                       | Indicates the HTTP request method such as GET, PUT, or POST.                                                                                                                                                                                                                                                                                                                                       |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Canonical URI                     | Indicates the absolute path of the URI. It starts with the "/" special character. Example:                                                                                                                                                                                                                                                                                                         |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                                                    |
      |                                   | The absolute path of http://bucketname.obs.example.com/myphoto.jpg is /bucketname/myphoto.jpg.                                                                                                                                                                                                                                                                                                     |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | CanonicalQueryString              | Indicates that name and values are encoded using URI-encode and sorted in the dictionary order.                                                                                                                                                                                                                                                                                                    |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                                                    |
      |                                   | Example:                                                                                                                                                                                                                                                                                                                                                                                           |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                                                    |
      |                                   | CanonicalQueryString of http://bucketname.obs.example.com/?prefix=somePrefix&marker=someMarker&max-keys=20 is as follows:                                                                                                                                                                                                                                                                          |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                                                    |
      |                                   | URI-encode("marker")+"="+URI-encode("someMarker")+"&"+URI-encode("max-keys")+"="+URI-encode("20")+"&"+URI-encode("prefix")+"="+URI-encode("somePrefix")                                                                                                                                                                                                                                            |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                                                    |
      |                                   | If a parameter of the querystring request does not have a value, enter the value in the "" format. The following is an example:                                                                                                                                                                                                                                                                    |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                                                    |
      |                                   | CanonicalQueryString of http://bucketname.obs.example.com/?acl is as follows:                                                                                                                                                                                                                                                                                                                      |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                                                    |
      |                                   | URI-encode("acl") + "=" + ""                                                                                                                                                                                                                                                                                                                                                                       |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Canonical Headers                 | Indicates the request header list. The name and value of each header are connected using a colon (:). Headers are separated by **\\n**. The name of a header must use lowercase letters. The list is sorted in the dictionary order.                                                                                                                                                               |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                                                    |
      |                                   | Canonical Headers are constructed using the value of SignedHeaders=date;host;x-amz-content-sha256;x-amz-date;x-amz-storage-class in the **Authentication** field of the HTTP header. In this example, the server uses date, host, x-amz-content-sha256, x-amz-date, and xamz-storage-class to calculate signatures. OBS must extract the five fields from the HTTP header to calculate signatures. |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                                                    |
      |                                   | Host: bucketname..obs.example.com                                                                                                                                                                                                                                                                                                                                                                  |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                                                    |
      |                                   | Date: Fri, 24 May 2015 00:00:00 GMT                                                                                                                                                                                                                                                                                                                                                                |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                                                    |
      |                                   | x-amz-content-sha256: 44ce7dd67c959e0d3524ffac1771dfbba87d2b6b4b4e99e42034a8b803f8b072                                                                                                                                                                                                                                                                                                             |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                                                    |
      |                                   | x-amz-date: 20150524T000000Z                                                                                                                                                                                                                                                                                                                                                                       |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                                                    |
      |                                   | x-amz-storage-class: STANDARD                                                                                                                                                                                                                                                                                                                                                                      |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | SignedHeaders                     | Indicates the name that can be used to calculate signature headers. The names are sorted in the dictionary order. Fields are separated from each other by a semicolon (;).                                                                                                                                                                                                                         |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                                                    |
      |                                   | Example:                                                                                                                                                                                                                                                                                                                                                                                           |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                                                    |
      |                                   | date;host;x-amz-content-sha256;x-amz-date;x-amz-storage-class                                                                                                                                                                                                                                                                                                                                      |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Hashed Payload                    | Indicates the SHA256 hash value of the data that is uploaded.                                                                                                                                                                                                                                                                                                                                      |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   The following is a Canonical Request example.

   .. code-block:: text

      PUT /test%24file.text date:Fri, 24 May 2015 00:00:00 GMT
      host:bucketname.obs.example.com
      x-amz-content-sha256:44ce7dd67c959e0d3524ffac1771dfbba87d2b6b4b4e99e42034a8b803f8b072 x-amz-date:20150524T000000Z x-amz-storage-class:STANDARD date;host;x-amz-content-sha256;x-amz-date;x-amz-storage-class 44ce7dd67c959e0d3524ffac1771dfbba87d2b6b4b4e99e42034a8b803f8b072

#. Generate SigningKey.

   SigningKey is calculated as follows:

   .. code-block::

      DateKey = HMAC-SHA256("AWS4"+"<SecretAccessKey>", "<yyyymmdd>")
      DateRegionKey = HMAC-SHA256(<DateKey>, "<aws-region>")
      DateRegionServiceKey = HMAC-SHA256(<DateRegionKey>, "<aws-service>")
      SigningKey = HMAC-SHA256(<DateRegionServiceKey>, "aws4_request")

   Each field is described as follows:

   -  **<SecretAccessKey>**: Indicates the SK of the requester.

   -  *<yyyymmdd>*: Indicates the period in which Signing Key obtained from Authorization in the HTTP header is valid.

   -  **<aws-region>**: Indicates the region of the request.

   -  **<aws-service>**: Indicates the service type of the request.

#. Use StringToSign and SigningKey to calculate the signature.

.. code-block::

   HMAC-SHA256(SigningKey, StringToSign)

After the HMAC-SHA256 algorithm is used to calculate the signature, convert the signature into a hexadecimal code to get the ultimate signature.

The common request authentication involves a special authentication method known as chunked uploading authentication. You can use this method when authenticating objects uploaded in a chunked manner.

Chunked uploading indicates that the data flows are composed of data blocks. Each data block is called a chunk. Each chunk consists of chunk metadata and chunk data. Chunk metadata includes the size and signature of the current chunk data. The chunk format is as follows:

.. code-block::

   chunk-size + ";chunk-signature=" + signature + \r\n + chunk-data + \r\n

:ref:`Figure 2 <en-us_topic_0125560310__fig727315155523>` shows the signature computing process of each chunk.

.. _en-us_topic_0125560310__fig727315155523:

.. figure:: /_static/images/en-us_image_0125560434.png
   :alt: **Figure 2** Signature calculation process of each chunk

   **Figure 2** Signature calculation process of each chunk

Chunk signature calculation is an iterative process. The signature of each chunk is calculated based on the previous chunk signature. For the first chunk, its previous chunk signature is the seed signature in the header.

After OBS receives the object uploading request, OBS verifies the signature in the request header and then verifies the signature of each chunk when user data is uploaded. Objects are uploaded successfully only after the header signature and each chunk signature are verified.
