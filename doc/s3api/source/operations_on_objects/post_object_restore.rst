:original_name: en-us_topic_0125560388.html

.. _en-us_topic_0125560388:

POST Object restore
===================

If you want to obtain the content of a Cold object, restore the object first. Then, you can download the object.

Versioning
----------

By default, the object of the latest version is restored. If the object has a delete marker, status code 404 is returned. To restore an object of a specified version, the **versionId** parameter can be used to specify the desired version.

Request Syntax
--------------

.. code-block:: text

   POST /ObjectName?restore&versionId=VersionID HTTP/1.1
   User-Agent: agent
   Host: bucketname.obs.example.com
   Accept: */*
   Date: date
   Authorization: authorization string
   Content-MD5: MD5

   <RestoreRequest>
      <Days>NumberOfDays</Days>
      <GlacierJobParameters>
          <Tier>RetrievalOption</Tier>
      </GlacierJobParameters>
   </RestoreRequest>

Request Parameters
------------------

+-----------------------+-----------------------------------------------+-----------------------+
| Parameter             | Description                                   | Remarks               |
+=======================+===============================================+=======================+
| versionId             | Version ID of the Cold object to be restored. | Optional              |
|                       |                                               |                       |
|                       | Type: String                                  |                       |
+-----------------------+-----------------------------------------------+-----------------------+

Request Headers
---------------

This request uses common headers. For details, see section :ref:`Common Request Headers <en-us_topic_0125560462>`.

Request Elements
----------------

.. table:: **Table 1** Request elements

   +-----------------------+------------------------------------------------------------------------------------------------------+-----------------------+
   | Element               | Description                                                                                          | Remarks               |
   +=======================+======================================================================================================+=======================+
   | RestoreRequest        | Container for restore information.                                                                   | Mandatory             |
   |                       |                                                                                                      |                       |
   |                       | Type: Container                                                                                      |                       |
   +-----------------------+------------------------------------------------------------------------------------------------------+-----------------------+
   | Days                  | Indicates the retention period of the restored object. The value is an integer ranging from 1 to 30. | Mandatory             |
   |                       |                                                                                                      |                       |
   |                       | Type: Positive integer                                                                               |                       |
   +-----------------------+------------------------------------------------------------------------------------------------------+-----------------------+
   | GlacierJobParameters  | Container for Glacier job parameters.                                                                | Optional              |
   |                       |                                                                                                      |                       |
   |                       | Type: Container                                                                                      |                       |
   +-----------------------+------------------------------------------------------------------------------------------------------+-----------------------+
   | Tier                  | Indicates the retrieval option used when restoring a Cold object.                                    | Optional              |
   |                       |                                                                                                      |                       |
   |                       | Valid Values: **Expedited**, **Standard**, and **Bulk**                                              |                       |
   |                       |                                                                                                      |                       |
   |                       | -  **Expedited**: indicates that data can be restored within 1 to 5 minutes.                         |                       |
   |                       |                                                                                                      |                       |
   |                       | -  **Standard**: indicates that data can be restored within 3 to 5 hours.                            |                       |
   |                       |                                                                                                      |                       |
   |                       | -  **Bulk**: indicates that data can be restored within 5 to 12 hours.                               |                       |
   |                       |                                                                                                      |                       |
   |                       | The default value is **Standard**.                                                                   |                       |
   |                       |                                                                                                      |                       |
   |                       | Type: String                                                                                         |                       |
   +-----------------------+------------------------------------------------------------------------------------------------------+-----------------------+

Response Syntax
---------------

.. code-block::

   HTTP/1.1 status_code
   Server: server
   x-amz-request-id: request id
   x-amz-id-2: id
   x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
   Date: date

Response Headers
----------------

This response uses common headers. For details, see section :ref:`Common Response Headers <en-us_topic_0125560484>`.

Response Elements
-----------------

This response involves no elements.

Error Responses
---------------

.. table:: **Table 2** List of OBS error codes

   +--------------------------+--------------------------------------------------------------------------------------------------------------+-----------------------+
   | Error Code               | Description                                                                                                  | HTTP Status Code      |
   +==========================+==============================================================================================================+=======================+
   | RestoreAlreadyInProgress | The object is being restored. The request conflicts with another.                                            | 409 Conflict          |
   |                          |                                                                                                              |                       |
   |                          | ErrorMessage: Object restore is already in progress                                                          |                       |
   +--------------------------+--------------------------------------------------------------------------------------------------------------+-----------------------+
   | ObjectHasAlreadyRestored | The object has been restored and the retention period of the restored object is not allowed to be shortened. | 409 Conflict          |
   |                          |                                                                                                              |                       |
   |                          | ErrorMessage: After restoring a Cold object, you cannot shorten the restoration period of the Cold object    |                       |
   +--------------------------+--------------------------------------------------------------------------------------------------------------+-----------------------+
   | MalformedXML             | Invalid value for the **Days** field (not an integer)                                                        | 400 Bad Request       |
   |                          |                                                                                                              |                       |
   |                          | ErrorMessage: The XML you provided was not well-formed or did not validate against our published schema      |                       |
   +--------------------------+--------------------------------------------------------------------------------------------------------------+-----------------------+
   | InvalidArgument          | The value of the **Days** field is not within the range of 1to 30.                                           | 400 Bad Request       |
   |                          |                                                                                                              |                       |
   |                          | ErrorMessage: restoration days should be at least 1 and at most 30                                           |                       |
   +--------------------------+--------------------------------------------------------------------------------------------------------------+-----------------------+
   | MalformedXML             | Invalid value for the **Tier** field.                                                                        | 400 Bad Request       |
   |                          |                                                                                                              |                       |
   |                          | ErrorMessage: The XML you provided was not well-formed or did not validate against our published schema      |                       |
   +--------------------------+--------------------------------------------------------------------------------------------------------------+-----------------------+
   | InvalidObjectState       | The restored object is not a Cold object.                                                                    | 403 Forbidden         |
   |                          |                                                                                                              |                       |
   |                          | ErrorMessage: Restore is not allowed, as object's storage class is not GLACIER                               |                       |
   +--------------------------+--------------------------------------------------------------------------------------------------------------+-----------------------+

Sample Request
--------------

.. code-block:: text

   POST /object?restore HTTP/1.1
   User-Agent: curl/7.19.7 (x86_64-suse-linux-gnu) libcurl/7.19.7 OpenSSL/0.9.8j zlib/1.2.7 libidn/1.10
   Host: bucketname.obs.example.com
   Accept: */*
   Date: Tue, 07 Mar 2017 08:54:09 +0000
   Authorization: AWS UDSIAMSTUBTEST000002:kaEwOixnSVuS6If3Q0Lnd6kxm5A=
   Content-Length: 183
   Expect: 100-continue

   <RestoreRequest xmlns="http://s3.amazonaws.com/doc/2006-3-01">
      <Days>3</Days>
      <GlacierJobParameters>
          <Tier>Expedited</Tier>
      </GlacierJobParameters>
   </RestoreRequest>

Sample Response
---------------

.. code-block::

   HTTP/1.1 100 Continue
   HTTP/1.1 202 Accepted
   Server: OBS
   x-amz-request-id: 00013235600000015AA7FE74DCAE68RC
   x-amz-id-2: W5NZYb1KhRt+updrvY4OCgmESg7R1lsdR3CMA450Gq2jtrc07YAThUJmV8mPg9D4   x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
   Content-Length: 0
   Date: Tue, 07 Mar 2017 08:59:15 GMT
