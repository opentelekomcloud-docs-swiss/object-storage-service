:original_name: obs_03_0080.html

.. _obs_03_0080:

Granting an IAM User Permissions to Operate a Specific Bucket
=============================================================

Create an IAM user under in an account. The IAM user has no permission to any resource before it is added to any user group. The bucket owner (root account) or other accounts and IAM users, who have the permission to set bucket policies, can configure bucket policies to grant the bucket operation permissions to IAM users.

The following is an example about how to grant an IAM user the bucket access and object upload permissions.

Procedure
---------

#. In the bucket list, click the bucket you want to operate to go to the **Objects** page.
#. In the navigation pane, choose **Permissions**.
#. Choose **Bucket Policies**.
#. Click **Create**.
#. Configure parameters listed in the table below to grant IAM users the permissions to access the bucket (to list objects in the bucket) and to upload objects. Retain the default values for the other parameters.

   .. table:: **Table 1** Parameters for granting the object listing and upload permissions

      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter             |                       | Description                                                                                                                                                                                      |
      +=======================+=======================+==================================================================================================================================================================================================+
      | Configuration method  |                       | Choose **Visual Editor**.                                                                                                                                                                        |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Policy Name           |                       | Enter a custom policy name.                                                                                                                                                                      |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Policy content        | Effect                | Select **Allow**.                                                                                                                                                                                |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                       | Principal             | -  Select **Other accounts**.                                                                                                                                                                    |
      |                       |                       | -  IAM users: Specify IAM users in the *Account ID*\ **/**\ *IAM user ID* format, with each IAM user on a separate line.                                                                         |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                       | Resources             | Select **Entire bucket (including the objects in it)**.                                                                                                                                          |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                       | Actions               | Select **Customize** and then the **ListBucket** and **PutObject** actions.                                                                                                                      |
      |                       |                       |                                                                                                                                                                                                  |
      |                       |                       | .. note::                                                                                                                                                                                        |
      |                       |                       |                                                                                                                                                                                                  |
      |                       |                       |    In this example, only the object upload action is selected. You can also select other object actions to grant corresponding permissions if needed. An asterisk (``*``) indicates all actions. |
      |                       |                       |                                                                                                                                                                                                  |
      |                       |                       |    For details about the supported actions, see :ref:`Actions <obs_03_0051>`.                                                                                                                    |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **Create**.
