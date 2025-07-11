:original_name: obs_04_0087.html

.. _obs_04_0087:

Restoring Cold Objects
======================

Functions
---------

To obtain the content of an object in the Cold storage class, you need to restore the object first and then you can download it. After an object is restored, a copy of the object is saved in the Standard storage class. By doing so, the object in the Cold storage class and its copy in the Standard storage class co-exist in the bucket. The copy will be automatically deleted once its retention period ends.

Versioning
----------

By default, this operation returns the latest version of an object. If the object has a delete marker, status code 404 is returned. To restore an object of a specified version, the **versionId** parameter can be used to specify the desired version.

Request Syntax
--------------

.. code-block:: text

   POST /ObjectName?restore&versionId=VersionID HTTP/1.1
   Host: bucketname.obs.region.example.com
   Date: date
   Authorization: authorization string
   Content-MD5: MD5

   <RestoreRequest>
      <Days>NumberOfDays</Days>
      <RestoreJob>
          <Tier>RetrievalOption</Tier>
      </RestoreJob>
   </RestoreRequest>

Request Parameters
------------------

+-----------------+-----------------+--------------------+-------------------------------------------------------------------------------------------+
| Parameter       | Type            | Mandatory (Yes/No) | Description                                                                               |
+=================+=================+====================+===========================================================================================+
| versionId       | String          | No                 | **Explanation**:                                                                          |
|                 |                 |                    |                                                                                           |
|                 |                 |                    | Version ID of the Cold object to be restored                                              |
|                 |                 |                    |                                                                                           |
|                 |                 |                    | **Restrictions**:                                                                         |
|                 |                 |                    |                                                                                           |
|                 |                 |                    | None                                                                                      |
|                 |                 |                    |                                                                                           |
|                 |                 |                    | **Value range**:                                                                          |
|                 |                 |                    |                                                                                           |
|                 |                 |                    | None                                                                                      |
|                 |                 |                    |                                                                                           |
|                 |                 |                    | **Default value**:                                                                        |
|                 |                 |                    |                                                                                           |
|                 |                 |                    | None. If this parameter is not configured, the latest version of the object is specified. |
+-----------------+-----------------+--------------------+-------------------------------------------------------------------------------------------+

Request Headers
---------------

This request uses common headers. For details, see :ref:`Table 3 <obs_04_0007__table25197309>`.

Request Elements
----------------

.. table:: **Table 1** Request elements

   +-----------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Element         | Type            | Mandatory (Yes/No) | Description                                                                                                                                                                                                     |
   +=================+=================+====================+=================================================================================================================================================================================================================+
   | RestoreRequest  | Container       | Yes                | **Explanation**:                                                                                                                                                                                                |
   |                 |                 |                    |                                                                                                                                                                                                                 |
   |                 |                 |                    | Container for the restore information                                                                                                                                                                           |
   |                 |                 |                    |                                                                                                                                                                                                                 |
   |                 |                 |                    | **Restrictions**:                                                                                                                                                                                               |
   |                 |                 |                    |                                                                                                                                                                                                                 |
   |                 |                 |                    | None                                                                                                                                                                                                            |
   |                 |                 |                    |                                                                                                                                                                                                                 |
   |                 |                 |                    | **Value range**:                                                                                                                                                                                                |
   |                 |                 |                    |                                                                                                                                                                                                                 |
   |                 |                 |                    | None                                                                                                                                                                                                            |
   |                 |                 |                    |                                                                                                                                                                                                                 |
   |                 |                 |                    | **Default value**:                                                                                                                                                                                              |
   |                 |                 |                    |                                                                                                                                                                                                                 |
   |                 |                 |                    | None                                                                                                                                                                                                            |
   +-----------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Days            | Integer         | Yes                | **Explanation**:                                                                                                                                                                                                |
   |                 |                 |                    |                                                                                                                                                                                                                 |
   |                 |                 |                    | After an object is restored, a Standard copy of it is generated. This parameter specifies how long the Standard copy can be retained, that is, the validity period of the restored object.                      |
   |                 |                 |                    |                                                                                                                                                                                                                 |
   |                 |                 |                    | **Restrictions**:                                                                                                                                                                                               |
   |                 |                 |                    |                                                                                                                                                                                                                 |
   |                 |                 |                    | The retention period starts from the first 01:00 CET (02:00 CEST) after the object retrieval is initiated.                                                                                                      |
   |                 |                 |                    |                                                                                                                                                                                                                 |
   |                 |                 |                    | For example, if the retention period is one day and the retrieval is initiated any time between 01:00 CET on the 27th day and 01:00 CET on the 28th day, the expiration is always at 01:00 CET on the 29th day. |
   |                 |                 |                    |                                                                                                                                                                                                                 |
   |                 |                 |                    | **Value range**:                                                                                                                                                                                                |
   |                 |                 |                    |                                                                                                                                                                                                                 |
   |                 |                 |                    | The value ranges from 1 to 30, in days.                                                                                                                                                                         |
   |                 |                 |                    |                                                                                                                                                                                                                 |
   |                 |                 |                    | **Default value**:                                                                                                                                                                                              |
   |                 |                 |                    |                                                                                                                                                                                                                 |
   |                 |                 |                    | None                                                                                                                                                                                                            |
   +-----------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | RestoreJob      | Container       | No                 | **Explanation**:                                                                                                                                                                                                |
   |                 |                 |                    |                                                                                                                                                                                                                 |
   |                 |                 |                    | Container for the restore options                                                                                                                                                                               |
   |                 |                 |                    |                                                                                                                                                                                                                 |
   |                 |                 |                    | **Restrictions**:                                                                                                                                                                                               |
   |                 |                 |                    |                                                                                                                                                                                                                 |
   |                 |                 |                    | None                                                                                                                                                                                                            |
   |                 |                 |                    |                                                                                                                                                                                                                 |
   |                 |                 |                    | **Value range**:                                                                                                                                                                                                |
   |                 |                 |                    |                                                                                                                                                                                                                 |
   |                 |                 |                    | None                                                                                                                                                                                                            |
   |                 |                 |                    |                                                                                                                                                                                                                 |
   |                 |                 |                    | **Default value**:                                                                                                                                                                                              |
   |                 |                 |                    |                                                                                                                                                                                                                 |
   |                 |                 |                    | None                                                                                                                                                                                                            |
   +-----------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Tier            | String          | No                 | **Explanation**:                                                                                                                                                                                                |
   |                 |                 |                    |                                                                                                                                                                                                                 |
   |                 |                 |                    | Retrieval speed tier. You can select a tier that suits your retrieval needs.                                                                                                                                    |
   |                 |                 |                    |                                                                                                                                                                                                                 |
   |                 |                 |                    | **Value range**:                                                                                                                                                                                                |
   |                 |                 |                    |                                                                                                                                                                                                                 |
   |                 |                 |                    | -  **Expedited** indicates that objects can be quickly restored from Archive storage within 1 to 5 minutes.                                                                                                     |
   |                 |                 |                    | -  **Standard** indicates that objects can be restored from Archive storage within 3 to 5 hours.                                                                                                                |
   |                 |                 |                    |                                                                                                                                                                                                                 |
   |                 |                 |                    | **Default value**:                                                                                                                                                                                              |
   |                 |                 |                    |                                                                                                                                                                                                                 |
   |                 |                 |                    | Standard                                                                                                                                                                                                        |
   +-----------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Response Syntax
