:original_name: obs_03_0083.html

.. _obs_03_0083:

Overview
========

The bucket inventory function periodically generate lists of metadata information of objects in a bucket. Inventories help you better understand object statuses in the bucket.

An inventory is a CSV file. Inventory files are automatically uploaded to the specified bucket.

You specify that inventories are generated for objects with the same object name prefix. You can also determine the inventory generation interval and whether to list all object versions in the inventory file. In addition, you can specify the object metadata to be included in the inventory, such as object size, modification time, and replication status.

Limitations and Constraints
---------------------------

-  A bucket can have a maximum of 10 inventory rules.
-  The source bucket (for which a bucket inventory rule is configured) and the target bucket (where the generated inventory files are stored) must belong to the same account.
-  The source bucket and the target bucket must be in the same region.
-  Inventory files must be in the CSV format.
-  OBS can generate inventory files for all objects in a bucket or a group of objects whose names begin with the same prefix.
-  If a bucket has multiple inventory rules, overlaps between the inventory rules are not allowed.

   -  If a bucket already has an inventory rule for the entire bucket, new inventory rules that filter objects by prefixes cannot be created. If you need an inventory rule that covers only a subset of objects in the bucket, delete the inventory rule configured for the entire bucket.
   -  If an inventory rule that filters objects by a specified prefix already exists, you cannot create an inventory rule for the entire bucket. To create an inventory rule for the entire bucket, make sure that the bucket has no other inventory rules that filter objects by specified prefixes.
   -  If a bucket already has an inventory rule that filters objects by the object name prefix **ab**, the filter of a new inventory rule cannot start with **a** or **ab**. Or, you can delete the existing inventory rule and create a new one that filters objects according to your needs.
