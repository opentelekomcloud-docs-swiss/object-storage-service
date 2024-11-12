:original_name: obs_faq_0138.html

.. _obs_faq_0138:

Why Am I Unable to Create a Bucket?
===================================

-  If the number of created buckets has reached 100 (the maximum number allowed), delete some unneeded buckets and try again.
-  If the new bucket name already exists, use another one and try again. Each OBS bucket name must be globally unique. Specifically, it must be different from that of buckets created by its owner or by any other users.
-  The name of a deleted bucket cannot be reused immediately after the deletion. It can be reused for a bucket at least 30 minutes later after the deletion.
-  Check whether the account has required permissions. If not, grant the account permissions as needed.
-  Check whether the network connectivity between the local computer and OBS is normal. If the network is faulty, restore the network connection.
-  If the failure is not caused by any of the described reasons, you can check the returned error code to try to find the reason.
