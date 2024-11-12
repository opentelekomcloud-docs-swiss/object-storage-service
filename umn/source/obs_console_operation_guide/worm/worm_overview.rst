:original_name: obs_03_0716.html

.. _obs_03_0716:

WORM Overview
=============

OBS provides write-once-read-many (WORM) to protect objects from being deleted or tampered with within a specified period. WORM works at both the bucket and object levels in compliance mode.

Scenarios
---------

In compliance mode, a WORM-protected object version cannot be overwritten or deleted by anyone, including the root user in your account.

When WORM is configured for a bucket, the protection applies to all objects in the bucket. When WORM is configured for an object version, the protection applies to the current object version only. No matter which type of WORM protection you want to use, you must enable WORM for the bucket first. A bucket-level WORM retention policy takes effect only for objects uploaded after the policy was configured. If an object is protected by a bucket-level WORM policy and an object-level WORM policy at the same time, the object-level WORM policy takes precedence.

Precautions
-----------

-  When you enable WORM for a bucket, OBS automatically enables versioning and versioning cannot be suspended later for that bucket. WORM protects objects based on the object version IDs. Only object versions with any WORM retention policy configured can be protected. Assume that object **test.txt 001** is protected by WORM. If another file with the same name is uploaded, a new object version **test.txt 002** with no WORM policy configured will be generated. In such case, **test.txt 002** is not protected and can be deleted. When you download an object without specifying a version ID, the current object version (**test.txt 002**) will be downloaded.
-  A lifecycle rule cannot delete WORM-protected objects, but can transition their storage class. After an object is no longer protected, it will be deleted when meeting the expiration rule in a lifecycle configuration.
-  If you do not enable WORM when creating a bucket, you cannot enable or configure it for that bucket later. If you cannot configure WORM for a bucket, it may be because you did not enable WORM when you created the bucket or your bucket was created before this feature was released. In such case, to use WORM, you need to create a new bucket and enable WORM for it.
-  Once you enable WORM for a bucket, you cannot disable it or suspend versioning for the bucket, but you can disable the default WORM policy for the bucket.
-  If you have deregistered your account, the WORM-protected objects will be permanently deleted.
-  WORM-based protection is not available for migration.
-  The metadata of a WORM-protected object can still be modified.
