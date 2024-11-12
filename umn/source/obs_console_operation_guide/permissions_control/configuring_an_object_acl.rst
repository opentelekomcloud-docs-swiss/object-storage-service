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

#. Click the object to be operated.

#. On the **Object ACL** tab page, click **Edit** to grant the owner and anonymous user ACL permissions for the object.

   .. note::

      ACL permissions for encrypted objects cannot be granted to registered users or anonymous users.

#. Click **Add** to apply specific ACL permissions to an account.

   Enter an account ID or account name and specify ACL permissions for the account. You can obtain the account ID or account name from the **My Credentials** page. The account ID and account name correspond to the **Domain ID** and **Domain Name** respectively on the **My Credentials** page.


   .. figure:: /_static/images/en-us_image_0000001180662112.png
      :alt: **Figure 1** Adding ACL permissions for an object

      **Figure 1** Adding ACL permissions for an object

#. Click **Save**.
