:original_name: en-us_topic_0125560343.html

.. _en-us_topic_0125560343:

Server-Side Encryption
======================

Users can upload and download objects in common mode or using server-side encryption.

Object Storage Service (OBS) supports server-side encryption.

Users can implement this function based on various the key management types to meet site requirements. OBS supports two server-side encryption modes:

-  Server-side encryption with KMS-managed keys (SSE-KMS).
-  Server-side encryption with customer-provided keys (SSE-C).

In SSE-KMS mode, OBS uses the keys provided by Key Management Service (KMS) for server-side encryption.

In SSE-C mode, OBS uses the keys and MD5 values provided by customers for server-side encryption.

When server-side encryption is used, the returned ETag value is not the MD5 value of the object. When server-side encryption is used to upload an object, the server does not verify the imported Content-MD5 value.

-  :ref:`SSE-KMS <en-us_topic_0125560445>`
-  :ref:`SSE-C <en-us_topic_0125560282>`
-  :ref:`Interfaces Related to Server-Side Encryption <en-us_topic_0125560285>`

.. toctree::
   :maxdepth: 1
   :hidden: 

   sse-kms
   sse-c
   interfaces_related_to_server-side_encryption
