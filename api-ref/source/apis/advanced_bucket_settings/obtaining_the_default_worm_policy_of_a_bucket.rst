:original_name: obs_04_0168.html

.. _obs_04_0168:

Obtaining the Default WORM Policy of a Bucket
=============================================

Functions
---------

This operation returns the default WORM policy of a bucket.

To perform this operation, you must have the GetBucketObjectLockConfiguration permission. The bucket owner can perform this operation by default and can grant this permission to others by using a bucket policy or a user policy.

.. note::

   If you have never configured the default bucket-level retention policy after you enable WORM for a bucket, you can still use this API to check whether WORM is enabled.

Request Syntax
--------------

.. code-block:: text

   GET /?object-lock HTTP/1.1
   Host: bucketname.obs.region.example.com
   Date: date
   Authorization: authorization
   Content-Type: application/xml
   Content-Length: length

Request Parameters
------------------

This request contains no message parameters.

Request Headers
---------------

This request uses common headers. For details, see :ref:`Table 3 <obs_04_0007__table25197309>`.

Request Elements
----------------

This request involves no elements.

Response Syntax
---------------

.. code-block::

   HTTP/1.1 status_code
   Date: date
   Content-Type: application/xml
   Content-Length: length

   <?xml version="1.0" encoding="UTF-8"?>
   <ObjectLockConfiguration xmlns="http://obs.region.example.com/doc/2015-06-30/">
       <ObjectLockEnabled>Enabled</ObjectLockEnabled>
       <Rule>
          <DefaultRetention>
             <Days>integer</Days>
             <Mode>COMPLIANCE</Mode>
             <Years>integer</Years>
          </DefaultRetention>
       </Rule>
   </ObjectLockConfiguration>

Response Headers
----------------

This response uses common headers. For details, see :ref:`Table 1 <obs_04_0013__d0e686>`.

Response Elements
-----------------

:ref:`Table 1 <obs_04_0168__table17259161213419>` describes the elements of the default bucket-level WORM policy in the response.

.. _obs_04_0168__table17259161213419:

.. table:: **Table 1** Elements of the default bucket-level WORM policy

   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Element                           | Description                                                                                                                                            |
   +===================================+========================================================================================================================================================+
   | ObjectLockConfiguration           | Container for configuring for a bucket.                                                                                                                |
   |                                   |                                                                                                                                                        |
   |                                   | Type: container                                                                                                                                        |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ObjectLockEnabled                 | Indicates whether WORM is enabled for the bucket. The value can only be **Enabled**.                                                                   |
   |                                   |                                                                                                                                                        |
   |                                   | Type: string                                                                                                                                           |
   |                                   |                                                                                                                                                        |
   |                                   | Example: **Enabled**                                                                                                                                   |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Rule                              | Container for the default bucket-level WORM policy. If you have never configured the default policy, this header will not be included in the response. |
   |                                   |                                                                                                                                                        |
   |                                   | Type: container                                                                                                                                        |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+
   | DefaultRetention                  | Container for the default bucket-level WORM policy.                                                                                                    |
   |                                   |                                                                                                                                                        |
   |                                   | Type: container                                                                                                                                        |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Mode                              | Default protection mode. It can only be set to **COMPLIANCE** now.                                                                                     |
   |                                   |                                                                                                                                                        |
   |                                   | Type: string                                                                                                                                           |
   |                                   |                                                                                                                                                        |
   |                                   | Example: **COMPLIANCE**                                                                                                                                |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Days                              | Default protection period, in days. The value is from **1** to **36500**.                                                                              |
   |                                   |                                                                                                                                                        |
   |                                   | Type: integer                                                                                                                                          |
   |                                   |                                                                                                                                                        |
   |                                   | Example: **1**                                                                                                                                         |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Years                             | Default protection period, in years. The value is from 1 to 100. In a leap year, only 365 days are calculated.                                         |
   |                                   |                                                                                                                                                        |
   |                                   | Type: integer                                                                                                                                          |
   |                                   |                                                                                                                                                        |
   |                                   | Example: **1**                                                                                                                                         |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+

Error Responses
---------------

:ref:`Table 2 <obs_04_0168__table13791928162213>` describes possible special errors in this request.

.. _obs_04_0168__table13791928162213:

.. table:: **Table 2**

   +----------------+-------------------------------------------------------------------------------------------------+------------------+
   | Error Code     | Description                                                                                     | HTTP Status Code |
   +================+=================================================================================================+==================+
   | InvalidRequest | The default object lock rule cannot be get, because object lock is not enabled for this bucket. | 400              |
   +----------------+-------------------------------------------------------------------------------------------------+------------------+

For other errors, see :ref:`Table 2 <obs_04_0115__d0e843>`.

Sample Request 1
----------------

Get the configuration where the bucket has WORM enabled, but has no default retention policy configured.

.. code-block:: text

   GET /?object-lock HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: WED, 01 Jul 2015 02:25:05 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:75/Y4Ng1izvzc1nTGxpMXTE6ynw=
   Content-Length: 0

Sample Response 1
-----------------

.. code-block::

   HTTP/1.1 200 OK
   Server: OBS
   x-obs-request-id: BF260000016435CE298386946AE4C482
   x-obs-id-2: 32AAAQAAEAABSAAgAAEAABAAAQAAEAABCT9W2tcvLmMJ+plfdopaD62S0npbaRUz
   Date: WED, 01 Jul 2015 02:25:06 GMT
   Content-Length: 157

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <ObjectLockConfiguration xmlns="http://obs.region.example.com/doc/2015-06-30/">
     <ObjectLockEnabled>Enabled</ObjectLockEnabled>
   </ObjectLockConfiguration>

Sample Request 2
----------------

Get the configuration where the bucket has WORM enabled and has the default retention policy configured.

.. code-block:: text

   GET /?object-lock HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: WED, 01 Jul 2015 02:25:05 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:75/Y4Ng1izvzc1nTGxpMXTE6ynw=
   Content-Length: 0

Sample Response 2
-----------------

.. code-block::

   HTTP/1.1 200 OK
   Server: OBS
   x-obs-request-id: BF260000016435CE298386946AE4C482
   x-obs-id-2: 32AAAQAAEAABSAAgAAEAABAAAQAAEAABCT9W2tcvLmMJ+plfdopaD62S0npbaRUz
   Date: WED, 01 Jul 2015 02:25:06 GMT
   Content-Length: 157

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <ObjectLockConfiguration xmlns="http://obs.region.example.com/doc/2015-06-30/">
     <ObjectLockEnabled>Enabled</ObjectLockEnabled>
     <Rule>
       <DefaultRetention>
         <Mode>COMPLIANCE</Mode>
         <Days>10</Days>
         <Years>0</Years>
       </DefaultRetention>
     </Rule>
   </ObjectLockConfiguration>
