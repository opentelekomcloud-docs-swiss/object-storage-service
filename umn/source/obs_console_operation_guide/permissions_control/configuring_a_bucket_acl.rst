:original_name: obs_03_0326.html

.. _obs_03_0326:

Configuring a Bucket ACL
========================

Prerequisites
-------------

You are the bucket owner or you have the permission to write the bucket ACL.

Procedure
---------

#. In the bucket list, click the bucket you want to operate to go to the **Objects** page.

#. In the navigation pane, choose **Permissions** > **Bucket ACLs**.

#. On the **Bucket ACLs** page, choose **Private**, **Public Read**, or **Public Read/Write** to grant the bucket ACL permission for anonymous users.

   .. note::

      -  After you change **Public Read** or **Public Read/Write** to **Private**, only the bucket owner or object owner has the access.
      -  After you change **Private** to **Public Read**, anyone can read objects in the bucket. No identity authentication is required.
      -  After you change **Private** to **Public Read/Write**, anyone can read, write, and delete objects in the bucket. No identity authentication is required.

#. In the **Operation** column, click **Edit** to grant the owner, anonymous user, or log delivery user required ACL permissions for the bucket.

#. In the middle of the page, click **Export** to get the bucket ACL configuration. The file includes the user type, account, bucket access, and ACL access.

#. In the middle of the page, click **Add** to apply specific ACL permissions to an account.

   Enter an account ID and specify ACL permissions for the account. You can obtain the account ID from the **My Credentials** page.

   Click **OK**.
