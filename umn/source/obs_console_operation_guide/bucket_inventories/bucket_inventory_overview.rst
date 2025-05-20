:original_name: obs_03_0083.html

.. _obs_03_0083:

Bucket Inventory Overview
=========================

The bucket inventory function periodically generates lists of metadata information of objects in a bucket. Inventories help you better understand object statuses in the bucket.

An inventory is a CSV file. Inventory files are automatically uploaded to the specified bucket.

You specify that inventories are generated for objects with the same object name prefix. You can also determine the inventory generation interval and whether to list all object versions in the inventory file. The object metadata you specify in the inventory include the file size, last modification time, storage class, ETag, multipart upload, encryption status, and replication status.

Constraints
-----------

-  A bucket can have a maximum of 10 inventory rules.
-  The source bucket (for which the inventory is configured) and the destination bucket (that stores the generated inventory files) must belong to the same account.
-  The source and destination buckets must be in the same region.
-  Inventory files must be in the CSV format.
-  OBS can generate inventory files for all objects in a bucket or a group of objects whose names begin with the same prefix.
-  If a bucket has multiple inventory rules, overlaps between the inventory rules are not allowed.

   -  If a bucket already has an inventory rule for the entire bucket, new inventory rules that filter objects by prefixes cannot be created. If you need an inventory rule that covers only a subset of objects in the bucket, delete the inventory rule configured for the entire bucket.
   -  If an inventory rule that filters objects by a specified prefix already exists, you cannot create an inventory rule for the entire bucket. To create an inventory rule for the entire bucket, make sure that the bucket has no other inventory rules that filter objects by specified prefixes.
   -  If a bucket already has an inventory rule that filters objects by the object name prefix **ab**, the filter of a new inventory rule cannot start with **a** or **abc**. To create such a rule, you need to first delete the existing inventory rule that conflicts with the rule you will create.

-  Bucket inventory files can be encrypted only in the SSE-KMS mode.
-  The destination bucket cannot have server-side encryption enabled.

Content in an Inventory File
----------------------------

:ref:`Table 1 <obs_03_0083__table2291537413>` lists all possible metadata fields that an inventory file can contain.

.. _obs_03_0083__table2291537413:

.. table:: **Table 1** Object metadata fields allowed in an inventory file

   +---------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Metadata            | Description                                                                                                                                                                                                                                                                                                             |
   +=====================+=========================================================================================================================================================================================================================================================================================================================+
   | Bucket              | Name of the source bucket                                                                                                                                                                                                                                                                                               |
   +---------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Key                 | Name of an object. Each object in a bucket has a unique key. Object names in the inventory file are URL-encoded using UTF-8 and must be decoded before you can use them.                                                                                                                                                |
   +---------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | VersionId           | Object version ID. This field is not included in the inventory file if **ObjectVersions** in the inventory configuration is set to **Current version only**.                                                                                                                                                            |
   +---------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | IsLatest            | This field is set to **True** if the object version is the latest. This field is not included in the inventory file if **ObjectVersions** in the inventory configuration is set to **Current version only**.                                                                                                            |
   +---------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | IsDeleteMarker      | When versioning is enabled for the source bucket, deleting an object will create a new piece of object metadata and set **IsDeleteMarker** of the metadata to **true**. This field is not included in the inventory file if **ObjectVersions** in the inventory configuration is set to **Current version only**.       |
   +---------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Size                | Object size, in bytes                                                                                                                                                                                                                                                                                                   |
   +---------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | LastModifiedDate    | Object creation date or the last modification date                                                                                                                                                                                                                                                                      |
   +---------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ETag                | Hexadecimal digest of the object MD5. ETag is the unique identifier of the object content. It reflects whether the object content is changed. For example, if the ETag value is **A** when an object is uploaded but changes to **B** when the object is downloaded, it means that the object content has been changed. |
   +---------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | StorageClass        | Storage class of an object                                                                                                                                                                                                                                                                                              |
   +---------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | IsMultipartUploaded | Whether an object is uploaded using multipart upload                                                                                                                                                                                                                                                                    |
   +---------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ReplicationStatus   | Cross-region replication status of an object                                                                                                                                                                                                                                                                            |
   +---------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | EncryptionStatus    | Encryption status of an object                                                                                                                                                                                                                                                                                          |
   +---------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_03_0083__section14172191411423:

Inventory File Name
-------------------

The name of an inventory file is in the following format:

.. code-block::

   destinationPrefix/sourceBucketName/inventoryId/yyyy-MM-dd'T'HH-mm'Z'/files/UUID_index.csv

-  *destinationPrefix* indicates the prefix specified in the inventory configuration, which can be used to group inventory files. If no prefix is specified, the default prefix is **BucketInventory**.
-  *sourceBucketName* indicates the source bucket for which the inventory is configured. This field can prevent conflicts when inventory files of different source buckets are saved to the same destination bucket.
-  *inventoryId* can prevent conflicts when multiple inventory files of the same source bucket are sent to the same destination bucket.
-  *yyyy-MM-dd'T'HH-mm'Z'* indicates the start time and date when the inventory generation begins scanning the bucket. Objects uploaded to the source bucket after this time may not be listed in the inventory file.
-  **UUID_index.csv** indicates one of the inventory files.

The manifest.json File
----------------------

If there are a large number of objects in a bucket, multiple inventory files may be generated for a single inventory configuration. It takes some time to generate these files. For example, if there are 200,000 objects in a bucket, it will take about 1.5 minutes to generate all inventory files. One or two hours after all inventory files are generated, a **manifest.json** file will be generated. The **manifest.json** file contains information about all inventory files generated this time, including:

-  **sourceBucket** that indicates the name of the source bucket
-  **destinationBucket** that indicates the name of the destination bucket
-  **version** that indicates the inventory version
-  **fileFormat** that indicates the inventory file format
-  **fileSchema** that indicates the object metadata fields contained in the inventory files
-  **files** that indicates the list of all inventory files
-  **key** that indicates the inventory file name
-  **size** that indicates the inventory file size, in bytes
-  **inventoriedRecord** that indicates the number of inventory records

The following is an example of a **manifest.json** file.

.. code-block::

   {
           "sourceBucket":"user001",
           "destinationBucket":"bucket001",
           "version":"2019-01-03",
           "fileFormat":"CSV",
           "fileSchema":"Bucket,Key,Size,LastModifiedDate,ETag,StorageClass,IsMultipartUploaded,ReplicationStatus,EncryptionStatus",
           "files":[
                   {
                           "key":"inventory%2Fuser001%2Ftest_id%2F2019-01-03T12-28Z%2Ffiles%2F0000016813AF58E66806C1E2D7F15155_1.csv",
                           "size":6705647390,
                           "inventoriedRecord":70585762,
                   }
           ]
   }

The name of the **manifest.json** file is as follows (for details about each field, see :ref:`Inventory File Name <obs_03_0083__section14172191411423>`):

.. code-block::

   destinationPrefix/sourceBucketName/inventoryId/yyyy-MM-dd'T'HH-mm'Z'/manifest.json

The symlink.txt File
--------------------

The **symlink.txt** file records the path of an inventory file. It helps quickly find all inventory files in big data scenarios. Apache Hive is compatible with the **symlink.txt** file. Hive can automatically find the **symlink.txt** file and the inventory files recorded in it.

The name of the **symlink.txt** file is as follows (for details about each field, see :ref:`Inventory File Name <obs_03_0083__section14172191411423>`):

.. code-block::

   destinationPrefix/sourceBucketName/inventoryId/hive/dt=YYYY-MM-DD-00-00/symlink.txt
