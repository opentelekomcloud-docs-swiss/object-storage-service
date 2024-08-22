:original_name: obs_04_0166.html

.. _obs_04_0166:

Configuring WORM Retention for an Object
========================================

Functions
---------

This operation configures or updates the retention period for objects uploaded to a bucket with WORM enabled.

-  When you upload an object, if you do not configure a protection period or apply the default bucket-level protection rule to the object, you can perform this operation to configure a protection period for the object.
-  When you upload an object, if you configure a protection period or apply the default bucket-level protection rule to the object, you can perform this operation to prolong the protection period for the object.
-  The protection period of an object can only be modified, but not deleted.

   .. note::

      To configure or update the protection period of an object, you must have the PutObjectRetention permission.

Versioning
----------

OBS automatically enables versioning when you enable WORM for a bucket. In such case, the object you uploaded to the bucket will be assigned a version ID. An object-level WORM policy is applied to the current object version by default, but you can specify a version ID to make the policy applied to a specific object version. The WORM configuration does not apply to a delete marker with a unique version ID.

Multipart Upload
----------------

Before a multipart upload is complete, the default bucket-level WORM policy is not automatically applied to the object parts uploaded. Besides, you cannot configure an object-level WORM policy using a header when you upload a part or assemble the object parts, or for a part that is already uploaded to the bucket. You can call this API to configure a WORM retention policy for the new object after the object parts are assembled.

Request Syntax
--------------

.. code-block:: text

   PUT /ObjectName?retention HTTP/1.1
   Host: bucketname.obs.region.example.com
   Date: date
   Authorization: authorization

   <Retention>
       <Mode>String</Mode>
       <RetainUntilDate>Timestamp</RetainUntilDate>
   </Retention>

Request Parameters
------------------

:ref:`Table 1 <obs_04_0166__table44298471191845>` describes the parameters.

.. _obs_04_0166__table44298471191845:

.. table:: **Table 1** Request parameters

   +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Parameter             | Description                                                                                                                                              | Mandatory             |
   +=======================+==========================================================================================================================================================+=======================+
   | versionId             | ID of the object version on which this operation will be performed. If this header is not carried, this operation applies to the current object version. | No                    |
   |                       |                                                                                                                                                          |                       |
   |                       | Type: string                                                                                                                                             |                       |
   +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

Request Headers
---------------

This request uses common headers. For details, see :ref:`Table 3 <obs_04_0007__table25197309>`.

Request Elements
----------------

+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
| Element               | Description                                                                                                                                    | Mandatory             |
+=======================+================================================================================================================================================+=======================+
| Retention             | Container for configuring an object-level WORM retention policy.                                                                               | Yes                   |
|                       |                                                                                                                                                |                       |
|                       | Type: container                                                                                                                                |                       |
+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
| Mode                  | Protection mode for the object. It can only be set to **COMPLIANCE** now.                                                                      | Yes                   |
|                       |                                                                                                                                                |                       |
|                       | Type: string                                                                                                                                   |                       |
|                       |                                                                                                                                                |                       |
|                       | Example: **COMPLIANCE**                                                                                                                        |                       |
+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
| RetainUntilDate       | Protection period for the object. The value can be a timestamp or in the ISO format.                                                           | Yes                   |
|                       |                                                                                                                                                |                       |
|                       | A timestamp must be accurate to milliseconds. For example, the timestamp for 13:20:35 on July 1, 2015 should be **1435728035000**.             |                       |
|                       |                                                                                                                                                |                       |
|                       | A time zone is required in the ISO time format. For example, the ISO UTC time for 13:20:35 on July 1, 2015 should be **2015-07-01T13:20:35Z**. |                       |
|                       |                                                                                                                                                |                       |
|                       | .. note::                                                                                                                                      |                       |
|                       |                                                                                                                                                |                       |
|                       |    The value of this field must be later than the current time and can be extended but not shortened.                                          |                       |
|                       |                                                                                                                                                |                       |
|                       | Type: string                                                                                                                                   |                       |
|                       |                                                                                                                                                |                       |
|                       | Example: **1435728035000** (a timestamp) or **2015-07-01T13:20:35Z** (in the ISO format)                                                       |                       |
|                       |                                                                                                                                                |                       |
|                       | Remarks: timestamp value is accurate to milliseconds in Unix time.                                                                             |                       |
+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

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

:ref:`Table 2 <obs_04_0166__table13791928162213>` describes possible special errors in this request.

.. _obs_04_0166__table13791928162213:

.. table:: **Table 2**

   +--------------------------+----------------------------------------------------------------------------------+------------------+
   | Error Code               | Description                                                                      | HTTP Status Code |
   +==========================+==================================================================================+==================+
   | InvalidRequest           | The object lock is disabled for the bucket.                                      | 400              |
   +--------------------------+----------------------------------------------------------------------------------+------------------+
   | InvalidRequest           | The retention period date must be later than the current or the configured date. | 400              |
   +--------------------------+----------------------------------------------------------------------------------+------------------+
   | MalformedObjectLockError | Invalid format of the Object Lock configuration.                                 | 400              |
   +--------------------------+----------------------------------------------------------------------------------+------------------+

For other errors, see :ref:`Table 2 <obs_04_0115__d0e843>`.

Sample Request 1
----------------

.. code-block:: text

   PUT /objectname?retention HTTP/1.1
   Host: bucketname.obs.region.example.com
   Date: WED, 01 Jul 2015 02:25:05 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:75/Y4Ng1izvzc1nTGxpMXTE6ynw=
   Content-Type: application/xml
   Content-Length: 157
   <Retention>
       <Mode>COMPLIANCE</Mode>
       <RetainUntilDate>1435728035000</RetainUntilDate>
   </Retention>

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

Configure the WORM protection (with the protection period specified in the ISO format) for an object.

.. code-block:: text

   PUT /objectname?retention HTTP/1.1
   Host: bucketname.obs.region.example.com
   WED, 01 Jul 2015 02:25:06 GMT
   Authorization: OBS UDSIAMSTUBTEST043961:qWxD1d0LIT6fGT4Lp7KNUTZ+ikU=
   Content-Type: application/xml
   Content-Length: 193
   <Retention>
       <Mode>COMPLIANCE</Mode>
       <RetainUntilDate>2015-07-01T13:20:35Z</RetainUntilDate>
   </Retention>

Sample Response 2
-----------------

.. code-block::

   HTTP/1.1 200 OK
   Server: OBS
   x-obs-request-id: 0000018E3CC039E75306D1560F6A5B61
   x-obs-id-2: 32AAAUgAIAABAAAQAAEAABAAAQAAEAABCS14XamzycaPY1tivqczu/2SI2sbVBNZ
   Date: WED, 01 Jul 2015 02:25:06 GMT
   Content-Length: 0
