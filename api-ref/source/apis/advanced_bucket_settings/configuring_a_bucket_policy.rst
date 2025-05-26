:original_name: obs_04_0027.html

.. _obs_04_0027:

Configuring a Bucket Policy
===========================

Functions
---------

This operation creates or modifies policies for buckets. The existing policy in a bucket is overwritten by the policy in the request. You can add as many statements as you would like to a bucket. All these statements in JSON cannot exceed 20 KB.

To perform this operation, the user must be the bucket owner or the bucket owner's IAM user that has permissions required for configuring bucket policies.

Request Syntax
--------------

.. code-block:: text

   PUT /?policy HTTP/1.1
   Host: bucketname.obs.region.example.com
   Date: date
   Authorization: signatureValue
   Policy written in JSON

Request Parameters
------------------

This request contains no message parameters.

Request Headers
---------------

This request uses common headers. For details, see :ref:`Table 3 <obs_04_0007__table25197309>`.

Request Elements
----------------

The request body is a JSON string that contains the bucket policy information.

Response Syntax
---------------

::

   HTTP/1.1 status_code
   Date: date
   Content-Length: length

Response Headers
----------------

The response to the request uses common headers. For details, see :ref:`Table 1 <obs_04_0013__d0e686>`.

Response Elements
-----------------

This response contains no elements.

Error Responses
---------------

No special error responses are returned. For details, see :ref:`Table 2 <obs_04_0115__d0e843>`.

Sample Request 1
----------------

**Grant permissions to an OBS tenant**.

Grant permissions to the tenant whose ID is **783fc6652cf246c096ea836694f71855**.

For details about how to obtain the tenant ID, see :ref:`Obtaining a Domain ID and a User ID <obs_04_0117>`.

.. code-block:: text

   PUT /?policy HTTP/1.1
   Host: examplebucket.obs.region.example.com
   Date: WED, 01 Jul 2015 02:32:25 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:jZiAT8Vx4azWEvPRMWi0X5BpJMA=

   {
       "Statement": [
           {
               "Sid": "Stmt1375240018061",
               "Action": [
                   "GetBucketLogging"
               ],
               "Effect": "Allow",
               "Resource": "logging.bucket",
               "Principal": {
                   "ID": [
                       "domain/783fc6652cf246c096ea836694f71855:user/*"
                   ]
               }
           }
       ]
   }

Sample Response 1
-----------------

::

   HTTP/1.1 204 No Content
   x-obs-request-id: 7B6DFC9BC71DD58B061285551605709
   x-obs-id-2: N0I2REZDOUJDNzFERDU4QjA2MTI4NTU1MTYwNTcwOUFBQUFBQUFBYmJiYmJiYmJD
   Date: WED, 01 Jul 2015 02:32:25 GMT
   Content-Length: 0
   Server: OBS

Sample Request 2
----------------

**Grant permissions to an OBS user**.

The user ID is **71f3901173514e6988115ea2c26d1999**, and the account ID is **783fc6652cf246c096ea836694f71855**.

For details about how to obtain the account ID and user ID, see :ref:`Obtaining a Domain ID and a User ID <obs_04_0117>`.

.. code-block:: text

   PUT /?policy HTTP/1.1
   Host: examplebucket.obs.region.example.com
   Date: WED, 01 Jul 2015 02:33:28 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:jZiAT8Vx4azWEvPRMWi0X5BpJMA=

   {
       "Statement": [
           {
               "Sid": "Stmt1375240018062",
               "Action": [
                   "PutBucketLogging"
               ],
               "Effect": "Allow",
               "Resource": "examplebucket",
               "Principal": {
                   "ID": [
                       "domain/783fc6652cf246c096ea836694f71855:user/71f3901173514e6988115ea2c26d1999"
                   ]
               }
           }
       ]
   }

Sample Response 2
-----------------

::

   HTTP/1.1 204 No Content
   x-obs-request-id: 7B6DFC9BC71DD58B061285551605709
   x-obs-id-2: N0I2REZDOUJDNzFERDU4QjA2MTI4NTU1MTYwNTcwOUFBQUFBQUFBYmJiYmJiYmJD
   Date: WED, 01 Jul 2015 02:33:28 GMT
   Content-Length: 0
   Server: OBS

