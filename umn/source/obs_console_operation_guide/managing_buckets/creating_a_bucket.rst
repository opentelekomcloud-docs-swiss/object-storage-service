:original_name: en-us_topic_0045853662.html

.. _en-us_topic_0045853662:

Creating a Bucket
=================

This section describes how to create a bucket on OBS Console. A bucket is a container that stores objects in OBS. Before you store data in OBS, you need to create a bucket first.

.. note::

   An account can create a maximum of 100 buckets.

Procedure
---------

#. In the upper right corner of the OBS Console homepage, click **Create Bucket**.


   .. figure:: /_static/images/en-us_image_0000001226098225.png
      :alt: **Figure 1** Creating a bucket

      **Figure 1** Creating a bucket

#. Configure bucket parameters.

   .. table:: **Table 1** Bucket parameters

      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                            |
      +===================================+========================================================================================================================================================================================+
      | Region                            | Geographic area where a bucket resides. For low network latency and quick resource access, select the nearest region. Once a bucket is created, the region cannot be changed.          |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Bucket Name                       | Name of the bucket. A bucket name must be unique across all accounts and regions. Once a bucket is created, you cannot change its name.                                                |
      |                                   |                                                                                                                                                                                        |
      |                                   | An OBS bucket must be named according to the globally applied DNS naming rules as follows:                                                                                             |
      |                                   |                                                                                                                                                                                        |
      |                                   | -  A bucket name must be unique across all accounts and regions.                                                                                                                       |
      |                                   | -  A bucket name must contain 3 to 63 characters. Only lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                                            |
      |                                   | -  A bucket name cannot start or end with a period (.) or hyphen (-), and cannot contain two consecutive periods (..) or contain a period (.) and a hyphen (-) adjacent to each other. |
      |                                   | -  A bucket name cannot be an IP address.                                                                                                                                              |
      |                                   |                                                                                                                                                                                        |
      |                                   |    .. note::                                                                                                                                                                           |
      |                                   |                                                                                                                                                                                        |
      |                                   |       If the bucket name contains a period (.), certificate verification will fail when you access OBS through HTTPS using a virtual host.                                             |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Bucket Policy                     | Controls read and write permissions for buckets.                                                                                                                                       |
      |                                   |                                                                                                                                                                                        |
      |                                   | -  **Private**: Only users granted permissions by the ACL can access the bucket.                                                                                                       |
      |                                   | -  **Public Read**: Anyone can read objects in the bucket.                                                                                                                             |
      |                                   | -  **Public Read and Write**: Anyone can read, write, or delete objects in the bucket.                                                                                                 |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Tags                              | Optional. Tags are used to identify and classify buckets in OBS. Each tag is represented by a key-value pair.                                                                          |
      |                                   |                                                                                                                                                                                        |
      |                                   | For more information, see :ref:`Tag Overview <en-us_topic_0059888284>`.                                                                                                                |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **Create Now**.
