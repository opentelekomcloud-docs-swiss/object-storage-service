:original_name: obs_03_0096.html

.. _obs_03_0096:

Granting Anonymous Users Permission to Access Folders
=====================================================

If all objects in a folder need to be accessible to anonymous users, you can configure a bucket policy or an object policy to grant anonymous users the permission to access the folder. In this example, a bucket policy is used. If you want to use an object policy to grant permission, select the target folder and configure an object policy. Parameters in both types of policies are the same.

Procedure
---------

#. In the bucket list, click the bucket you want to operate to go to the **Objects** page.
#. In the navigation pane, choose **Permissions**.
#. Choose **Bucket Policies**.
#. Click **Create**.
#. Configure parameters according to the following table, so that you can grant anonymous users the permission to access the folder and objects in it. Retain the default values for the other parameters.

   .. table:: **Table 1** Parameters for granting the object listing and upload permissions

      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                |
      +===================================+============================================================================================================================================+
      | Configuration method              | Choose **Visual Editor**.                                                                                                                  |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+
      | Policy Name                       | Enter a policy name.                                                                                                                       |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+
      | Effect                            | Allow                                                                                                                                      |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+
      | Principal                         | -  Select **Other accounts**.                                                                                                              |
      |                                   | -  IAM users: Specify IAM users in the *Account ID*\ **/**\ *IAM user ID* format, with each IAM user on a separate line.                   |
      |                                   |                                                                                                                                            |
      |                                   |    -  *Account ID*\ **/\*** indicates that permissions are granted to all IAM users under the account.                                     |
      |                                   |    -  **\*/\*** indicates that permissions are granted to all anonymous users.                                                             |
      |                                   |                                                                                                                                            |
      |                                   | .. note::                                                                                                                                  |
      |                                   |                                                                                                                                            |
      |                                   |    You can obtain the account ID and IAM user ID from the **My Credentials** page.                                                         |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+
      | Resources                         | Select **Specified objects**. Then, set an object name prefix (for example, **folder-001/\***) to allow access to all objects in a folder. |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+
      | Actions                           | Select **Customize** and then the **GetObject** action.                                                                                    |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **Create**.

Verification
------------

#. After the permission is successfully configured, select an object in the folder and click the object name to view its details. The object link (URL) is displayed on the details page. Share the URL over the Internet, so that all users can access or download the object through the Internet.
#. Use the URL to access the object in a browser. An anonymous user can access the object.
