:original_name: obs_03_0142.html

.. _obs_03_0142:

Configuring a Standard Bucket Policy
====================================

For standard bucket policy, OBS offers three options, namely the Private, Public Read, and Public Read and Write policies. These policies are pre-defined and can be applied with a few clicks.

Procedure
---------

#. In the bucket list, click the bucket you want to operate. The **Overview** page is displayed.
#. In the navigation pane, choose **Permissions**.
#. On the **Bucket Policies** tab page, select a policy from the **Standard Bucket Policies** area.

   -  **Private**: No access beyond the bucket ACL settings is granted.
   -  **Public Read**: Anyone can read objects in the bucket.
   -  **Public Read and Write**: Anyone can read, write, or delete objects in the bucket.

   .. note::

      For your data security, the **Public Read** and **Public Read and Write** policies are not recommended.

#. In the dialog box that is displayed, click **Yes**.
