:original_name: obs_03_0096.html

.. _obs_03_0096:

Granting Anonymous Users Permission to Access Folders
=====================================================

If all objects in a folder need to be accessible to anonymous users, you can configure a bucket policy or an object policy to grant anonymous users the permission to access the folder. In this example, a bucket policy is used. If you want to use an object policy to grant permission, select the target folder and configure an object policy. Parameters in both types of policies are the same.

Procedure
---------

#. In the bucket list, click the bucket you want to operate to go to the **Objects** page.
#. In the navigation pane, choose **Permissions** > **Bucket Policies**.
#. Click **Create**.
#. Configure the following parameters in the **Create Bucket Policy** dialog box.

   .. table:: **Table 1** Authorizing folder access permissions to anonymous users

      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                            |
      +===================================+========================================================================================================================+
      | Configuration method              | Choose **Visual Editor**.                                                                                              |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------+
      | Policy Name                       | Enter a custom name.                                                                                                   |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------+
      | Effect                            | Allow                                                                                                                  |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------+
      | Principal                         | Select **All accounts**.                                                                                               |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------+
      | Resources                         | -  Resource scope: Select **Specified objects**.                                                                       |
      |                                   | -  Resource path: If the folder name is **folder-001**, enter **folder-001/\***, indicating all objects in the folder. |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------+
      | Actions                           | Select **Customize** and select the **GetObject** action.                                                              |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------+

#. Click **Create** in the lower right corner.

Verification
------------

#. After the permission is successfully configured, select an object in the folder and click the object name to view its details. The object link (URL) is displayed on the details page. Share the URL over the Internet, so that all users can access or download the object through the Internet.
#. Use the URL to access the object in a browser. An anonymous user can access the object.
