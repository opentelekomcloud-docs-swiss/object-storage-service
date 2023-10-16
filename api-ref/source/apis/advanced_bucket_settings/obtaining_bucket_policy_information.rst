:original_name: obs_04_0028.html

.. _obs_04_0028:

Obtaining Bucket Policy Information
===================================

Functions
---------

This operation uses the sub-resources of policy to return the policy information of a specified bucket.

To perform this operation, the user must be the bucket owner or the bucket owner's IAM user that has permissions required for obtaining bucket policies.

This operation cannot be performed in the following scenarios, and the 404 error code "NoSuchBucketPolicy" is returned:

-  The specified bucket policy does not exist.
-  The standard bucket policy is set to **Private** and no custom bucket policy is configured.

Request Syntax
--------------

.. code-block:: text

   GET /?policy HTTP/1.1
   Host: bucketname.obs.region.example.com
   Date: date
   Authorization: authorization

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

::

   HTTP/1.1 status_code
   Content-Type: application/xml
   Date: date
   Policy Content

Response Headers
----------------

The response to the request uses common headers. For details, see :ref:`Table 1 <obs_04_0013__d0e686>`.

Response Elements
-----------------

The response body is a JSON string that contains the bucket policy information.

Error Responses
---------------

No special error responses are returned. For details, see :ref:`Table 2 <obs_04_0115__d0e843>`.

Sample Request
--------------

.. code-block:: text

   GET /?policy HTTP/1.1
   Host: examplebucket.obs.region.example.com
   Date: WED, 01 Jul 2015 02:35:46 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:jZiAT8Vx4azWEvPRMWi0X5BpJMA=

Sample Response
---------------

::

   HTTP/1.1 200 OK
   x-obs-request-id: A603000001604A7DFE4A4AF31E301891
   x-obs-id-2: BKOvGmTlt6sda5X4G89PuMO4fabObGYmnpRGkaMba1LqPt0fCACEuCMllAObRK1n
   Date: WED, 01 Jul 2015 02:35:46 GMT
   Content-Length: 509
   Server: OBS

   {
       "Statement":[
           {
               "Sid":"Stmt1375240018061",
               "Effect":"Allow",
               "Principal":{
                   "ID":[
                       "domain/domainiddomainiddomainiddo006666:user/useriduseriduseriduseridus004001",
                       "domain/domainiddomainiddomainiddo006667:user/*"
                   ]
               },
               "Action":[
                   "*"
               ],
               "Resource":[
                   "examplebucket"
               ]
           }
       ]
   }
