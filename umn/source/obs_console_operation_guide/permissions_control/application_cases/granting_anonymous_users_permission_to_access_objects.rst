:original_name: obs_03_0132.html

.. _obs_03_0132:

Granting Anonymous Users Permission to Access Objects
=====================================================

An enterprise stores a large volume of file data in OBS, and offers the data for public query. This enterprise sets a read permission for anonymous users, and provides the data URLs on the Internet. Then all users can read or download the data through the URLs.

Procedure
---------

#. Log in to OBS Console and click **Create Bucket** to create a bucket.
#. In the bucket list, click the name of the newly created bucket. On the displayed object management page, upload the file data to the new bucket. The file data is stored as an object.
#. Click the object name. The object details page is displayed.
#. Under **Object ACL** > **User Access** > **Anonymous User**, click **Edit** and set **Access to Object** to **Read** to grant the object read permission for anonymous users.
#. Click **Save** to save the permission setting.

Verification
------------

#. Click the object. Its URL is displayed under **Link**. Share the URL over the Internet, so that all users can access or download the object through the Internet.
#. An anonymous user can view the object by copying the URL of the object to the web browser.
