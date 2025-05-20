:original_name: en-us_topic_0045853821.html

.. _en-us_topic_0045853821:

Configuring an Object ACL
=========================

Prerequisites
-------------

You are the object owner or you have the permission to write the object ACL.

An object owner is the account that uploads the object, but may not be the owner of the bucket that stores the object. For example, account **B** is granted the permission to access a bucket of account **A**, and account **B** uploads a file to the bucket. In that case, account **B**, instead of the bucket owner account **A**, is the owner of the object. By default, account A is not allowed to access this object and cannot read or modify the object ACL.

Procedure
---------

#. In the bucket list, click the bucket you want to operate to go to the **Objects** page.

#. Click a desired object.

#. On the **Object ACL** page, choose a permission from **Private** and **Public Read** to grant object ACL permission for anonymous users.

   .. note::

      -  After you change **Public Read** to **Private**, only the bucket owner or object owner has the access.
      -  After you change **Private** to **Public Read**, anyone can read the object content and metadata. No identity authentication is required.

#. Click **Edit** to grant the owner, anonymous user, or other accounts required permissions for the object.

   .. note::

      ACL permissions for encrypted objects cannot be granted to registered users or anonymous users.

#. Click **Export** to get the object ACL configuration. The file includes the user type, account, object access, and ACL access.

#. Click **Add** to apply specific ACL permissions to an account.

   Enter an account ID and specify ACL permissions for the account. You can obtain the account ID from the **My Credentials** page. The account ID corresponds to the one on the **My Credentials** page.

   Click **OK**.


   .. figure:: /_static/images/en-us_image_0000002136490136.png
      :alt: **Figure 1** Granting permissions

      **Figure 1** Granting permissions
