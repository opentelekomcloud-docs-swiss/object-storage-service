:original_name: en-us_topic_0125560243.html

.. _en-us_topic_0125560243:

V2 Common Request
=================

A common HTTP/HTTPS request is authenticated by its **Authorization** header. The following is the format of the **Authorization** header:

.. code-block::

   Authorization: AWS AccessKeyID:signature

To generate the signature, perform the following steps:

#. Construct **StringToSign** using request parameters.

   .. code-block::

      StringToSign = HTTP-Verb + "\n" + Content-MD5 + "\n" + Content-Type + "\n" + Date + "\n" + CanonicalizedOBSHeaders + CanonicalizedResource

   :ref:`Table 1 <en-us_topic_0125560243__table41134075>` describes the parameters of a request.

   .. _en-us_topic_0125560243__table41134075:

   .. table:: **Table 1** Request parameters

      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
      +===================================+===============================================================================================================================================================================================================================================================================================================================================================================================================================================================+
      | HTTP-Verb                         | Indicates an HTTP request method supported by OBS REST API. The value can be an HTTP verb such as PUT, GET, or DELETE.                                                                                                                                                                                                                                                                                                                                        |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Date                              | Indicates the time when the request is initiated. The value must be in RFC 1123 format. This parameter is an empty string when the **x-amz-date** is specified. For details, see :ref:`Table 3 <en-us_topic_0125560243__table25172842>`.                                                                                                                                                                                                                      |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
      |                                   | This parameter can be omitted if the request is for a temporarily authorized operation.                                                                                                                                                                                                                                                                                                                                                                       |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Content-Type                      | Indicates the content type and is used for specifying the request content type, for example, **text/plain**.                                                                                                                                                                                                                                                                                                                                                  |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
      |                                   | This parameter is an empty string when the request does not contain the header. See :ref:`Table 2 <en-us_topic_0125560243__table54992765>`.                                                                                                                                                                                                                                                                                                                   |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Content-MD5                       | The MD5 digest string of the message body is calculated according to the RFC 1864 standard. That is, calculate the 128-bit binary array (the message header data encrypted with MD5) first, and then use Base 64 encoding to convert the binary data to a character string.                                                                                                                                                                                   |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | CanonicalizedOBSHeaders           | Indicates an OBS-defined header prefixed with **x-amz-**, for example, **x-amz-date** or **x-amz-acl**.                                                                                                                                                                                                                                                                                                                                                       |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
      |                                   | 1. All characters in the OBS-defined header must be converted to lower-case letters. If a request contains multiple OBS-defined headers, the headers are organized in a dictionary order.                                                                                                                                                                                                                                                                     |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
      |                                   | 2. If multiple OBS-defined headers in a request have the same prefix, combine the headers into one. For example, if headers **x-amz-meta-name:name1** and **x-amz-meta-name:name2** are added, combine the headers to **x-amze-meta-name:name1,name2**.                                                                                                                                                                                                       |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
      |                                   | 3. If an OBS-defined header contains non-ASCII or unrecognizable characters, the header must be Base64 encoded.                                                                                                                                                                                                                                                                                                                                               |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
      |                                   | 4. An OBS-defined header contains spaces or tabs only when necessary. Unnecessary spaces must be omitted. For example, **x-amz-meta-name: name** must be changed to **x-amz-meta-name:name**. The space between **x-amz-meta-name:** and **name** is omitted.                                                                                                                                                                                                 |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
      |                                   | 5. Each OBS-defined header occupies a separate line. For details, see :ref:`Table 4 <en-us_topic_0125560243__table25228990>`.                                                                                                                                                                                                                                                                                                                                 |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | CanonicalizedResource             | Indicates a requested resource. This parameter is constructed as follows:                                                                                                                                                                                                                                                                                                                                                                                     |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
      |                                   | ["/" + Bucket ] + <HTTP-Request-URI, ["/" + object name]> + [subresource].                                                                                                                                                                                                                                                                                                                                                                                    |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
      |                                   | [subresource] is mandatory if any subresource exists.                                                                                                                                                                                                                                                                                                                                                                                                         |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
      |                                   | In virtual-style requests, the bucket name is required. In other requests, the bucket name is not required. For details, see :ref:`Table 2 <en-us_topic_0125560243__table54992765>`.                                                                                                                                                                                                                                                                          |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
      |                                   | If a subresource (such as **?acl** and **?logging**) exists, the subresource must be added. The subresource includes **acl**, **lifecycle**, **location**, **logging**, **notification**, **partNumber**, **policy**, **uploadId**, **uploads**, **versionId**, **versioning**, **versions**, **website**, **quota**, **storagePolicy**, **storageinfo**, and **deletebucket**. For details, see :ref:`Table 5 <en-us_topic_0125560243__table4097412592916>`. |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   Note that the calculation method of Content-MD5 is to first calculate the binary array encrypted by MD5, and then perform Base-64 encoding for the binary array, instead of directly encoding the 32-bit character string. The following is an example of the Java code used to calculate the Content-MD5 value:

   .. code-block::

      MessageDigest md = MessageDigest.getInstance("MD5");
      md.update(buffer);
      byte[] digests = md.digest();
      String md5 = Base64.encode(digests);

   In the code, buffer stands for the byte stream of the message body, and digests stands for the 128-bit binary array calculated from the message body with MD5. Then the binary data is converted to the correct Content-MD5 value by Base-64 encoding.

   :ref:`Table 2 <en-us_topic_0125560243__table54992765>` lists example **StringToSign**.

   .. _en-us_topic_0125560243__table54992765:

   .. table:: **Table 2** StringToSign generated for GET Object ACL

      +-------------------------------------+-----------------------------------+
      | Request Header                      | StringToSign                      |
      +=====================================+===================================+
      | GET /object.txt HTTP/1.1            | GET \\n                           |
      |                                     |                                   |
      | Host: bucketname.obs.example.com    | ``\n``                            |
      |                                     |                                   |
      | Date: Sat, 12 Oct 2015 08:12:38 GMT | Sat, 12 Oct 2015 08:12:38 GMT\\n  |
      |                                     |                                   |
      |                                     | /bucket/object.txt                |
      +-------------------------------------+-----------------------------------+

   .. _en-us_topic_0125560243__table25172842:

   .. table:: **Table 3** StringToSign generated for a PUT Object request containing OBS-defined headers (1)

      +------------------------------------------+---------------------------------------------+
      | Request Header                           | StringToSign                                |
      +==========================================+=============================================+
      | PUT /object.txt HTTP/1.1                 | PUT\\n                                      |
      |                                          |                                             |
      | User-Agent: curl/7.15.5                  | ``\n``                                      |
      |                                          |                                             |
      | Host: bucketname.obs.example.com         | ``\n``                                      |
      |                                          |                                             |
      | x-amz-date:Tue, 15 Oct 2015 07:20:09 GMT | x-amz-date:Tue, 15 Oct 2015 07:20:09 GMT\\n |
      |                                          |                                             |
      | content-type: text/plain                 | /bucket/object.txt                          |
      |                                          |                                             |
      | Content-Length: 5913339                  |                                             |
      +------------------------------------------+---------------------------------------------+

   .. _en-us_topic_0125560243__table25228990:

   .. table:: **Table 4** StringToSign generated for a PUT Object request containing OBS-defined headers (2)

      +-------------------------------------+-----------------------------------+
      | Request Header                      | StringToSign                      |
      +=====================================+===================================+
      | PUT /object.txt HTTP/1.1            | PUT\\n                            |
      |                                     |                                   |
      | User-Agent: curl/7.15.5             | ``\n``                            |
      |                                     |                                   |
      | Host: bucketname.obs.example.com    | text/plain\\n                     |
      |                                     |                                   |
      | Date: Mon, 14 Oct 2015 12:08:34 GMT | ``\n``                            |
      |                                     |                                   |
      | x-amz-acl: public-read              | Mon, 14 Oct 2015 12:08:34 GMT\\n  |
      |                                     |                                   |
      | content-type: text/plain            | x-amz-acl:public-read\\n          |
      |                                     |                                   |
      | Content-Length: 5913339             | /bucket/object.txt                |
      +-------------------------------------+-----------------------------------+

   .. _en-us_topic_0125560243__table4097412592916:

   .. table:: **Table 5** StringToSign generated for GET Object ACL

      +-------------------------------------+-----------------------------------+
      | Request Header                      | StringToSign                      |
      +=====================================+===================================+
      | GET /object.txt?acl HTTP/1.1        | GET \\n                           |
      |                                     |                                   |
      | Host: bucketname.obs.example.com    | ``\n``                            |
      |                                     |                                   |
      | Date: Sat, 12 Oct 2015 08:12:38 GMT | Sat, 12 Oct 2015 08:12:38 GMT\\n  |
      |                                     |                                   |
      |                                     | /bucket/object.txt?acl            |
      +-------------------------------------+-----------------------------------+

#. Generate the signature using **StringToSign** and the SK.

   Use the hash-based message authentication code (HMAC) algorithm to calculate the signature.

   .. code-block::

      Signature = Base64( HMAC-SHA1( UTF-8-Encoding-Of(YourSecretAccessKeyID, StringToSign ) ) )
