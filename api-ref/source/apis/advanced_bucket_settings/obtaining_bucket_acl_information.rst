:original_name: obs_04_0031.html

.. _obs_04_0031:

Obtaining Bucket ACL Information
================================

Functions
---------

This operation returns the ACL information of a bucket. To obtain the ACL of a bucket, you need to have the **READ_ACP** or **FULL_CONTROL** permission for the bucket.

Request Syntax
--------------

.. code-block:: text

   GET /?acl HTTP/1.1
   Host: bucketname.obs.region.example.com
   Date: date
   Authorization: authorization

Request Parameters
------------------

This request contains no parameter.

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
   Content-Length: length
   Content-Type: application/xml

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <AccessControlPolicy xmlns="http://obs.region.example.com/doc/2015-06-30/">
       <Owner>
           <ID>id</ID>
       </Owner>
       <AccessControlList>
           <Grant>
               <Grantee>
                   <ID>id</ID>
               </Grantee>
               <Permission>permission</Permission>
               <Delivered>false</Delivered>
           </Grant>
       </AccessControlList>
   </AccessControlPolicy>

Response Headers
----------------

The response to the request uses common headers. For details, see :ref:`Table 1 <obs_04_0013__d0e686>`.

Response Elements
-----------------

This response returns information (in the form of elements) about the bucket ACL. :ref:`Table 1 <obs_04_0031__table46938871>` describes the elements.

.. _obs_04_0031__table46938871:

.. table:: **Table 1** Response elements

   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------+
   | Element                           | Description                                                                                                                  |
   +===================================+==============================================================================================================================+
   | Owner                             | Bucket owner                                                                                                                 |
   |                                   |                                                                                                                              |
   |                                   | Type: XML                                                                                                                    |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------+
   | ID                                | Account ID                                                                                                                   |
   |                                   |                                                                                                                              |
   |                                   | Type: string                                                                                                                 |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------+
   | AccessControlList                 | Indicates the ACL that records all users who have permissions to access the bucket and the permissions granted to the users. |
   |                                   |                                                                                                                              |
   |                                   | Type: XML                                                                                                                    |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------+
   | Grant                             | Container for the grantee and the granted permissions                                                                        |
   |                                   |                                                                                                                              |
   |                                   | Type: XML                                                                                                                    |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------+
   | Grantee                           | Grantee information                                                                                                          |
   |                                   |                                                                                                                              |
   |                                   | Type: XML                                                                                                                    |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------+
   | Canned                            | Grants permissions to all users.                                                                                             |
   |                                   |                                                                                                                              |
   |                                   | Type: Enumeration The value must be **Everyone**.                                                                            |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------+
   | Delivered                         | Indicates whether the bucket ACL is applied to objects in the bucket.                                                        |
   |                                   |                                                                                                                              |
   |                                   | Type: boolean                                                                                                                |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------+
   | Permission                        | Grantee's permission for a bucket                                                                                            |
   |                                   |                                                                                                                              |
   |                                   | Type: string                                                                                                                 |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------+

Error Responses
---------------

No special error responses are involved. For details about error responses, see :ref:`Table 2 <obs_04_0115__d0e843>`.

Sample Request
--------------

.. code-block:: text

   GET /?acl HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: WED, 01 Jul 2015 02:39:28 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:X7HtzGsIEkzJbd8vo1DRu30vVrs=

Sample Response
---------------

::

   HTTP/1.1 200 OK
   Server: OBS
   x-obs-request-id: BF260000016436B69D82F14E93528658
   x-obs-id-2: 32AAAQAAEAABAAAQAAEAABAAAQAAEAABCSjTh8661+HF5y8uAnTOBIpNO133hji+
   Content-Type: application/xml
   Date: WED, 01 Jul 2015 02:39:28 GMT
   Content-Length: 784

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <AccessControlPolicy xmlns="http://obs.example.com/doc/2015-06-30/">
     <Owner>
       <ID>b4bf1b36d9ca43d984fbcb9491b6fce9</ID>
     </Owner>
     <AccessControlList>
       <Grant>
         <Grantee>
           <ID>b4bf1b36d9ca43d984fbcb9491b6fce9</ID>
         </Grantee>
         <Permission>FULL_CONTROL</Permission>
       </Grant>
       <Grant>
         <Grantee>
           <ID>783fc6652cf246c096ea836694f71855</ID>
         </Grantee>
         <Permission>READ</Permission>
         <Delivered>false</Delivered>
       </Grant>
       <Grant>
         <Grantee>
           <Canned>Everyone</Canned>
         </Grantee>
         <Permission>READ_ACP</Permission>
       </Grant>
     </AccessControlList>
   </AccessControlPolicy>
