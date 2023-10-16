:original_name: obs_04_0023.html

.. _obs_04_0023:

Obtaining Bucket Metadata
=========================

Functions
---------

This operation queries the metadata of a bucket. To use this operation, you must have the permission to read the bucket.

Request Syntax
--------------

::

   HEAD / HTTP/1.1
   Host: bucketname.obs.region.example.com
   Date: date
   Authorization: authorization

Request Parameters
------------------

This request contains no parameters.

Request Headers
---------------

This request uses common headers. For details, see :ref:`Table 3 <obs_04_0007__table25197309>`.

:ref:`Table 1 <obs_04_0023__table1147631064117>` lists the header fields required when obtaining CORS configuration information.

.. _obs_04_0023__table1147631064117:

.. table:: **Table 1** Request headers for obtaining CORS configuration

   +--------------------------------+--------------------------------------------------------------------------------------------------+-----------------------+
   | Header                         | Description                                                                                      | Mandatory             |
   +================================+==================================================================================================+=======================+
   | Origin                         | Origin of the cross-domain request specified by the pre-request. Generally, it is a domain name. | Yes                   |
   |                                |                                                                                                  |                       |
   |                                | Type: string                                                                                     |                       |
   +--------------------------------+--------------------------------------------------------------------------------------------------+-----------------------+
   | Access-Control-Request-Headers | HTTP headers of a request. The request can use multiple HTTP headers.                            | No                    |
   |                                |                                                                                                  |                       |
   |                                | Type: string                                                                                     |                       |
   +--------------------------------+--------------------------------------------------------------------------------------------------+-----------------------+

Request Elements
----------------

This request contains no elements.

Response Syntax
---------------

::

   HTTP/1.1 status_code
   x-obs-bucket-location: region
   Date: date

Response Headers
----------------

The response to the request uses common headers. For details, see :ref:`Table 1 <obs_04_0013__d0e686>`.

In addition to the common response headers, the message headers listed in :ref:`Table 2 <obs_04_0023__table13151171313444>` may be used.

.. _obs_04_0023__table13151171313444:

.. table:: **Table 2** Additional response headers

   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Header                            | Description                                                                                                                                                                                        |
   +===================================+====================================================================================================================================================================================================+
   | x-obs-bucket-location             | The region where the bucket resides.                                                                                                                                                               |
   |                                   |                                                                                                                                                                                                    |
   |                                   | Type: string                                                                                                                                                                                       |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | x-obs-version                     | OBS version of the bucket.                                                                                                                                                                         |
   |                                   |                                                                                                                                                                                                    |
   |                                   | Type: string                                                                                                                                                                                       |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access-Control-Allow-Origin       | Indicates that the origin is included in the response if the origin in the request meets the CORS configuration requirements when CORS is configured for buckets.                                  |
   |                                   |                                                                                                                                                                                                    |
   |                                   | Type: string                                                                                                                                                                                       |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access-Control-Allow-Headers      | Indicates that the headers are included in the response if headers in the request meet the CORS configuration requirements when CORS is configured for buckets.                                    |
   |                                   |                                                                                                                                                                                                    |
   |                                   | Type: string                                                                                                                                                                                       |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access-Control-Max-Age            | Value of **MaxAgeSeconds** in the CORS configuration of the server when CORS is configured for buckets.                                                                                            |
   |                                   |                                                                                                                                                                                                    |
   |                                   | Type: integer                                                                                                                                                                                      |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access-Control-Allow-Methods      | Indicates that methods in the rule are included in the response if **Access-Control-Request-Method** in the request meets the CORS configuration requirements when CORS is configured for buckets. |
   |                                   |                                                                                                                                                                                                    |
   |                                   | Type: string                                                                                                                                                                                       |
   |                                   |                                                                                                                                                                                                    |
   |                                   | Value options: **GET**, **PUT**, **HEAD**, **POST**, **DELETE**                                                                                                                                    |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access-Control-Expose-Headers     | Value of **ExposeHeader** in the CORS configuration of a server when CORS is configured for buckets.                                                                                               |
   |                                   |                                                                                                                                                                                                    |
   |                                   | Type: string                                                                                                                                                                                       |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Response Elements
-----------------

This response contains no elements.

Error Responses
---------------

No special error responses are returned. For details about error responses, see :ref:`Table 2 <obs_04_0115__d0e843>`.

Sample Request: Getting CORS Configuration (with No Headers Specified)
----------------------------------------------------------------------

::

   HEAD / HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: WED, 01 Jul 2015 02:30:25 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:niCQCuGIZpETKIyx1datxHZyYlk=

Sample Response: Getting CORS Configuration (with No Headers Specified)
-----------------------------------------------------------------------

::

   HTTP/1.1 200 OK
   Server: OBS
   x-obs-request-id: BF260000016439C734E0788404623FA8
   Content-Type: application/xml
   x-obs-id-2: 32AAAQAAEAABAAAQAAEAABAAAQAAEAABCSxwLpq9Hzf3OnaXr+pI/OPLKdrtiQAF
   Date: WED, 01 Jul 2015 02:30:25 GMT
   x-obs-bucket-location: region
   x-obs-version: 3.0
   Content-Length: 0

Sample Request: Getting Bucket Metadata and CORS Configuration
--------------------------------------------------------------

::

   HEAD / HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: WED, 01 Jul 2015 02:30:25 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:niCQCuGIZpETKIyx1datxHZyYlk=
   Origin:www.example.com
   Access-Control-Request-Headers:AllowedHeader_1

Sample Response: Getting Bucket Metadata and CORS Configuration
---------------------------------------------------------------

::

   HTTP/1.1 200 OK
   Server: OBS
   x-obs-request-id: BF260000016439C734E0788404623FA8
   Content-Type: application/xml
   x-obs-id-2: 32AAAQAAEAABAAAQAAEAABAAAQAAEAABCSxwLpq9Hzf3OnaXr+pI/OPLKdrtiQAF
   Date: WED, 01 Jul 2015 02:30:25 GMT
   x-obs-bucket-location: region
   Access-Control-Allow-Origin: www.example.com
   Access-Control-Allow-Methods: POST,GET,HEAD,PUT
   Access-Control-Allow-Headers: AllowedHeader_1
   Access-Control-Max-Age: 100
   Access-Control-Expose-Headers: ExposeHeader_1
   x-obs-version: 3.0
   Content-Length: 0
