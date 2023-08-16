:original_name: en-us_topic_0125560431.html

.. _en-us_topic_0125560431:

V2 Temporarily Authorized Request
=================================

Requests for temporarily authorized operations are authenticated using the query-string parameters instead of the **authorization** header.

In OBS, a registered and activated user can use its account to create a URL that contains authentication information. In addition, any user that obtains the URL can perform the operation specified by the URL.

For example, during temporarily authorized Get Object request, a specific URL is created and any user obtaining this URL can get the specified object before the expired time.

.. code-block:: text

   GET /ObjectKey?AWSAccessKeyId=AccessKeyID&Expires=ExpiresValue&Signature=signature HTTP/ 1.1
   Host: bucketname.obs.example.com

The required authentication elements are specified as query string parameters detailed in :ref:`Table 1 <en-us_topic_0125560431__table38455150>`.

.. _en-us_topic_0125560431__table38455150:

.. table:: **Table 1** Request parameters

   +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Parameter             | Description                                                                                                                                                                                    | Remarks               |
   +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | AWSAccessKeyId        | Indicates the AK of the permission grantor.                                                                                                                                                    | Mandatory             |
   |                       |                                                                                                                                                                                                |                       |
   |                       | Type: String                                                                                                                                                                                   |                       |
   +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Expires               | Indicates the time (expressed in seconds) when the temporarily authorized URL expires. The time must be in Coordinated Universal Time (UTC) format and later than 00:00:00 on January 1, 1970. | Mandatory             |
   |                       |                                                                                                                                                                                                |                       |
   |                       | Type: String                                                                                                                                                                                   |                       |
   +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Signature             | Indicates the signature generated using the SK and parameter **Expires**.                                                                                                                      | Mandatory             |
   |                       |                                                                                                                                                                                                |                       |
   |                       | Type: String                                                                                                                                                                                   |                       |
   +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

The query-string authentication differs from the authorization header authentication in the following aspects:

-  The signature is both Base64 and URL encoded.
-  **Expires** in **StringToSign** corresponds to **Date** in authorization information.

.. code-block::

   StringToSign = HTTP-Verb + "\n" + Content-MD5 + "\n" + Content-Type + "\n" + Expire + "\n" + CanonicalizedOBSHeaders + CanonicalizedResource.

    Signature = URL-Encode(Base64( HMAC-SHA1( UTF-8-Encoding-Of(YourSecretAccessKeyID, StringToSign ) ) )).
