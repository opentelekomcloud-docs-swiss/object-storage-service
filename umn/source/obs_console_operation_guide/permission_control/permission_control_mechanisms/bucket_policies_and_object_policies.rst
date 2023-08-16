:original_name: en-us_topic_0045853745.html

.. _en-us_topic_0045853745:

Bucket Policies and Object Policies
===================================

Bucket Owner and Object Owner
-----------------------------

The owner of a bucket is the account that created the bucket. If the bucket is created by an IAM user under the account, the bucket owner is the account instead of the IAM user.

The owner of an object is the account that uploads the object, who may not be the owner of the bucket to which the object belongs. For example, account **B** is granted the permission to access a bucket of account **A**, and account **B** uploads a file to the bucket. In that case, instead of the bucket owner account **A**, account **B** is the owner of the object.

Bucket Policy
-------------

A bucket policy is attached to a bucket and objects in the bucket. By leveraging bucket policies, the owner of a bucket can authorize IAM users or other accounts the permissions to operate the bucket and objects in the bucket.

**Bucket Policy Application Scenarios**:

-  If no IAM policies are used for access permission control and you want to authorize other accounts the permission to access your OBS resources, you can use bucket policies to authorize such permissions.
-  You can configure different bucket policies to grant IAM users different access permissions to different buckets.
-  You can also use bucket policies to grant other accounts the permissions to access your buckets.

**Standard Bucket Policies**:

There are three options for standard bucket policies.

-  **Private**: No access beyond the bucket ACL settings is granted.
-  **Public Read**: Any user can read objects in the bucket.
-  **Public Read and Write**: Any user can read, write, and delete objects in the bucket.

After a bucket is created, the default bucket policy is **Private**. Only the bucket owner has the full control permissions over the bucket. To ensure data security, it is recommended that you do not use the **Public Read** or **Public Read and Write** policies.

.. table:: **Table 1** Standard bucket policies

   +-----------------+-----------------+------------------------------+------------------------------+
   | Parameter       | Private         | Public Read                  | Public Read and Write        |
   +=================+=================+==============================+==============================+
   | Effect          | N/A             | Allow                        | Allow                        |
   +-----------------+-----------------+------------------------------+------------------------------+
   | Principal       | N/A             | \* (Any user)                | \* (Any user)                |
   +-----------------+-----------------+------------------------------+------------------------------+
   | Resources       | N/A             | \* (All objects in a bucket) | \* (All objects in a bucket) |
   +-----------------+-----------------+------------------------------+------------------------------+
   | Actions         | N/A             | -  GetObject                 | -  GetObject                 |
   |                 |                 | -  GetObjectVersion          | -  GetObjectVersion          |
   |                 |                 | -  ListBucket                | -  PutObject                 |
   |                 |                 |                              | -  DeleteObject              |
   |                 |                 |                              | -  DeleteObjectVersion       |
   |                 |                 |                              | -  ListBucket                |
   +-----------------+-----------------+------------------------------+------------------------------+
   | Conditions      | N/A             | N/A                          | N/A                          |
   +-----------------+-----------------+------------------------------+------------------------------+

.. note::

   For buckets whose version is 3.0, the default permissions of **Public Read** and **Public Read and Write** are updated to solve the problem where external buckets fail to be added to OBS Browser due to insufficient permissions.

   -  Added the ListBucket permission to the **Public Read** policy.
   -  Added the ListBucket permission to the **Public Read and Write** policy.
   -  If you want to add an external bucket to OBS Browser, manually update the configuration of standard bucket policies.

**Custom Bucket Policy**:

The following three modes are provided to facilitate quick configuration:

-  **Read-only**: With the **Read-only** mode, you only need to specify the **Principal** (authorized users). Then the authorized users have the read permission for the bucket and objects in the bucket, and can perform all GET operations on these resources.
-  **Read and write**: With the **Read and write** mode, you only need to specify the **Principal** (authorized users). Then the authorized users have the full control permissions for the bucket and objects in the bucket, and can perform any operation on these resources.
-  **Customized**: With the **Customized** mode, you can define the specific operation permissions that you want to authorize to users and accounts by configuring the parameters of **Effect**, **Principal**, **Resources**, **Actions**, and **Conditions**.

.. note::

   On OBS Console, when you use the custom bucket policy to authorize other users with resource operation permissions, you also need to authorize the users with the bucket read permission **ListBucket** (leave the resource name blank to indicate that the policy takes effect on the entire bucket). Otherwise, the users have no permission to access the bucket.

Object Policy
-------------

An object policy is a policy that applies to objects in a bucket. A bucket policy is applicable to a set of objects (with the same object name prefix) or to all objects (specified by an asterisk **\***) in the bucket. To configure an object policy, select an object, and then configure the object policy directly for the object.
