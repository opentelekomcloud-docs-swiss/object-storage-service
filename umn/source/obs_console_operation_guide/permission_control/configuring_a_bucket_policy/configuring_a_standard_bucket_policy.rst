:original_name: obs_03_0142.html

.. _obs_03_0142:

Configuring a Standard Bucket Policy
====================================

For standard bucket policy, OBS offers three options, namely the Private, Public Read, and Public Read and Write policies. These policies are pre-defined and can be applied with a few clicks.

Procedure
---------

#. In the bucket list, click the bucket to be operated. The **Overview** page of the bucket is displayed.
#. In the navigation pane on the left, click **Permissions** to go to the permission management page.
#. On the **Bucket Policies** tab page, select a policy from the **Standard Bucket Policies** area.

   -  **Private**: No access beyond the bucket ACL settings is granted.
   -  **Public Read**: Any user can read objects in the bucket.
   -  **Public Read and Write**: Any user can read, write, and delete objects in the bucket.

   .. note::

      For your data security, the **Public Read** and **Public Read and Write** policies are not recommended.

#. In the dialog box that is displayed, click **Yes**.
