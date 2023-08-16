:original_name: obs_faq_0064.html

.. _obs_faq_0064:

Why Can't I Delete a Bucket?
============================

-  Check whether the network connectivity between the local computer and OBS is normal. If the network is down, restore the network connectivity.
-  Check whether all objects in the bucket have been deleted. If not, delete all objects from the bucket.
-  Check whether all fragments in the bucket have been deleted. If not, delete all fragments from the bucket.
-  If versioning is enabled, check whether there are deleted objects remaining in the bucket. If yes, permanently delete all deleted objects from the bucket.
-  Check whether the account that deletes the bucket is the owner of the bucket.
-  If the fault persists, contact the administrator.
