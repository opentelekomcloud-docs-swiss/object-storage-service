:original_name: en-us_topic_0045853514.html

.. _en-us_topic_0045853514:

Managing Fragments
==================

Background Information
----------------------

Data can be uploaded to OBS using multipart uploads. There will be fragments generated, if a multipart upload fails because of the following causes (included but not limited to):

-  The network is in poor conditions, and the connection to the OBS server is interrupted frequently.
-  The upload task is manually suspended.
-  The device is faulty.
-  The device is powered off suddenly.

On OBS Console, storage used by fragments is charged. Clear fragments when they are not needed. If a file upload task fails, upload the file again.

.. important::

   Generated fragments take up storage space that is billable.

Procedure
---------

#. In the bucket list, click the bucket you want to operate to go to the **Objects** page.

#. Click **Fragments**, select the fragment that you want to delete, and click **Delete** on the right.

   You can also select multiple fragments and click **Delete** above the fragment list to batch delete them.

#. Click **Yes** to confirm the deletion.