---------------

::

   HTTP/1.1 status_code
   Date: date

Response Headers
----------------

The response to the request uses common headers. For details, see :ref:`Table 1 <obs_04_0013__d0e686>`.

Response Elements
-----------------

This response contains no elements.

Error Responses
---------------

.. table:: **Table 2** List of OBS access error codes

   +--------------------------+--------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Error Code               | Description                                                                                                        | HTTP Status Code      |
   +==========================+====================================================================================================================+=======================+
   | RestoreAlreadyInProgress | **Explanation**:                                                                                                   | 409 Conflict          |
   |                          |                                                                                                                    |                       |
   |                          | The object is being restored. The request conflicts with another.                                                  |                       |
   |                          |                                                                                                                    |                       |
   |                          | ErrorMessage: Object restore is already in progress                                                                |                       |
   +--------------------------+--------------------------------------------------------------------------------------------------------------------+-----------------------+
   | ObjectHasAlreadyRestored | **Explanation**:                                                                                                   | 409 Conflict          |
   |                          |                                                                                                                    |                       |
   |                          | The objects have been restored and the retention period of the objects cannot be shortened.                        |                       |
   |                          |                                                                                                                    |                       |
   |                          | ErrorMessage: After restoring an archived object, you cannot shorten the restoration period of the archived object |                       |
   +--------------------------+--------------------------------------------------------------------------------------------------------------------+-----------------------+
   | MalformedXML             | **Explanation**:                                                                                                   | 400 Bad Request       |
   |                          |                                                                                                                    |                       |
   |                          | Invalid value for the **Days** field (supposed to be an integer)                                                   |                       |
   |                          |                                                                                                                    |                       |
   |                          | ErrorMessage: The XML you provided was not well-formed or did not validate against our published schema            |                       |
   +--------------------------+--------------------------------------------------------------------------------------------------------------------+-----------------------+
   | InvalidArgument          | **Explanation**:                                                                                                   | 400 Bad Request       |
   |                          |                                                                                                                    |                       |
   |                          | Invalid value for the **Days** field (valid range: 1 to 30).                                                       |                       |
   |                          |                                                                                                                    |                       |
   |                          | ErrorMessage: restoration days should be at least 1 and at most 30                                                 |                       |
   +--------------------------+--------------------------------------------------------------------------------------------------------------------+-----------------------+
   | MalformedXML             | **Explanation**:                                                                                                   | 400 Bad Request       |
   |                          |                                                                                                                    |                       |
   |                          | Invalid value for the **Tier** field.                                                                              |                       |
   |                          |                                                                                                                    |                       |
   |                          | ErrorMessage: The XML you provided was not well-formed or did not validate against our published schema            |                       |
   +--------------------------+--------------------------------------------------------------------------------------------------------------------+-----------------------+
   | InvalidObjectState       | **Explanation**:                                                                                                   | 403 Forbidden         |
   |                          |                                                                                                                    |                       |
   |                          | The restored object is not in the Cold storage.                                                                    |                       |
   |                          |                                                                                                                    |                       |
   |                          | ErrorMessage: Restore is not allowed, as object's storage class is not COLD                                        |                       |
   +--------------------------+--------------------------------------------------------------------------------------------------------------------+-----------------------+

Sample Request
--------------

.. code-block:: text

   POST /object?restore HTTP/1.1
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: WED, 01 Jul 2015 04:39:46 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:kaEwOixnSVuS6If3Q0Lnd6kxm5A=
   Content-Length: 183

   <RestoreRequest>
      <Days>2</Days>
      <RestoreJob>
        <Tier>Expedited</Tier>
      </RestoreJob>
   </RestoreRequest>

Sample Response
---------------

::

   HTTP/1.1 202 Accepted
   Server: OBS
   x-obs-request-id: A2F500000163F374CCBB2063F834C6C4
   x-obs-id-2: 32AAAUgAIAABAAAQAAEAABAAAQAAEAABCSLbWIs23RR95NVpkbWlJdlm8Dq+wQBw
   Date: WED, 01 Jul 2015 04:39:46 GMT
   Content-Length: 0
