:original_name: obs_03_0122.html

.. _obs_03_0122:

Creating a User and Granting OBS Permissions
============================================

Process
-------


.. figure:: /_static/images/en-us_image_0170301902.png
   :alt: **Figure 1** Granting an IAM user the access permissions to OBS

   **Figure 1** Granting an IAM user the access permissions to OBS

Procedure
---------

#. Log in to the management console using a cloud service account.

#. On the top navigation menu, choose **Service List** > **Management & Deployment** > **Identity and Access Management**. The IAM console page is displayed.

#. Create a user group and grant the OBS permissions to the user group.

   User groups facilitate centralized user management and streamlined permissions management. Users in the same user group have the same permissions. Users created in IAM inherit permissions from the groups to which they belong.

   a. In the navigation pane on the left, click **User Groups**. The **User Groups** page is displayed.

   b. Click **Create User Group**.

   c. On the **Create User Group** page, enter a name for the user group and click **OK**.

      The user group is displayed in the user group list once the creation completes.

   d. Click **Modify** in the **Operation** column of the row where the created user group resides.

   e. In the **Group Permissions** area, locate the row that displays **Global service** > **OBS**, click **Attach Policy** in the **Operation** column, select the policy name, and click **OK**.

      .. note::

         In the **Policy Information** area, you can view the details about the policy.

         Due to data caching, an RBAC policy and fine-grained policy involving OBS actions will take effect 10 to 15 minutes after it is attached to a user and user group.

#. Create a user.

   a. In the navigation pane on the left, click **Users**. The **Users** page is displayed.
   b. Click **Create User**.
   c. Set user information and click **Next**.

      .. table:: **Table 1** User parameters

         +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Parameter                         | Description                                                                                                                                                                                                                                                |
         +===================================+============================================================================================================================================================================================================================================================+
         | Username                          | The user name for logging in to the cloud service.                                                                                                                                                                                                         |
         +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Credential Type                   | A credential refers to the identity credential used for user system authentication. In this example, password is selected.                                                                                                                                 |
         |                                   |                                                                                                                                                                                                                                                            |
         |                                   | -  **Password**: Used for accessing cloud services using the console or development tools.                                                                                                                                                                 |
         |                                   | -  **Access key**: Used for logging to the cloud service using development tools. This credential type is more secure, and is recommended if the user does not need to use the console.                                                                    |
         +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | User Groups                       | You can add a user to one or more user groups. Then the user will inherit the permissions granted to these user groups. The default user group **admin** has the administrator permissions and all of the permissions required to use all cloud resources. |
         +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Description                       | (Optional) Brief description about the user.                                                                                                                                                                                                               |
         +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   d. Select a type for password generation, set the email address and mobile number, and click **OK**.

#. Use the created IAM user to log in to OBS Console and verify the user permissions.
