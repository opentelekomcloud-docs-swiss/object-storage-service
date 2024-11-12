:original_name: obs_03_0081.html

.. _obs_03_0081:

Granting Other Accounts Permissions to Operate a Specific Bucket
================================================================

The bucket owner (root account) or other accounts and IAM users, who have the permission to set bucket policies, can configure bucket policies to grant the bucket operation permissions to other accounts or IAM users under other accounts.

The following is an example about how to grant other accounts bucket access and object upload permissions.

.. note::

   To grant permissions to IAM users under other accounts, you need to configure both bucket policies and IAM policies.

   #. Configure a bucket policy to allow IAM users to access the bucket.
   #. Configure IAM policies for the account where authorized IAM users belong, to allow the IAM users to access the bucket.

   Only permissions that are allowed by both the bucket policy and IAM policies can take effect.

Procedure
---------

#. In the bucket list, click the bucket you want to operate to go to the **Objects** page.
#. In the navigation pane, choose **Permissions**.
#. Choose **Bucket Policies**.
#. Click **Create**.
#. Configure the parameters listed in the table below to grant other accounts the bucket access permission. Retain the default values for the other parameters.

   .. table:: **Table 1** Parameters for granting the object listing and upload permissions

      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------+
      | Parameter             |                       | Description                                                                                                              |
      +=======================+=======================+==========================================================================================================================+
      | Configuration method  |                       | Choose **Visual Editor**.                                                                                                |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------+
      | Policy Name           |                       | Enter a custom policy name.                                                                                              |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------+
      | Policy content        | Effect                | Select **Allow**.                                                                                                        |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------+
      |                       | Principal             | -  Select **Other accounts**.                                                                                            |
      |                       |                       | -  IAM users: Specify IAM users in the *Account ID*\ **/**\ *IAM user ID* format, with each IAM user on a separate line. |
      |                       |                       |                                                                                                                          |
      |                       |                       |    -  *Account ID*\ **/\*** indicates that permissions are granted to all IAM users under the account.                   |
      |                       |                       |    -  **\*/\*** indicates that permissions are granted to all anonymous users.                                           |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------+
      |                       | Resources             | Select **Entire bucket (including the objects in it)**.                                                                  |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------+
      |                       | Actions               | Select **Customize** and then the **ListBucket** and **PutObject** actions.                                              |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------+

#. Click **Create**.
