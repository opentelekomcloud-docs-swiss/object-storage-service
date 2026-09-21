:original_name: obs_03_1058.html

.. _obs_03_1058:

Adding an External Bucket
=========================

Add buckets of other users through OBS Browser+.

Prerequisites
-------------

You have been granted the ACL permissions to access buckets of other users.

For example, account A needs to add bucket **bucket_share** of account B to itself for it to read objects stored in bucket **bucket_share**. To do this, account B must obtain the **Account ID** of account A and grant account A the read permission on bucket **bucket_share** through OBS Console.

Account A can obtain its account ID (same as the owner ID) from the **Basic Information** page of the bucket.

If account B has granted anonymous users the read permission for bucket **bucket_share**, all OBS-registered users can add bucket **bucket_share**. For details about how to grant permissions to anonymous users, see :ref:`Configuring a Bucket ACL <obs_03_1049>`.

Procedure
---------

#. Log in to OBS Browser+.

#. In the navigation pane, choose **External Bucket**, as shown in :ref:`Figure 1 <obs_03_1058__fig11715141135020>`.

   .. _obs_03_1058__fig11715141135020:

   .. figure:: /_static/images/en-us_image_0000002683558514.png
      :alt: **Figure 1** External buckets

      **Figure 1** External buckets

#. Click **Add**. In the **Add External Bucket** dialog box, enter the external bucket name and click **OK**, as shown in :ref:`Figure 2 <obs_03_1058__fig174389178182>`.

   .. _obs_03_1058__fig174389178182:

   .. figure:: /_static/images/en-us_image_0000002713118367.png
      :alt: **Figure 2** Adding an external bucket

      **Figure 2** Adding an external bucket

   An external bucket name must be globally unique and:

   -  Must be 3 to 63 characters long and start with a digit or letter. Only lowercase letters, digits, hyphens (-), and periods (.) are allowed.
   -  Cannot be formatted as an IP address.
   -  Cannot start or end with a hyphen (-) or period (.).
   -  Cannot contain two consecutive periods (..), for example, **my..bucket**.
   -  Cannot contain a period (.) and a hyphen (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.

   After external buckets are added, you can see them in the bucket list and have ACL access permissions for them.

Example
-------

If you grant anonymous users the read and write permissions on bucket **test**, anonymous users can log in to OBS Browser+ and add bucket **test** using their own accounts, so they can access the bucket locally. On the external bucket page of OBS Browser+, anonymous users can see bucket **test** in the list and have the write permission for the bucket. They can upload, overwrite, and delete any object in bucket **test**.
