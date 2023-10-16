:original_name: obs_04_0072.html

.. _obs_04_0072:

Obtaining the Static Website Hosting Configuration of a Bucket
==============================================================

Functions
---------

You can perform this operation to get the static website hosting configuration of a bucket.

To perform this operation, you must have the **GetBucketWebsite** permission. By default, only the bucket owner can perform this operation. The bucket owner can grant the permission to other users by configuring the bucket policy or user policy.

Request Syntax
--------------

.. code-block:: text

   GET /?website HTTP/1.1
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
   Date: date
   Content-Type: type
   Content-Length: length
   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <WebsiteConfiguration xmlns="http://obs.region.example.com/doc/2015-06-30/">
       <RedirectAllRequestsTo>
           <HostName>hostName</HostName>
       </RedirectAllRequestsTo>
   </WebsiteConfiguration>

Response Headers
----------------

The response to the request uses common headers. For details, see :ref:`Table 1 <obs_04_0013__d0e686>`.

Response Elements
-----------------

This response contains elements the same as those used by the PutBucketWebsite request. For details, see :ref:`Request Elements <obs_04_0071__section12388580153122>`.

Error Responses
---------------

:ref:`Table 1 <obs_04_0072__table12494839144020>` describes possible special errors in this request.

.. _obs_04_0072__table12494839144020:

.. table:: **Table 1** Special error

   +----------------------------+-------------------------------------------+------------------+
   | Error Code                 | Description                               | HTTP Status Code |
   +============================+===========================================+==================+
   | NoSuchWebsiteConfiguration | The website configuration does not exist. | 404 Not Found    |
   +----------------------------+-------------------------------------------+------------------+

For other errors, see :ref:`Table 2 <obs_04_0115__d0e843>`.

Sample Request
--------------

.. code-block:: text

   GET /?website HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: WED, 01 Jul 2015 03:41:54 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:Yxt1Ru+feHE0S94R7dcBp+hfLnI=

Sample Response
---------------

::

   HTTP/1.1 200 OK
   Server: OBS
   x-obs-request-id: BF2600000164363442EC03A8CA3DD7F5
   x-obs-id-2: 32AAAQAAEAABAAAQAAEAABAAAQAAEAABCSFbGOmlN0BVp1kbwN3har8jbVvtKEKN
   Content-Type: application/xml
   Date: WED, 01 Jul 2015 03:41:54 GMT
   Content-Length: 250

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <WebsiteConfiguration xmlns="http://obs.region.example.com/doc/2015-06-30/">
     <RedirectAllRequestsTo>
       <HostName>www.example.com</HostName>
     </RedirectAllRequestsTo>
   </WebsiteConfiguration>
