:original_name: obs_03_0037.html

.. _obs_03_0037:

Creating an Agency
==================

To use some OBS features, you need to use IAM agencies to grant required permissions to OBS for processing your data.

Creating an Agency for Uploading Logs
-------------------------------------

#. In the **Logging** dialog box, click **Create Agency** to jump to the **Agencies** page on the **Identity and Access Management** console.

#. Click **Create Agency**.

#. Enter an agency name.

#. Select **Cloud service** for the **Agency Type**.

#. Select **Object Storage Service (OBS)** as the cloud service.

#. Set a validity period.

#. Click **Next**.

#. On the **Select Policy/Role** page, select a custom policy that has the permission to upload data to the log storage bucket and click **Next**.

   If no custom policy is available, create one by referring to section "Creating a Custom Policy" in the *Identity and Access Management User Guide*.

   Select **JSON** for **Policy View**. The policy content is as follows.

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

#. On the **Select Scope** page, select **Global services** for **Scope** and click **OK**.

#. (Optional) If the log storage bucket has server-side encryption enabled, the agency also requires the **KMS Administrator** permission for the region where the bucket is located.

   a. Go to the **Agencies** page of the IAM console and click the name of the agency created in the previous step.
   b. Choose the **Permissions** tab and click **Authorize**.
   c. On the **Select Policy/Role** page, search for and select **KMS Administrator**. Then, click **Next**.
   d. On the **Select Scope** page, select **Region-specific projects** for **Scope**. Then, select the project in the region where the log storage bucket is located.
