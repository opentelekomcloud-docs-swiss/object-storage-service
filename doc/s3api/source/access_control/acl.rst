:original_name: en-us_topic_0125560406.html

.. _en-us_topic_0125560406:

ACL
===

A default ACL is generated during the creation of a bucket or an object. The entries in an ACL define permission granted to accounts. You can use PUT Bucket/Object acl to create a new ACL for a bucket or an object.

-  :ref:`Table 1 <en-us_topic_0125560406__table49181932>` gives a description of each Grantee and their access permission.

.. _en-us_topic_0125560406__table49181932:

.. table:: **Table 1** Grantees in OBS

   +----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Grantee                    | Description                                                                                                                                                                                                                               |
   +============================+===========================================================================================================================================================================================================================================+
   | OBS user                   | The permission to access a bucket or object can be granted to any OBS user. An OBS user can access the bucket or object in OBS using its AK and SK.                                                                                       |
   +----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Registered user group user | The permission to access a bucket or object can be granted to all users in a registered user group. A user in a registered user group can access the bucket or object in OBS using its AK and SK. This group represents all OBS accounts. |
   +----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Anonymous user             | The permission to access a bucket or object can be granted to anonymous users. After the permission is granted, all users can access the bucket or object.                                                                                |
   +----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Log delivery user group    | The permission to access a bucket can be granted to all users in a log delivery user group. A user in a log delivery user group can access the bucket. The permission is mainly used in log management.                                   |
   +----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

-  ACL syntax

The request for modifying or setting the ACL of a bucket or object must contain an ACL in the following syntax:

.. code-block::

   <AccessControlPolicy>
       <Owner>
           <ID>id</ID>
           <DisplayName>displayname</DisplayName>
       </Owner>
       <AccessControlList>
           <Grant>
               <Grantee>grantee</Grantee>
               <Permission>permission</Permission>
           </Grant>
           <Grant>…………</Grant>
       </AccessControlList>
   </AccessControlPolicy>

In the preceding ACL, **permission** indicates one of the five permission types supported by OBS. For details about the permission, see :ref:`Table 2 <en-us_topic_0125560406__table39984204>`. The format of content in **Grantee** varies with the grantee.

#. An OBS user as the grantee

   .. code-block::

      <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="CanonicalUser">
          <ID>DomainId</ID>
          <DisplayName>displayname</DisplayName>
      </Grantee>

#. A registered user group user as the grantee

   .. code-block::

      <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="Group">
          <URI>http://acs.amazonaws.com/groups/global/AuthenticatedUsers</URI>
      </Grantee>

#. An anonymous user as the grantee

   .. code-block::

      <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="Group">
          <URI>http://acs.amazonaws.com/groups/global/AllUsers</URI>
      </Grantee>

#. Log delivery user group user as the grantee

   .. code-block::

      <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="Group">
          <URI>http://acs.amazonaws.com/groups/s3/LogDelivery</URI>
      </Grantee>

.. _en-us_topic_0125560406__table39984204:

.. table:: **Table 2** Permission on an OBS bucket or object

   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | Permission                        | Description                                                                                                                        |
   +===================================+====================================================================================================================================+
   | READ                              | A grantee with such permission for a bucket can obtain the list of objects in the bucket and its metadata.                         |
   |                                   |                                                                                                                                    |
   |                                   | A grantee with such permission for an object can obtain the object content and metadata.                                           |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | WRITE                             | A grantee with such permission for a bucket can upload, overwrite, and delete any object in the bucket.                            |
   |                                   |                                                                                                                                    |
   |                                   | Such permission for an object is **NOT** applicable.                                                                               |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | READ_ACP                          | A grantee with such permission can obtain the ACL of a bucket or object. A bucket or object owner has such permission permanently. |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | WRITE_ACP                         | A grantee with such permission can update the ACL of a bucket or object. A bucket or object owner has such permission permanently. |
   |                                   |                                                                                                                                    |
   |                                   | A grantee with such permission can modify the access control policy to obtain desired access permission.                           |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | FULL_CONTROL                      | A grantee with such permission for a bucket has **READ**, **WRITE**, **READ_ACP**, and **WRITE_ACP** permission.                   |
   |                                   |                                                                                                                                    |
   |                                   | A grantee with such permission for an object has **READ**, **READ_ACP**, and **WRITE_ACP** permission.                             |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------+

