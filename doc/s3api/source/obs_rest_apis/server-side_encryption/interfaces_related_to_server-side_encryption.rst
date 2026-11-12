:original_name: en-us_topic_0125560285.html

.. _en-us_topic_0125560285:

Interfaces Related to Server-Side Encryption
============================================

This section lists the interfaces related to server-side encryption and describes transfer protocols and authentication applicable to the interfaces.

The following tables describe transfer protocols and authentication applicable to the interfaces related to server-side encryption.

.. table:: **Table 1** Transfer protocols and authentication applicable to SSE-C-related interfaces

   ========================= ================= ==============
   Interface                 Transfer Protocol Authentication
   ========================= ================= ==============
   PUT Object                HTTPS             V2 or V4
   POST Object               HTTPS             V2 or V4
   Initiate Multipart Upload HTTPS             V2 or V4
   HEAD Object               HTTPS             V2 or V4
   GET Object                HTTPS             V2 or V4
   Upload Part               HTTPS             V2 or V4
   Complete Multipart Upload HTTP or HTTPS     V2 or V4
   ========================= ================= ==============

.. table:: **Table 2** Transfer protocols and authentication applicable to SSE-KMS-related interfaces

   ========================= ================= ==============
   Interface                 Transfer Protocol Authentication
   ========================= ================= ==============
   PUT Object                HTTPS             V4
   POST Object               HTTPS             V4
   Initiate Multipart Upload HTTPS             V4
   HEAD Object               HTTP or HTTPS     V2 or V4
   GET Object                HTTPS             V4
   Upload Part               HTTPS             V4
   Complete Multipart Upload HTTP or HTTPS     V2 or V4
   ========================= ================= ==============

.. table:: **Table 3** Transfer protocols and authentication applicable to PUT Object - Copy interfaces

   +--------------------------------+--------------------------------+-------------------+----------------+
   | Source Object                  | Target Object                  | Transfer Protocol | Authentication |
   +================================+================================+===================+================+
   | Non-encrypted object           | Object encrypted using SSE-KMS | HTTPS             | V4             |
   +--------------------------------+--------------------------------+-------------------+----------------+
   | Object encrypted using SSE-KMS | Object encrypted using SSE-KMS | HTTPS             | V4             |
   +--------------------------------+--------------------------------+-------------------+----------------+
   | Object encrypted using SSE-C   | Object encrypted using SSE-KMS | HTTPS             | V4             |
   +--------------------------------+--------------------------------+-------------------+----------------+
   | Non-encrypted object           | Object encrypted using SSE-C   | HTTPS             | V2 or V4       |
   +--------------------------------+--------------------------------+-------------------+----------------+
   | Object encrypted using SSE-KMS | Object encrypted using SSE-C   | HTTPS             | V2 or V4       |
   +--------------------------------+--------------------------------+-------------------+----------------+
   | Object encrypted using SSE-C   | Object encrypted using SSE-C   | HTTPS             | V2 or V4       |
   +--------------------------------+--------------------------------+-------------------+----------------+
   | Non-encrypted object           | Non-encrypted object           | HTTP or HTTPS     | V2 or V4       |
   +--------------------------------+--------------------------------+-------------------+----------------+
   | Object encrypted using SSE-KMS | Non-encrypted object           | HTTP or HTTPS     | V2 or V4       |
   +--------------------------------+--------------------------------+-------------------+----------------+
   | Object encrypted using SSE-C   | Non-encrypted object           | HTTP or HTTPS     | V2 or V4       |
   +--------------------------------+--------------------------------+-------------------+----------------+

.. table:: **Table 4** Transfer protocols and authentication applicable to Upload Part - Copy interfaces

   +--------------------------------+------------------------------+-------------------+----------------+
   | Source Object                  | Target Part                  | Transfer Protocol | Authentication |
   +================================+==============================+===================+================+
   | Non-encrypted object           | Part encrypted using SSE-KMS | HTTP or HTTPS     | V2 or V4       |
   +--------------------------------+------------------------------+-------------------+----------------+
   | Object encrypted using SSE-KMS | Part encrypted using SSE-KMS | HTTP or HTTPS     | V2 or V4       |
   +--------------------------------+------------------------------+-------------------+----------------+
   | Object encrypted using SSE-C   | Part encrypted using SSE-KMS | HTTP or HTTPS     | V2 or V4       |
   +--------------------------------+------------------------------+-------------------+----------------+
   | Non-encrypted object           | Part encrypted using SSE-C   | HTTPS             | V2 or V4       |
   +--------------------------------+------------------------------+-------------------+----------------+
   | Object encrypted using SSE-KMS | Part encrypted using SSE-C   | HTTPS             | V2 or V4       |
   +--------------------------------+------------------------------+-------------------+----------------+
   | Object encrypted using SSE-C   | Part encrypted using SSE-C   | HTTPS             | V2 or V4       |
   +--------------------------------+------------------------------+-------------------+----------------+
   | Non-encrypted object           | Non-encrypted part           | HTTP or HTTPS     | V2 or V4       |
   +--------------------------------+------------------------------+-------------------+----------------+
   | Object encrypted using SSE-KMS | Non-encrypted part           | HTTP or HTTPS     | V2 or V4       |
   +--------------------------------+------------------------------+-------------------+----------------+
   | Object encrypted using SSE-C   | Non-encrypted part           | HTTP or HTTPS     | V2 or V4       |
   +--------------------------------+------------------------------+-------------------+----------------+
