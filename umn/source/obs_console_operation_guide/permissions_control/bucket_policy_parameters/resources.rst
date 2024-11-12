:original_name: obs_03_0118.html

.. _obs_03_0118:

Resources
=========

The resources a bucket policy is applied to can be the current entire bucket or objects in the bucket.

Resources can be specified in either of the following ways:

-  **Include**: The bucket policy applies to specified OBS resources.
-  **Exclude**: The bucket policy applies to OBS resources except the specified ones.

Applying a Bucket Policy to a Bucket
------------------------------------

To specify the current bucket as the resource, keep the resource text box empty. When configuring actions for the policy, select bucket related actions.

Applying a Bucket Policy to Specified Objects
---------------------------------------------

To apply the bucket policy to specified objects in a bucket, object-related actions must be configured in the policy. The configuration format is as follows:

-  For an object, enter the object name (including its folder name if any). If you want to specify the **example.jpg** file in the **imgs-folder** folder in the bucket, enter the following content in the resource text box:

   **imgs-folder/example.jpg**

-  For an object set, the wildcard asterisk (*) should be used. The asterisk \* indicates an empty string or any combination of multiple characters. The format rules are as follows:

   -  Use only one asterisk (*) to indicate all objects in a bucket.

   -  Use *Object name prefix*\ \* to indicate objects starting with this prefix in a bucket. For example,

      imgs\*

   -  Use \*\ *Object name suffix* to indicate objects ending with this suffix in a bucket. For example,

      \*.jpg

.. note::

   Use commas (,) to separate one object (or object set) from another.