.. note::

   #. A request can contain a maximum of 100 grants.
   #. The ACL of a bucket or object is overwritten after permission associated with the bucket or object is granted

The following table shows how each of the ACL permissions maps to the corresponding access policy permissions. As you can see, access policy allows more permissions than ACL does, you use ACL to primarily grant basic read/write permissions.

.. table:: **Table 3** ACL permissions map

   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ACL                   | Corresponding access policy permissions when the ACL permission is granted on a bucket                                                                                               | Corresponding access policy permissions when the ACL permission is granted on an object                                                                                      |
   |                       |                                                                                                                                                                                      |                                                                                                                                                                              |
   | Permission            |                                                                                                                                                                                      |                                                                                                                                                                              |
   +=======================+======================================================================================================================================================================================+==============================================================================================================================================================================+
   | READ                  | s3:ListBucket, s3:ListBucketVersions, and s3:ListBucketMultipartUploads                                                                                                              | s3:GetObject and s3:GetObjectVersion                                                                                                                                         |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | WRITE                 | s3:PutObject and s3:DeleteObject.                                                                                                                                                    | Not applicable                                                                                                                                                               |
   |                       |                                                                                                                                                                                      |                                                                                                                                                                              |
   |                       | In addition, when the grantee is the bucket owner, granting WRITE permission in a bucket ACL allows the s3:DeleteObjectVersion action to be performed on any version in that bucket. |                                                                                                                                                                              |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | READ_ACP              | s3:GetBucketAcl                                                                                                                                                                      | s3:GetObjectAcl and s3:GetObjectVersionAcl                                                                                                                                   |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | WRITE_ACP             | s3:PutBucketAcl                                                                                                                                                                      | s3:PutObjectAcl and s3:PutObjectVersionAcl                                                                                                                                   |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | FULL_CONTROL          | It is equivalent to granting READ, WRITE, READ_ACP, and WRITE_ACP ACL permissions. Accordingly, this ACL permission maps to combination of corresponding access policy permissions.  | It is equivalent to granting READ, READ_ACP, and WRITE_ACP ACL permissions. Accordingly, this ACL permission maps to combination of corresponding access policy permissions. |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Access Control Policies
-----------------------

You can set an access control policy in **x-amz-acl** HTTP header when creating a bucket or uploading an object. Available access control policies are predefined in OBS, as described in :ref:`Table 4 <en-us_topic_0125560406__table40200743>`.

.. _en-us_topic_0125560406__table40200743:

.. table:: **Table 4** Predefined access control policies

   +---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Policy                    | Description                                                                                                                                                                               |
   +===========================+===========================================================================================================================================================================================+
   | private                   | Indicates that the owner of a bucket or object has **FULL_CONTROL** permission for the bucket or object. Other users have no permission to access the bucket or object.                   |
   +---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | public-read               | Indicates that the owner of a bucket or object has **FULL_CONTROL** permission for the bucket or object. Other users including anonymous users have **READ** permission.                  |
   +---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | public-read-write         | Indicates that the owner of a bucket or object has **FULL_CONTROL** permission for the bucket or object. Other users including anonymous users have **READ** and **WRITE** permission.    |
   +---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | authenticated-read        | Indicates that the owner of a bucket or object has **FULL_CONTROL** permission for the bucket or object. Other OBS users have **READ** permission.                                        |
   +---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | bucket-owner-read         | Indicates that the owner of an object has **FULL_CONTROL** permission for the object and the owner of the bucket where the object resides has **READ** permission.                        |
   +---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | bucket-owner-full-control | Indicates that the owner of an object has **FULL_CONTROL** permission for the object and the owner of the bucket where the object resides has **FULL_CONTROL** permission for the object. |
   +---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | log-delivery-write        | Indicates that a log delivery group has **WRITE** and **READ_ACP** permission for buckets.                                                                                                |
   +---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. note::

   By default, the access control policy is **private**.
