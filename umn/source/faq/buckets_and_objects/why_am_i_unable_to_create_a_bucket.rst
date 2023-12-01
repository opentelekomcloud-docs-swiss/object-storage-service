:original_name: obs_faq_0138.html

.. _obs_faq_0138:

Why Am I Unable to Create a Bucket?
===================================

-  If the number of buckets created by the current user reaches 100, delete some unneeded buckets first.
-  If the name for the new bucket already exists, use another name and try again. Each OBS bucket name must be globally unique. Specifically, it must be different from that of buckets created by its owner or by any other users.
-  The name of a deleted bucket cannot be reused immediately after the deletion. It can be reused for a bucket at least 30 minutes later after the deletion.
-  Check whether the account has required permissions. If the account does not have the permissions, grant them.
-  Check whether the network connectivity between the local computer and OBS is normal. If the network is down, restore the network connection.
-  If the failure is not caused by any of the preceding reasons, check the returned error code and find the reason.
