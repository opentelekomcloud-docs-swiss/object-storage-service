:original_name: obs_faq_0050.html

.. _obs_faq_0050:

Can I Upload Objects with the Same Name to the Same Folder?
===========================================================

When versioning is enabled for a bucket, OBS automatically assigns a unique version ID to each object uploaded to the bucket. Objects with the same name are stored in OBS with different version IDs.

If versioning is not enabled for a bucket, a newly uploaded object in the folder will overwrite the previously uploaded object with the same name.
