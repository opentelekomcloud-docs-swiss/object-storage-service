:original_name: obs_03_0138.html

.. _obs_03_0138:

Why Did Some of My Data Stored on OBS Get Lost?
===============================================

-  Check whether there is a lifecycle rule configured to automatically delete objects after a certain date.
-  Check whether the write permission to the bucket has been granted to other users. If it was, those other users can delete objects from the bucket. If you have enabled logging, you can check the logs to find out who deleted the objects.
