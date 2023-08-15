:original_name: obs_03_0096.html

.. _obs_03_0096:

Authorizing Folder Access Permissions to Anonymous Users
========================================================

If all objects in a folder need to be accessible to anonymous users, you can configure a bucket policy or an object policy to grant anonymous users the permission to access the folder. In this example, a bucket policy is used. If you want to use an object policy to authorize the permission, select the target folder and configure the object policy directly. Parameters are the same as those in the bucket policy.

Procedure
---------

#. In the bucket list, click the bucket to be operated. The **Overview** page of the bucket is displayed.
#. In the navigation pane on the left, click **Permissions** to go to the permission management page.
#. Choose **Bucket Policies** > **Custom Bucket Policies**.
#. Click **Create Bucket Policy**. The **Create Bucket Policy** dialog box is displayed.
#. Configure parameters according to the following table, so that you can grant anonymous users the permission to access the folder and objects in it:

   .. table:: **Table 1** Parameters for authorizing the permission to access a specified bucket

      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Value                                                                                                                                 |
      +===================================+=======================================================================================================================================+
      | Policy Mode                       | **Customized**                                                                                                                        |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------+
      | Effect                            | **Allow**                                                                                                                             |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------+
      | Principal                         | -  **Include**                                                                                                                        |
      |                                   | -  Select **Other account**, and enter an asterisk (*) as the account ID, indicating all anonymous users.                             |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------+
      | Resources                         | -  **Include**                                                                                                                        |
      |                                   | -  Set this parameter to all objects in the selected folder. If the folder name is **folder-001**, enter the value **folder-001/\***. |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------+
      | Actions                           | -  **Include**                                                                                                                        |
      |                                   | -  GetObject                                                                                                                          |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------+

#. Click **OK**.

Verification
------------

#. After the permission is successfully configured, select an object in the folder and click the object name to view its details. The object link (URL) is displayed on the details page. Share the URL over the Internet, so that all users can access or download the object through the Internet.
#. An anonymous user can view the object by copying the URL of the object to the web browser.
