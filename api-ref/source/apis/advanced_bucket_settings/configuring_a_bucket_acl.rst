:original_name: obs_04_0030.html

.. _obs_04_0030:

Configuring a Bucket ACL
========================

Functions
---------

This operation controls access permissions for buckets. By default, only the creator of a bucket has the permission to read and write the bucket. You can also set other access permissions. For example, you can set a public read policy to grant the read permission to all users.

You can configure an ACL when creating a bucket, and modify or obtain the ACLs of existing buckets using the API operations. A bucket ACL supports a maximum of 100 grants. The PUT method is idempotent. With this method, a new bucket ACL will overwrite the previous bucket ACL. To modify or delete an ACL, you just need to create a new one using the PUT method.

Request Syntax
--------------

.. code-block:: text

   PUT /?acl HTTP/1.1
   Host: bucketname.obs.region.example.com
   Date: date
   Authorization: authorization
   Content-Type: application/xml
   Content-Length: length

   <AccessControlPolicy>
       <Owner>
           <ID>ID</ID>
       </Owner>
       <AccessControlList>
           <Grant>
               <Grantee>
                  <ID>domainId</ID>
               </Grantee>
               <Permission>permission</Permission>
               <Delivered>false</Delivered>
           </Grant>
       </AccessControlList>
   </AccessControlPolicy>

Request Parameters
------------------

This request contains no parameters.

Request Headers
---------------

You can change the ACL of a bucket by using the header settings. Each ACL configured with the header setting has a set of predefined grantees and authorized permissions. If you want to authorize access permissions by adding the header to a request, you must add the following header and specify the value.

.. table:: **Table 1** Optional header for specifying canned ACLs

   +-----------------+-----------------+--------------------+-----------------------------------+
   | Header          | Type            | Mandatory (Yes/No) | Description                       |
   +=================+=================+====================+===================================+
   | x-obs-acl       | String          | No                 | **Definition**:                   |
   |                 |                 |                    |                                   |
   |                 |                 |                    | Uses the canned ACL for a bucket. |
   |                 |                 |                    |                                   |
   |                 |                 |                    | **Constraints**:                  |
   |                 |                 |                    |                                   |
   |                 |                 |                    | None                              |
   |                 |                 |                    |                                   |
   |                 |                 |                    | **Range**:                        |
   |                 |                 |                    |                                   |
   |                 |                 |                    | -  private                        |
   |                 |                 |                    | -  public-read                    |
   |                 |                 |                    | -  public-read-write              |
   |                 |                 |                    | -  public-read-delivered          |
   |                 |                 |                    | -  public-read-write-delivered    |
   |                 |                 |                    |                                   |
   |                 |                 |                    | .                                 |
   |                 |                 |                    |                                   |
   |                 |                 |                    | **Default value**:                |
   |                 |                 |                    |                                   |
   |                 |                 |                    | private                           |
   +-----------------+-----------------+--------------------+-----------------------------------+

Request Elements
----------------

This request carries ACL information in elements to specify an ACL. :ref:`Table 3 <obs_04_0007__table25197309>` describes the elements.

