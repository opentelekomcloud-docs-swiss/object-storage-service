:original_name: obs_04_0167.html

.. _obs_04_0167:

Configuring a Default WORM Policy for a Bucket
==============================================

Functions
---------

This API configures a default WORM policy and retention period for a bucket.

With the bucket's default WORM policy, if you do not specify a WORM policy or a retention period when you upload an object to the bucket, the default policy will be automatically applied to the newly uploaded object. An object-level WORM policy requires configuring a specific date, which indicates an object will be protected until that date. For a default bucket-level WORM policy, a retention period is required, and the protection for an object starts when the object is uploaded to the bucket.

To perform this operation, you must have the PutBucketObjectLockConfiguration permission. The bucket owner can perform this operation by default and can grant this permission to others by using a bucket policy or a user policy.

.. note::

   -  You can modify or even delete the default WORM policy of a bucket. The change applies only to the objects uploaded after the change, but not to those uploaded before.
   -  During a multipart upload, the object parts uploaded are not protected before they are assembled. After object parts are assembled, the new object is protected by the default bucket-level WORM policy. You can also configure an object-level WORM policy for the new object.
   -  You can also configure an object-level WORM policy when initializing a multipart upload or for an already assembled multipart object.

Other restrictions on the WORM retention configuration:

-  The WORM mode can only be **COMPLIANCE**.
-  The retention period can be set to **1** to **36500** days or **1** to **100** years.

Request Syntax
--------------

.. code-block:: text

   PUT /?object-lock HTTP/1.1
   Host: bucketname.obs.region.example.com
   Date: date
   Authorization: authorization
   Content-Type: application/xml
   Content-Length: length
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

Request Parameters
------------------

This request contains no message parameters.

Request Headers
---------------

This request uses common headers. For details, see :ref:`Table 3 <obs_04_0007__table25197309>`.

Request Elements
----------------

.. table:: **Table 1** Request elements

   +-------------------------+------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Element                 | Description                                                                                                            | Mandatory                                                                                                                                                |
   +=========================+========================================================================================================================+==========================================================================================================================================================+
   | ObjectLockConfiguration | Container for configuring WORM for a bucket.                                                                           | Yes                                                                                                                                                      |
   |                         |                                                                                                                        |                                                                                                                                                          |
   |                         | Type: container                                                                                                        |                                                                                                                                                          |
   +-------------------------+------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ObjectLockEnabled       | Indicates whether the bucket has WORM enabled. The value can only be **Enabled**.                                      | No                                                                                                                                                       |
   |                         |                                                                                                                        |                                                                                                                                                          |
   |                         | Type: string                                                                                                           |                                                                                                                                                          |
   |                         |                                                                                                                        |                                                                                                                                                          |
   |                         | Example: **Enabled**                                                                                                   |                                                                                                                                                          |
   +-------------------------+------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Rule                    | Rule container for the default bucket-level WORM policy.                                                               | This header is mandatory for configuring the default WORM policy for a bucket. If it is not contained, the existing default WORM policy will be deleted. |
   |                         |                                                                                                                        |                                                                                                                                                          |
   |                         | Type: container                                                                                                        |                                                                                                                                                          |
   +-------------------------+------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | DefaultRetention        | Container for the default WORM retention policy for the bucket.                                                        | Mandatory if the Rule container is included.                                                                                                             |
   |                         |                                                                                                                        |                                                                                                                                                          |
   |                         | Type: container                                                                                                        |                                                                                                                                                          |
   +-------------------------+------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Mode                    | Default protection mode. It can only be set to **COMPLIANCE** now.                                                     | Mandatory if the DefaultRetention container is included.                                                                                                 |
   |                         |                                                                                                                        |                                                                                                                                                          |
   |                         | Type: string                                                                                                           |                                                                                                                                                          |
   |                         |                                                                                                                        |                                                                                                                                                          |
   |                         | Example: **COMPLIANCE**                                                                                                |                                                                                                                                                          |
   +-------------------------+------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Days                    | Default protection period, in days. The value is from **1** to **36500**.                                              | If the DefaultRetention container is included, you must specify either **Days** or **Years**, but you cannot specify both at the same time.              |
   |                         |                                                                                                                        |                                                                                                                                                          |
   |                         | Type: integer                                                                                                          |                                                                                                                                                          |
   |                         |                                                                                                                        |                                                                                                                                                          |
   |                         | Example: **1**                                                                                                         |                                                                                                                                                          |
   +-------------------------+------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Years                   | Default protection period, in years. The value is from **1** to **100**. In a leap year, only 365 days are calculated. | If the DefaultRetention container is included, you must specify either **Years** or **Days**, but you cannot specify both at the same time.              |
   |                         |                                                                                                                        |                                                                                                                                                          |
   |                         | Type: integer                                                                                                          |                                                                                                                                                          |
   |                         |                                                                                                                        |                                                                                                                                                          |
   |                         | Example: **1**                                                                                                         |                                                                                                                                                          |
   +-------------------------+------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+

