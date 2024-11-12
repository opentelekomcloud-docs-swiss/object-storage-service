:original_name: obs_03_0207.html

.. _obs_03_0207:

Buckets
=======

Buckets are containers for storing objects. OBS provides flat storage in the form of buckets and objects. Unlike the conventional multi-layer directory structure of file systems, all objects in a bucket are stored at the same logical layer.

Each bucket has its own attributes, such as access permissions, and the region. You can specify access permissions, and regions when creating buckets. You can also configure advanced attributes to meet storage requirements in different scenarios.

Each bucket name in OBS is globally unique and cannot be changed after the bucket is created. The region where a bucket resides cannot be changed once the bucket is created. When you create a bucket, OBS creates a default access control list (ACL) that grants users permissions (such as read and write permissions) on the bucket. Only authorized users can perform operations such as creating, deleting, viewing, and configuring buckets.

An account (including all IAM users under this account) can create a maximum of 100 buckets. However, there is no restriction on the number and total size of objects in a bucket.

OBS adopts the REST architectural style, and is based on HTTP and HTTPS. You can use URLs to locate resources.

:ref:`Figure 1 <obs_03_0207__fig5658599310445>` illustrates the relationship between buckets and objects in OBS.

.. _obs_03_0207__fig5658599310445:

.. figure:: /_static/images/en-us_image_0129289279.png
   :alt: **Figure 1** Relationship between objects and buckets

   **Figure 1** Relationship between objects and buckets
