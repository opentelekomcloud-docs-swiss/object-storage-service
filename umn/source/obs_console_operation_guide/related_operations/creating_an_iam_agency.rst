:original_name: obs_03_0037.html

.. _obs_03_0037:

Creating an IAM Agency
======================

To use some OBS features, you need to use IAM agencies to grant required permissions to OBS for processing your data.

Creating an Agency for Uploading Logs
-------------------------------------

#. In the **Logging** dialog box, click **Create Agency** to jump to the **Agencies** page on the **Identity and Access Management** console.
#. Click **Create**.
#. Enter an agency name.
#. Select **Cloud service** for the **Agency Type**.
#. Select **Object Storage Service (OBS)** as the cloud service.
#. Set a validity period.
#. In the **Permissions** area, find **Global service** > **OBS** and click **Attach Policy** on the right.

   a. Search for and select the custom policy that has the permission to upload logs to the bucket, and click **OK**.

      If you have not created any custom policy, click **Policies** in the navigation pane on the left to create one.

      When creating a custom policy, select **Global services** for **Scope** and select **JSON** for **Policy View**. The policy content is as follows:

      .. note::

         When coding the policy content in an actual scenario, replace **mybucketlogs** with the actual bucket name:

      .. code-block::

         {
             "Version": "1.1",
             "Statement": [
                 {
                     "Action": [
                         "obs:object:PutObject"
                     ],
                     "Resource": [
                         "OBS:*:*:object:mybucketlogs/*"
                     ],
                     "Effect": "Allow"
                 }
             ]
         }

#. Click **OK** to complete the agency creation.
