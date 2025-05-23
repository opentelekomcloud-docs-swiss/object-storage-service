:original_name: obs_04_0004.html

.. _obs_04_0004:

Basic Concepts
==============

Basic Concepts Related to OBS APIs
----------------------------------

-  Account

   Your cloud service account. The account has full access permissions for all of its cloud services and resources. The account can also reset user passwords and grant permissions to users.

-  User

   A user is created using a domain on Identity and Access Management (IAM) to use cloud services. Each IAM user has its own identity credentials (password and access keys).

   On the **My Credentials** page on the console, you can view the domain ID and user ID, and manage the access keys of the domain or IAM users.

   Access keys of the domain and its IAM users are required for authentication when calling APIs.

-  Bucket

   A bucket is a container where objects are stored. It is the top namespace in OBS. Each object must reside in a bucket. For example, if you store object **picture.jpg** in bucket **photo**, the object can be accessed by using this URL: **http://photo.obs.**\ *region*.\ *example*\ **.com/picture.jpg**

-  Object

   An object is a basic data unit on OBS. A bucket can store multiple objects, and OBS does not distinguish between object file types. Objects are serialized in OBS. An object may be a text, a video, or any other types of files. In OBS, the size of a file can range from 0 bytes to 48.8 TB. However, when an object is uploaded through the **PutObject** operation, it cannot exceed the maximum size of 5 GB. Use the multipart upload method, if the object size is larger than 5 GB.

-  Region

   A region is a geographic area in which cloud resources are deployed. Availability zones (AZs) in the same region can communicate with each other over an intranet, while AZs in different regions are isolated from each other. Deploying cloud resources in different regions can better suit certain user requirements or comply with local laws or regulations.

   Each bucket in OBS must reside in a region. You can specify the region when creating the bucket. Once a bucket is created, its region cannot be changed. Select the most appropriate region for a bucket based on the location, cost, and regulatory compliance requirements. For details about the available regions, see :ref:`Endpoints <en-us_topic_0031051947__section124911550580>`.
