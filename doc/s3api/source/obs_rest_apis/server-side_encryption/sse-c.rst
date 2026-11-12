:original_name: en-us_topic_0125560282.html

.. _en-us_topic_0125560282:

SSE-C
=====

In SSE-C mode, OBS uses the keys and MD5 values provided by customers for server-side encryption.

OBS does not store your encryption keys. If you lost your encryption keys, you lost the objects. Six headers are added to support SSE-C.

:ref:`Table 1 <en-us_topic_0125560282__table44557321113316>` lists headers that are mandatory when you use SSE-C to encrypt objects.

.. _en-us_topic_0125560282__table44557321113316:

.. table:: **Table 1** Mandatory headers in SSE-C mode

   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Header                                          | Description                                                                                                                                                                                                                                              |
   +=================================================+==========================================================================================================================================================================================================================================================+
   | x-amz-server-side-encryption-customer-algorithm | Indicates the algorithm used to encrypt an object. The header is used in SSE-C mode.                                                                                                                                                                     |
   |                                                 |                                                                                                                                                                                                                                                          |
   |                                                 | Example:                                                                                                                                                                                                                                                 |
   |                                                 |                                                                                                                                                                                                                                                          |
   |                                                 | x-amz-server-side-encryption-customer-algorithm:AES256                                                                                                                                                                                                   |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | x-amz-server-side-encryption-customer-key       | Indicates the key used to encrypt an object. The header is used in SSE-C mode and it is a base64-encoded 256-bit or 512-bit key.                                                                                                                         |
   |                                                 |                                                                                                                                                                                                                                                          |
   |                                                 | Example:                                                                                                                                                                                                                                                 |
   |                                                 |                                                                                                                                                                                                                                                          |
   |                                                 | x-amz-server-side-encryption-customer-key:K7QkYpBkM5+hcs27fsNkUnNVaobncnLht/rCB2o/9Cw=                                                                                                                                                                   |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | x-amz-server-side-encryption-customer-key-MD5   | Indicates the MD5 value of the key used to encrypt an object. The header is used in SSE-C mode and it is a base64-encoded 128-bit MD5 value of customer key. The MD5 value is used to check whether any error occurs during the transmission of the key. |
   |                                                 |                                                                                                                                                                                                                                                          |
   |                                                 | Example:                                                                                                                                                                                                                                                 |
   |                                                 |                                                                                                                                                                                                                                                          |
   |                                                 | x-amz-server-side-encryption-customer-key-MD5:4XvB3tbNTN+tIEVa0/fGaQ==                                                                                                                                                                                   |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. table:: **Table 2** Interfaces to which the newly added headers apply

   +---------------------------------------------------------------------+
   | Interface                                                           |
   +=====================================================================+
   | PUT Object                                                          |
   +---------------------------------------------------------------------+
   | POST Object                                                         |
   +---------------------------------------------------------------------+
   | PUT Object - Copy (the newly added headers apply to target objects) |
   +---------------------------------------------------------------------+
   | HEAD Object                                                         |
   +---------------------------------------------------------------------+
   | GET Object                                                          |
   +---------------------------------------------------------------------+
   | Initiate Multipart Upload                                           |
   +---------------------------------------------------------------------+
   | Upload Part                                                         |
   +---------------------------------------------------------------------+
   | Upload Part - Copy (the newly added headers apply to target parts)  |
   +---------------------------------------------------------------------+

:ref:`Table 3 <en-us_topic_0125560282__table50397498113431>` lists three headers that are added for PUT Object - Copy and Upload Part - Copy interfaces to support source objects encrypted using SSE-C.

.. _en-us_topic_0125560282__table50397498113431:

.. table:: **Table 3** Headers

   +-------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Header                                                      | Description                                                                                                                                                                                       |
   +=============================================================+===================================================================================================================================================================================================+
   | x-amz-copy-source-server-side-encryption-customer-algorithm | Indicates the algorithm used to decrypt a source object. The header is used in SSE-C mode.                                                                                                        |
   |                                                             |                                                                                                                                                                                                   |
   |                                                             | Example: x-amz-copy-source-server-side-encryption-customer-algorithm:AES256                                                                                                                       |
   +-------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | x-amz-copy-source-server-side-encryption-customer-key       | Indicates the key used to decrypt a source object. The header is used in SSE-C mode.                                                                                                              |
   |                                                             |                                                                                                                                                                                                   |
   |                                                             | Example:                                                                                                                                                                                          |
   |                                                             |                                                                                                                                                                                                   |
   |                                                             | x-amz-copy-source-server-side-encryption-customer-key:K7QkYpBkM5+hcs27fsNkUnNVaobncnLht/rCB2o/9Cw=                                                                                                |
   +-------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | x-amz-copy-source-server-side-encryption-customer-key-MD5   | Indicates the MD5 value of the key used to decrypt a source object. The header is used in SSE-C mode. The MD5 value is used to check whether any error occurs during the transmission of the key. |
   |                                                             |                                                                                                                                                                                                   |
   |                                                             | Example:                                                                                                                                                                                          |
   |                                                             |                                                                                                                                                                                                   |
   |                                                             | x-amz-copy-source-server-side-encryption-customer-key-MD5:4XvB3tbNTN+tIEVa0/fGaQ==                                                                                                                |
   +-------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