Response Syntax
---------------

.. code-block::

   HTTP/1.1 status_code
   Date: date
   Content-Length: length

Response Headers
----------------

This response uses common headers. For details, see :ref:`Table 1 <obs_04_0013__d0e686>`.

Response Elements
-----------------

This response contains no elements.

Error Responses
---------------

:ref:`Table 2 <obs_04_0167__table13791928162213>` describes possible special errors in this request.

.. _obs_04_0167__table13791928162213:

.. table:: **Table 2**

   +----------------+--------------------------------------------------+------------------+
   | Error Code     | Description                                      | HTTP Status Code |
   +================+==================================================+==================+
   | InvalidRequest | The object lock is disabled for the bucket.      | 400              |
   +----------------+--------------------------------------------------+------------------+
   | MalformedXML   | Invalid format of the Object Lock configuration. | 400              |
   +----------------+--------------------------------------------------+------------------+

For other errors, see :ref:`Table 2 <obs_04_0115__d0e843>`.

Sample Request 1
----------------

Configure the default bucket-level WORM policy with a retention period of 2 years.

.. code-block:: text

   PUT /?object-lock HTTP/1.1
   Host: bucketname.obs.region.example.com
   Date: WED, 01 Jul 2015 02:25:05 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:75/Y4Ng1izvzc1nTGxpMXTE6ynw=
   Content-Type: application/xml
   Content-Length: 157
   <ObjectLockConfiguration xmlns="http://obs.region.example.com/doc/2015-06-30/">
       <ObjectLockEnabled>Enabled</ObjectLockEnabled>
       <Rule>
          <DefaultRetention>
             <Mode>COMPLIANCE</Mode>
             <Years>2</Years>
          </DefaultRetention>
       </Rule>
   </ObjectLockConfiguration>

Sample Response 1
-----------------

.. code-block::

   HTTP/1.1 200 OK
   Server: OBS
   x-obs-request-id: BF260000016435CE298386946AE4C482
   x-obs-id-2: 32AAAQAAEAABSAAgAAEAABAAAQAAEAABCT9W2tcvLmMJ+plfdopaD62S0npbaRUz
   Date: WED, 01 Jul 2015 02:25:06 GMT
   Content-Length: 0

Sample Request 2
----------------

Delete the configuration of the default bucket-level WORM policy.

.. code-block:: text

   PUT /?object-lock HTTP/1.1
   Host: bucketname.obs.region.example.com
   Date: WED, 01 Jul 2015 02:25:05 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:75/Y4Ng1izvzc1nTGxpMXTE6ynw=
   Content-Type: application/xml
   Content-Length: 157
   <ObjectLockConfiguration xmlns="http://obs.region.example.com/doc/2015-06-30/">
   </ObjectLockConfiguration>

Sample Response 2
-----------------

.. code-block::

   HTTP/1.1 200 OK
   Server: OBS
   x-obs-request-id: BF260000016435CE298386946AE4C482
   x-obs-id-2: 32AAAQAAEAABSAAgAAEAABAAAQAAEAABCT9W2tcvLmMJ+plfdopaD62S0npbaRUz
   Date: WED, 01 Jul 2015 02:25:06 GMT
   Content-Length: 0
