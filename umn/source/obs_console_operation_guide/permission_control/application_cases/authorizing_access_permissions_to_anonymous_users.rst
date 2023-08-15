:original_name: obs_03_0132.html

.. _obs_03_0132:

Authorizing Access Permissions to Anonymous Users
=================================================

An enterprise stores a large volume of map data in OBS, and offers the data for public query. This enterprise sets a read permission for anonymous users, and provides the data URLs on the Internet. Then all users can read or download the data through the URLs.

Procedure
---------

#. Log in to OBS Console and click **Create Bucket** to create a bucket.
#. In the bucket list, click the name of the newly created bucket. On the page that is displayed, click **Objects** in the pane on the left, and upload the map data as an object to the new bucket.
#. Click the object to be operated and click **Object ACL**.
#. In **Object ACL** > **Public Permissions** > **Anonymous User**, click **Edit** to set **Access to Object** to **Read**.
#. Click **Save** to save the permission setting.

Verification
------------

#. Click the object. Its URL is displayed under **Link**. Share the URL over the Internet, so that all users can access or download the object through the Internet.
#. An anonymous user can view the object by copying the URL of the object to the web browser.
