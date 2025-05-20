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
#. In the navigation pane, choose **Permissions** > **Bucket Policies**.
#. Click **Create**.
#. Configure parameters listed in the table below to grant other accounts the permissions to access the bucket (to list objects in the bucket) and to upload objects.

   .. table:: **Table 1** Parameters for granting the object listing and upload permissions

      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                                  |
      +===================================+==============================================================================================================================================================================================================================================+
      | Configuration method              | Choose **Visual Editor**.                                                                                                                                                                                                                    |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Policy Name                       | Enter a custom name.                                                                                                                                                                                                                         |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Effect                            | Select **Allow**.                                                                                                                                                                                                                            |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Principal                         | -  Select **Other accounts**.                                                                                                                                                                                                                |
      |                                   | -  If **Other accounts** is selected, enter the account ID and IAM user ID in the format of *Account ID/IAM User ID*. To specify multiple IAM users, enter each one on a separate line. An asterisk (*) indicates all accounts or IAM users. |
      |                                   |                                                                                                                                                                                                                                              |
      |                                   |    .. note::                                                                                                                                                                                                                                 |
      |                                   |                                                                                                                                                                                                                                              |
      |                                   |       The account ID and IAM user ID can be obtained on the **My Credentials** page of the account or user to be authorized. The following describes different authorization scenarios:                                                      |
      |                                   |                                                                                                                                                                                                                                              |
      |                                   |       -  **Granting permissions to all accounts and IAM users**: Enter **\*/\***.                                                                                                                                                            |
      |                                   |       -  **Granting permissions to an account and all IAM users under the account**: Enter *Account ID*\ **/\***.                                                                                                                            |
      |                                   |       -  **Granting permissions to a specific IAM user under an account**: Enter *Account ID/IAM user ID*.                                                                                                                                   |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Resources                         | Select **Entire bucket (including the objects in it)**.                                                                                                                                                                                      |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Actions                           | Select **Customize** and then the **ListBucket** and **PutObject** actions.                                                                                                                                                                  |
      |                                   |                                                                                                                                                                                                                                              |
      |                                   | .. note::                                                                                                                                                                                                                                    |
      |                                   |                                                                                                                                                                                                                                              |
      |                                   |    In this example, only the actions for listing and uploading objects are selected. You can also select other actions to grant corresponding permissions if needed. The asterisk (``*``) indicates all actions.                             |
      |                                   |                                                                                                                                                                                                                                              |
      |                                   |    For details about the supported actions, see :ref:`Actions <obs_03_0051>`.                                                                                                                                                                |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **Create** in the lower right corner.
