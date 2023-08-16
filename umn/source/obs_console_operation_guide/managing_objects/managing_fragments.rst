:original_name: en-us_topic_0045853514.html

.. _en-us_topic_0045853514:

Managing Fragments
==================

Background Information
----------------------

Fragments are generated when multipart upload tasks fail. Such failures generally occur in the following scenarios:

-  The network is in poor conditions, and the connection to the OBS server is interrupted frequently.
-  The upload task is manually suspended.
-  The device is faulty.
-  The device is powered off suddenly.

On OBS Console, storage used by fragments is charged. Clear fragments when they are not needed. If a file upload task fails, upload the file again.

.. important::

   Fragments on OBS consume storage spaces that are charged according to price rates of storage space.

Procedure
---------

#. In the bucket list, click the bucket to be operated. The **Overview** page of the bucket is displayed.

#. In the navigation pane, click **Objects**.

#. Click **Fragments**, select the fragment that you want to delete, and then click **Delete** on the right of the fragment.

   You can also select multiple fragments and click **Delete** on the top of fragment list to batch delete them.

#. Click **Yes** to confirm the deletion.
