:original_name: obs_03_0080.html

.. _obs_03_0080:

Granting an IAM User Permissions to Operate a Specific Bucket
=============================================================

Create an IAM user under in an account. The IAM user has no permission to any resource before it is added to any user group. The bucket owner (root account) or other accounts and IAM users, who have the permission to set bucket policies, can configure bucket policies to grant the bucket operation permissions to IAM users.

The following is an example about how to grant an IAM user the bucket access and object upload permissions.

Procedure
---------

#. In the bucket list, click the bucket you want to operate to go to the **Objects** page.
#. In the navigation pane, choose **Permissions** > **Bucket Policies**.
#. Click **Create**.
#. Configure parameters listed in the table below to grant an IAM user the permissions to access the bucket (to list objects in the bucket) and to upload objects.

   .. table:: **Table 1** Parameters for granting the object listing and upload permissions

      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                      |
      +===================================+==================================================================================================================================================================================================================+
      | Configuration method              | Choose **Visual Editor**.                                                                                                                                                                                        |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Policy Name                       | Enter a custom name.                                                                                                                                                                                             |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Effect                            | Allow                                                                                                                                                                                                            |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Principal                         | -  Current account                                                                                                                                                                                               |
      |                                   | -  Sub-user: Specify IAM users under the current account.                                                                                                                                                        |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Resources                         | Select **Entire bucket (including the objects in it)**.                                                                                                                                                          |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Actions                           | Select **Customize** and then the **ListBucket** and **PutObject** actions.                                                                                                                                      |
      |                                   |                                                                                                                                                                                                                  |
      |                                   | .. note::                                                                                                                                                                                                        |
      |                                   |                                                                                                                                                                                                                  |
      |                                   |    In this example, only the actions for listing and uploading objects are selected. You can also select other actions to grant corresponding permissions if needed. The asterisk (``*``) indicates all actions. |
      |                                   |                                                                                                                                                                                                                  |
      |                                   |    For details about the supported actions, see :ref:`Actions <obs_03_0051>`.                                                                                                                                    |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **Create** in the lower right corner.
