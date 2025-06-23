:original_name: obs_03_0310.html

.. _obs_03_0310:

Deleting a Bucket
=================

You can delete unwanted buckets on OBS Console to free up the quota of buckets.

Prerequisites
-------------

-  All objects in the bucket have been permanently deleted. A bucket must be emptied before it can be deleted.

   .. important::

      Objects under the **Objects**, **Deleted Objects**, and **Fragments** tabs must be all deleted.

-  A bucket can only be deleted by the bucket owner.

Procedure
---------

#. In the bucket list on OBS Console, select the bucket you want to delete, and then click **Delete** on the right.

   .. note::

      The name of a deleted bucket can be reused for another bucket at least 30 minutes after the deletion.

   .. important::
   
      Bucket name reuse may cause unintended data exposure. If a bucket is deleted and later a new bucket is created with the same name, all previously stored links or references to the old bucket will automatically point to the new one. 
   
      We strongly advise users to treat all bucket names and references as persistent and sensitive. If you publish or share links, always assume they might be reused in unintended ways.
   
      **Important**: we cannot take responsibility for any data exposure, misrouting, or access issues resulting from name reuse or improper reference management.

#. Click **Yes** to confirm the deletion.
