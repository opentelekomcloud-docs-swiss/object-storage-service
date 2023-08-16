:original_name: en-us_topic_0125560316.html

.. _en-us_topic_0125560316:

PUT Bucket policy
=================

You can use this operation to create or modify a policy on a bucket. If the bucket already has a policy, the policy will be overwritten by the one specified in this request.

Only the bucket owner or users granted the **s3:PutBucketPolicy** permission can create or modify the bucket policy.

Request Syntax
--------------

.. code-block:: text

   PUT /?policy HTTP/1.1
    User-Agent: agent
    Host: bucketname.obs.example.com
    Accept: */*
    Date: date
    Authorization: signatureValue
    Content-Length: length

    Policy written in JSON

Request Parameters
------------------

This request involves no parameters.

Request Headers
---------------

This request uses common headers. For details about common request headers, see section :ref:`Common Request Headers <en-us_topic_0125560462>`.

Request Elements
----------------

The request body is a JSON string containing bucket policies. For details about JSON elements, see :ref:`Bucket Policy <en-us_topic_0125560422>`.

Response Syntax
---------------

.. code-block::

   HTTP/1.1 status_code
    Server: Server Name
    x-amz-request-id: request id
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    x-amz-id-2: id
    Date: date

Response Headers
----------------

This response uses common headers. For details about common response headers, see section :ref:`Common Response Headers <en-us_topic_0125560484>`.

Response elements
-----------------

This response involves no elements.

Error Responses
---------------

No special error responses are returned. For details about error responses, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`.

Sample Request: Grant OBS account permission
--------------------------------------------

Account's domain ID is **783fc6652cf246c096ea836694f71855**.

.. code-block:: text

   PUT /?policy HTTP/1.1
    User-Agent: curl/7.19.0
    Host: bucketname.obs.example.com
    Date: Mon, 27 Sep 2010 01:40:03 GMT
    Accept: */*
    Authorization: AWS UDSIAMSTUBTEST000002:1YPpMv6hAokMd/r6Ft5/6SZANDw=
    Content-Length: 223

    {
       "Id": "Policy1375342051334",
       "Statement": [
           {
               "Sid": "Stmt1375240018061",
               "Action": [
                   "s3:GetBucketLogging"
               ],
               "Effect": "Allow",
               "Resource": "arn:aws:s3:::logging.bucket3",
               "Principal": {
                   "AWS": [
                       "arn:aws:iam::783fc6652cf246c096ea836694f71855:root"
                    ]
                }
            }
        ]
    }

Sample Response: Grant OBS account permission
---------------------------------------------

.. code-block::

   HTTP/1.1 204 No Content
    Server: OBS
    x-amz-request-id: 7B6DFC9BC71DD58B061285551605709
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    x-amz-id-2: N0I2REZDOUJDNzFERDU4QjA2MTI4NTU1MTYwNTcwOUFBQUFBQUFBYmJiYmJiYmJD
    Date: Mon, 27 Sep 2010 01:40:03 GMT

Sample Request: Grant OBS user permission
-----------------------------------------

User ID is **71f3901173514e6988115ea2c26d1999** and Account's domain ID is **219d520ceac84c5a98b237431a2cf4c2**.

.. code-block:: text

   PUT /?policy HTTP/1.1
   User-Agent: curl/7.19.0
   Host: bucketname.obs.example.com
   Accept: */*
   Date: Mon, 27 Sep 2010 01:40:03 GMT
   Authorization: AWS UDSIAMSTUBTEST000002:1YPpMv6hAokMd/r6Ft5/6SZANDw=
   Content-Length: 256

   {
       "Id": "Policy1375342051335",
       "Statement": [
           {
               "Sid": "Stmt1375240018062",
               "Action": [
                   "s3:PutBucketLogging"
               ],
               "Effect": "Allow",
               "Resource": "arn:aws:s3:::logging.bucket3",
               "Principal": {
                   "AWS": [
                       "arn:aws:iam::219d520ceac84c5a98b237431a2cf4c2:user/71f3901173514e6988115ea2c26d1999"
                   ]
               }
           }
       ]
   }

Sample Response: Grant OBS user permission
------------------------------------------

.. code-block::

   HTTP/1.1 204 No Content
   x-amz-request-id: 7B6DFC9BC71DD58B061285551605709
   x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
   x-amz-id-2: N0I2REZDOUJDNzFERDU4QjA2MTI4NTU1MTYwNTcwOUFBQUFBQUFBYmJiYmJiYmJD
   Date: Mon, 27 Sep 2010 01:40:03 GMT

Sample Request: Deny Operations of an OBS User
----------------------------------------------

The user ID is **useriduseriduseriduseridus004001** and the account's domain ID is **domainiddomainiddomainiddo006666**.

.. code-block:: text

   PUT /?policy HTTP/1.1
   User-Agent: curl/7.19.0
   Host: testbucketpolicy.obs.example.com
   Accept: */*
   Date: Mon, 27 Sep 2010 01:40:03 GMT
   Authorization: AWS UDSIAMSTUBTEST000002:1YPpMv6hAokMd/r6Ft5/6SZANDw=
   Content-Length: 311

   {
       "Statement": [
           {
               "Effect": "Deny",
               "Action": [
                   "s3:*"
               ],
               "Resource": [
                   "arn:aws:s3:::testbucketpolicy/*",
                   "arn:aws:s3:::testbucketpolicy"
               ],
               "Principal": {
                   "AWS": [
                       "arn:aws:iam::domainiddomainiddomainiddo006666:user/useriduseriduseriduseridus004001",
                       "arn:aws:iam::domainiddomainiddomainiddo006666:root"
                   ]
               }
           }
        ]
   }

Sample Response
---------------

.. code-block::

   HTTP/1.1 204 No Content
   x-amz-request-id: A603000001604A7DFE4A4AF31E301891
   x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
   x-amz-id-2: BKOvGmTlt6sda5X4G89PuMO4fabObGYmnpRGkaMba1LqPt0fCACEuCMllAObRK1n
   Date: Mon, 27 Sep 2010 01:40:03 GMT