Sample Request 3
----------------

**Deny all users except the specified one all the operation permissions**.

The user ID is **71f3901173514e6988115ea2c26d1999**, and the account ID is **783fc6652cf246c096ea836694f71855**.

For details about how to obtain the account ID and user ID, see :ref:`Obtaining a Domain ID and a User ID <obs_04_0117>`.

.. code-block:: text

   PUT /?policy HTTP/1.1
   Host: examplebucket.obs.region.example.com
   Date: WED, 01 Jul 2015 02:34:34 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:jZiAT8Vx4azWEvPRMWi0X5BpJMA=

   {
       "Statement": [
           {
               "Effect": "Deny",
               "Action": ["*"],
               "Resource": [
                   "examplebucket/*",
                   "examplebucket"
               ],
               "NotPrincipal": {
                   "ID": [
                       "domain/783fc6652cf246c096ea836694f71855:user/71f3901173514e6988115ea2c26d1999",
                       "domain/783fc6652cf246c096ea836694f71855"
                   ]
               }
           }
        ]
   }

Sample Response 3
-----------------

::

   HTTP/1.1 204 No Content
   x-obs-request-id: A603000001604A7DFE4A4AF31E301891
   x-obs-id-2: BKOvGmTlt6sda5X4G89PuMO4fabObGYmnpRGkaMba1LqPt0fCACEuCMllAObRK1n
   Date: WED, 01 Jul 2015 02:34:34 GMT
   Content-Length: 0
   Server: OBS

Sample Request 4
----------------

**Request to allow only the specified domain name and external link requests that have no referer headers by using the URL validation whitelist.**

URL validation whitelist: **http://storage.example.com**

.. code-block:: text

   PUT /?policy HTTP/1.1
   Host: examplebucket.obs.region.example.com
   Date: WED, 01 Jul 2015 02:34:34 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:jZiAT8Vx4azWEvPRMWi0X5BpJMA=

   {
       "Statement": [{
           "Effect": "Deny",
           "Action": [
           "GetObject",
           "GetObjectVersion"
           ],
           "Principal": {
               "ID": ["*"]
           },
           "Resource": ["examplebucket/*"],
           "Condition": {
               "StringNotLike": {
                   "Referer": [
                   "http://storage.example.com*",
                   "${null}"
                   ]
               }
           }
       }]
   }

Sample Response 4
-----------------

::

   HTTP/1.1 204 No Content
   x-obs-request-id: A603000001604A7DFE4A4AF31E301891
   x-obs-id-2: BKOvGmTlt6sda5X4G89PuMO4fabObGYmnpRGkaMba1LqPt0fCACEuCMllAObRK1n
   Date: WED, 01 Jul 2015 02:34:34 GMT
   Content-Length: 0
   Server: OBS

Sample Request 5
----------------

**Granting permissions to a specified agency**

The tenant whose account ID is **783fc6652cf246c096ea836694f71855** has an agency named **exampleAgency**. This example grants the agency the permission to view logs of the **logging.bucket** bucket.

.. code-block:: text

   PUT /?policy HTTP/1.1
   Host: examplebucket.obs.region.example.com
   Date: WED, 01 Jul 2015 02:32:25 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:jZiAT8Vx4azWEvPRMWi0X5BpJMA=

   {
       "Statement": [
           {
               "Sid": "Stmt1375240018061",
               "Action": [
                   "GetBucketLogging"
               ],
               "Effect": "Allow",
               "Resource": "logging.bucket",
               "Principal": {
                   "ID": [
                       "domain/783fc6652cf246c096ea836694f71855:agency/exampleAgency"
                   ]
               }
           }
       ]
   }

Sample Response 5
-----------------

::

   HTTP/1.1 204 No Content
   x-obs-request-id: A603000001604A7DFE4A4AF31E301891
   x-obs-id-2: BKOvGmTlt6sda5X4G89PuMO4fabObGYmnpRGkaMba1LqPt0fCACEuCMllAObRK1n
   Date: WED, 01 Jul 2015 02:34:34 GMT
   Content-Length: 0
   Server: OBS