.. table:: **Table 2** Additional request elements

   +-------------------+-----------------+--------------------+----------------------------------------------------------------------------------------------------------------------------------+
   | Element           | Type            | Mandatory (Yes/No) | Description                                                                                                                      |
   +===================+=================+====================+==================================================================================================================================+
   | Owner             | XML             | Yes                | **Definition**:                                                                                                                  |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | Owner information of a bucket. Owner is a parent node of ID.                                                                     |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | **Constraints**:                                                                                                                 |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | None                                                                                                                             |
   +-------------------+-----------------+--------------------+----------------------------------------------------------------------------------------------------------------------------------+
   | ID                | String          | Yes                | **Definition**:                                                                                                                  |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | Account ID of the bucket owner.                                                                                                  |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | **Constraints**:                                                                                                                 |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | None                                                                                                                             |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | **Range**:                                                                                                                       |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | None                                                                                                                             |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | **Default value**:                                                                                                               |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | None                                                                                                                             |
   +-------------------+-----------------+--------------------+----------------------------------------------------------------------------------------------------------------------------------+
   | AccessControlList | XML             | Yes                | **Definition**:                                                                                                                  |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | Access control list, which is the parent node of Grant.                                                                          |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | **Constraints**:                                                                                                                 |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | None                                                                                                                             |
   +-------------------+-----------------+--------------------+----------------------------------------------------------------------------------------------------------------------------------+
   | Grant             | XML             | No                 | **Definition**:                                                                                                                  |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | Used to identify users and user permissions. It is the parent node of Grantee, Permission and Delivered.                         |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | **Constraints**:                                                                                                                 |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | A single bucket can contain at most 100 grants in its ACL.                                                                       |
   +-------------------+-----------------+--------------------+----------------------------------------------------------------------------------------------------------------------------------+
   | Grantee           | XML             | No                 | **Definition**:                                                                                                                  |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | Records user information and is the parent node of the authorized account ID.                                                    |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | **Constraints**:                                                                                                                 |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | None                                                                                                                             |
   +-------------------+-----------------+--------------------+----------------------------------------------------------------------------------------------------------------------------------+
   | ID                | String          | Yes                | **Definition**:                                                                                                                  |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | Account ID of the authorized user.                                                                                               |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | **Constraints**:                                                                                                                 |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | None                                                                                                                             |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | **Range**:                                                                                                                       |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | None                                                                                                                             |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | **Default value**:                                                                                                               |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | None                                                                                                                             |
   +-------------------+-----------------+--------------------+----------------------------------------------------------------------------------------------------------------------------------+
   | Canned            | String          | No                 | **Definition**:                                                                                                                  |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | Grants permissions to all users.                                                                                                 |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | **Constraints**:                                                                                                                 |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | None                                                                                                                             |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | **Range**:                                                                                                                       |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | Everyone                                                                                                                         |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | **Default value**:                                                                                                               |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | None                                                                                                                             |
   +-------------------+-----------------+--------------------+----------------------------------------------------------------------------------------------------------------------------------+
   | Permission        | String          | Yes                | **Definition**:                                                                                                                  |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | Permissions to be granted.                                                                                                       |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | **Constraints**:                                                                                                                 |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | None                                                                                                                             |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | **Range**:                                                                                                                       |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | -  READ: Grants the permission to obtain the list of objects in the bucket and the metadata of the bucket.                       |
   |                   |                 |                    | -  READ_ACP: Grants the permission to read the ACL of the bucket.                                                                |
   |                   |                 |                    | -  WRITE: Grants the permission to upload objects to the bucket and allows to delete and overwrite existing objects in a bucket. |
   |                   |                 |                    | -  WRITE_ACP: Grants the permission to update the ACL of the bucket.                                                             |
   |                   |                 |                    | -  FULL_CONTROL: Grants the permission to read, write, read ACL, and write ACL of the bucket.                                    |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | **Default value**:                                                                                                               |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | None                                                                                                                             |
   +-------------------+-----------------+--------------------+----------------------------------------------------------------------------------------------------------------------------------+
   | Delivered         | Boolean         | No                 | **Definition**:                                                                                                                  |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | Whether the bucket ACL is applied to all objects in the bucket.                                                                  |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | **Constraints**:                                                                                                                 |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | None                                                                                                                             |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | **Range**:                                                                                                                       |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | -  true: The bucket ACL is applied to all objects in the bucket.                                                                 |
   |                   |                 |                    | -  false: The bucket ACL is not applied to any objects in the bucket.                                                            |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | **Default value**:                                                                                                               |
   |                   |                 |                    |                                                                                                                                  |
   |                   |                 |                    | false                                                                                                                            |
   +-------------------+-----------------+--------------------+----------------------------------------------------------------------------------------------------------------------------------+

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

No special error responses are returned. For details about error responses, see :ref:`Table 2 <obs_04_0115__d0e843>`.

Sample Request
--------------

.. code-block:: text

   PUT /?acl HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: WED, 01 Jul 2015 02:37:22 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:iqSPeUBl66PwXDApxjRKk6hlcN4=
   Content-Length: 727

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

Sample Response
---------------

::

   HTTP/1.1 200 OK
   Server: OBS
   x-obs-request-id: BF2600000164361F2954B4D063164704
   x-obs-id-2: 32AAAQAAEAABSAAgAAEAABAAAQAAEAABCT78HTIBuhe0FbtSptrb/akwELtwyPKs
   Date: WED, 01 Jul 2015 02:37:22 GMT
   Content-Length: 0
