:original_name: obs_03_0304.html

.. _obs_03_0304:

Configuring User Permissions
============================

If your cloud service account does not need individual IAM users, then you may skip this section. Your permissions to use OBS functions are not affected.

OBS is separately deployed from other cloud resources. If IAM users are required, you need to grant them access permissions for OBS.

Process
-------


.. figure:: /_static/images/en-us_image_0170301902.png
   :alt: **Figure 1** Process of granting an IAM user the OBS permissions

   **Figure 1** Process of granting an IAM user the OBS permissions

Procedure
---------

#. Log in to the management console with your account.

#. On the top menu bar, choose **Service List** > **Management & Deployment** > **Identity and Access Management**. The IAM console is displayed.

#. Create a user group and assign OBS permissions to it.

   A user group is a collection of users. By assigning permissions to a user group, you assign permissions to the users in this group. After you create an IAM user, add it to one or more user groups, so that it can inherit the permissions from the groups.

   a. In the navigation pane, choose **User Groups**. The **User Groups** page is displayed.

   b. Click **Create User Group**.

   c. Enter a user group name and click **OK**.

      The user group is displayed in the user group list once the creation is complete.

   d. Locate the user group you created and click **Modify** in the **Operation** column of the row.

   e. In the **Group Permissions** area, locate the row that displays **Global service** > **OBS**, click **Attach Policy** in the **Operation** column, select the policy name, and click **OK**.

      .. note::

         In the **Policy Information** area, you can view the details about the policy.

         Due to data caching, an RBAC policy or a fine-grained policy involving OBS actions will take effect 10 to 15 minutes after it is attached to a user or a user group.

#. Create an IAM user. For details, see section "Creating an IAM User" in the *Identity and Access Management User Guide*.

#. Use the created IAM user to log in to OBS Console and verify the user permissions.
