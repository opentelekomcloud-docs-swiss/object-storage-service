:original_name: obs_faq_0042.html

.. _obs_faq_0042:

How Can I Control Access to OBS?
================================

You can use the following mechanisms to control access to OBS.

-  IAM policies

   IAM policies define the actions that can be performed on your cloud resources, specifying what actions are allowed or denied.

   IAM policies can be used to grant access to various IAM users under the same parent account.

   The process is as follows:

   #. Create a user group and select an IAM permission set for it.
   #. Create an IAM user and add it to the user group, and it will inherit the permissions of the user group you added it to.

-  Bucket policies

   A bucket policy applies to the configured OBS bucket and all the objects in the bucket. An OBS bucket owner can use a bucket policy to grant permissions on buckets and objects in the buckets to IAM users or other accounts.

-  Access Control List (ACL)

   ACLs control read and write permissions for accounts. ACL control is not as fine-grained as bucket policies and IAM policies, so IAM policies and bucket policies are recommended instead.
