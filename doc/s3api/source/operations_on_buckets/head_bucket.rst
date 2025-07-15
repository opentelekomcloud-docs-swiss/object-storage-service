:original_name: en-us_topic_0125560467.html

.. _en-us_topic_0125560467:

HEAD Bucket
===========

After being granted **READ** permission for a bucket, you can use this operation to query whether the bucket exists.

Request Syntax
--------------

.. code-block::

   HEAD / HTTP/1.1
    User-Agent: agent
    Host: bucketname.obs.example.com
    Accept: */*
    Date: date
    Authorization: authorization

Request Parameters
------------------

This request involves no parameters.

Request Headers
---------------

This request uses common headers. For details about common request headers, see section :ref:`Common Request Headers <en-us_topic_0125560462>`.

If you want to obtain CORS configuration information, you must use the headers in :ref:`Table 1 <en-us_topic_0125560467__table48864719>`.

.. _en-us_topic_0125560467__table48864719:

.. table:: **Table 1** Request headers of CORS configuration

   +--------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | Header                         | Description                                                                                                                                                                        | Remarks                                                                          |
   +================================+====================================================================================================================================================================================+==================================================================================+
   | Origin                         | Indicates an origin specified by a pre-request. Generally, it is a domain name.                                                                                                    | Mandatory                                                                        |
   |                                |                                                                                                                                                                                    |                                                                                  |
   |                                | Type: String                                                                                                                                                                       |                                                                                  |
   +--------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | Access-Control-Request-Headers | Indicates the HTTP headers of a request. The request can use multiple HTTP headers.                                                                                                | Optional                                                                         |
   |                                |                                                                                                                                                                                    |                                                                                  |
   |                                | Type: String                                                                                                                                                                       |                                                                                  |
   +--------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | x-amz-security-token           | Header field used to identify the request of a federated user. When the federal authentication function is enabled, users sending such requests are identified as federated users. | Optional. This parameter must be carried in the request sent by federated users. |
   |                                |                                                                                                                                                                                    |                                                                                  |
   |                                | Type: string                                                                                                                                                                       |                                                                                  |
   +--------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+

Request Elements
----------------

This request involves no elements.

Response Syntax
---------------

.. code-block::

   HTTP/1.1 status_code
    Server: Server Name
    x-amz-request-id: request id
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    x-amz-bucket-region: region name
    Content-Type: */*
    x-obs-version: version
    x-default-storage-class: staorage class
    x-amz-id-2: id
    Date: date
    Content-Length: length

Response Headers
----------------

This response uses common headers. For details about common response headers, see section :ref:`Common Response Headers <en-us_topic_0125560484>`.

In addition to common headers, when CORS is configured for buckets, you can use the response headers in :ref:`Table 2 <en-us_topic_0125560467__table14722737>`.

.. _en-us_topic_0125560467__table14722737:

.. table:: **Table 2** Appended response headers when CORS is configured for buckets

   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Header                            | Description                                                                                                                                                          |
   +===================================+======================================================================================================================================================================+
   | Access-Control-Allow-Origin       | If **Origin** in the request meets the CORS configuration requirements, **Origin** is included in the response.                                                      |
   |                                   |                                                                                                                                                                      |
   |                                   | Type: String                                                                                                                                                         |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access-Control-Allow-Headers      | If **headers** in the request meet the CORS configuration requirements, **headers** are included in the response.                                                    |
   |                                   |                                                                                                                                                                      |
   |                                   | Type: String                                                                                                                                                         |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access-Control-Max-Age            | Indicates **MaxAgeSeconds** in the CORS configuration of a server.                                                                                                   |
   |                                   |                                                                                                                                                                      |
   |                                   | Type: Integer                                                                                                                                                        |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access-Control-Allow-Methods      | If **Access-Control-Request-Method** in the request meets the CORS configuration requirements, methods in the rule are included in the response.                     |
   |                                   |                                                                                                                                                                      |
   |                                   | Type: String                                                                                                                                                         |
   |                                   |                                                                                                                                                                      |
   |                                   | Valid values: **GET**, **PUT**, **HEAD**, **POST**, and **DELETE**                                                                                                   |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access-Control-Expose-Headers     | Indicates **ExposeHeader** in the CORS configuration of a server.                                                                                                    |
   |                                   |                                                                                                                                                                      |
   |                                   | Type: String                                                                                                                                                         |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | x-amz-bucket-region               | Indicates the region of the bucket.                                                                                                                                  |
   |                                   |                                                                                                                                                                      |
   |                                   | Type: String                                                                                                                                                         |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | x-default-storage-class           | Indicates the default storage class of the current bucket. There are three storage classes: STANDARD (OBS Standard), STANDARD_IA (OBS Warm), and GLACIER (OBS Cold). |
   |                                   |                                                                                                                                                                      |
   |                                   | Type: String                                                                                                                                                         |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Response Elements
-----------------

This response involves no elements.

Error Responses
---------------

No special error responses are returned. For details about error responses, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`.

Sample Request
--------------

.. code-block::

   HEAD / HTTP/1.1
    User-Agent: Jakarta Commons-HttpClient/3.1
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Sun, 26 Sep 2010 09:16:00 GMT
    Authorization: AWS 04RZT432N80TGDF2Y2G2:JUtd9kkJFjbKbkP9f6T/tAxozYY=

Sample Response
---------------

.. code-block::

   HTTP/1.1 200 OK
   Server: OBS
   x-amz-request-id: 367CB63A2F283044981285492719060
   x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
   x-amz-bucket-region: R1
   Content-Type: application/xml
   x-obs-version: 3.0
   x-default-storage-class: STANDARD
   x-amz-id-2: MzY3Q0I2M0EyRjI4MzA0NDk4MTI4NTQ5MjcxOTA2MEFBQUFBQUFBYmJiYmJiYmJD
   Date: Sun, 26 Sep 2010 09:18:36 GMT
   Content-Length: 0

Sample Request (Getting Bucket Metadata and CORS Configuration when CORS is properly configured)
------------------------------------------------------------------------------------------------

.. code-block::

   HEAD / HTTP/1.1
   User-Agent: curl/7.19.0 (x86_64-suse-linux-gnu) libcurl/7.19.0 OpenSSL/0.9.8{ zlib/1.2.3 libidn/1.10
   Host: bucketname.obs.example.com
   Accept: */*
   Date: Tue, 28 Apr 2015 13:47:30 +0000
   Authorization: AWS D13E0C94E722DD69423C:1UL75oi0bFRpJlgZMfvh4lUyjBs=
   Origin:www.example.com
   Access-Control-Request-Headers:AllowedHeader_1

Sample Response (Getting Bucket Metadata and CORS Configuration when CORS is properly configured)
-------------------------------------------------------------------------------------------------

.. code-block::

   HTTP/1.1 200 OK
   x-amz-request-id: BC4C45F57B0DED38D006D5F8FEB738C4
   x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
   Access-Control-Allow-Origin: www.example.com
   Access-Control-Allow-Methods: POST,GET,HEAD,PUT
   Access-Control-Allow-Headers: AllowedHeader_1
   Access-Control-Max-Age: 100
   Access-Control-Expose-Headers: ExposeHeader_1
   x-amz-bucket-region: R1
   Content-Type: text/xml
   x-obs-version: 3.0
   x-default-storage-class: STANDARD
   x-amz-id-2: YkFlH3FTA2Tf/lIc2XiyuICp/EUqpVI4j1/g5hlatg75TTZdERSCYliqitChspgA
   Date: Tue, 28 Apr 2015 13:47:30 GMT
   Content-Length: 0
