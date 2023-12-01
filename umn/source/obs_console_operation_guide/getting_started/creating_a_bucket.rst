:original_name: obs_03_0306.html

.. _obs_03_0306:

Creating a Bucket
=================

This section describes how to create a bucket on OBS Console. A bucket is a container that stores objects in OBS. Before you can store data in OBS, you need to create a bucket.

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

      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                                   |
      +===================================+===============================================================================================================================================================================================================================================+
      | Region                            | Geographic area where a bucket resides. For low latency and faster access, select the region nearest to you. Once the bucket is created, its region cannot be changed.                                                                        |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Bucket Name                       | Name of the bucket. A bucket name must be unique across all accounts and regions. Once a bucket is created, its name cannot be changed.                                                                                                       |
      |                                   |                                                                                                                                                                                                                                               |
      |                                   | According to the globally applied DNS naming rules, an OBS bucket name:                                                                                                                                                                       |
      |                                   |                                                                                                                                                                                                                                               |
      |                                   | -  Must be unique across all accounts and regions. The name of a deleted bucket can be reused for another bucket at least 30 minutes later after the deletion.                                                                                |
      |                                   | -  Must be 3 to 63 characters long. Only lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                                                                                                                 |
      |                                   | -  Cannot start or end with a period (.) or hyphen (-), and cannot contain two consecutive periods (..) or contain a period (.) and a hyphen (-) adjacent to each other.                                                                      |
      |                                   | -  Cannot be formatted as an IP address.                                                                                                                                                                                                      |
      |                                   |                                                                                                                                                                                                                                               |
      |                                   |    .. note::                                                                                                                                                                                                                                  |
      |                                   |                                                                                                                                                                                                                                               |
      |                                   |       When you access OBS through HTTPS using virtual hosted-style URLs, if the bucket name contains a period (.), the certificate verification will fail. To work around this issue, you are advised not to use periods (.) in bucket names. |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Bucket Policy                     | Controls read and write permissions for buckets.                                                                                                                                                                                              |
      |                                   |                                                                                                                                                                                                                                               |
      |                                   | -  **Private**: No access beyond the bucket ACL settings is granted.                                                                                                                                                                          |
      |                                   | -  **Public Read**: Anyone can read objects in the bucket.                                                                                                                                                                                    |
      |                                   | -  **Public Read and Write**: Anyone can read, write, or delete objects in the bucket.                                                                                                                                                        |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Tags                              | Optional. Tags are used to identify and classify buckets in OBS. Each tag is represented by a key-value pair.                                                                                                                                 |
      |                                   |                                                                                                                                                                                                                                               |
      |                                   | For more information, see :ref:`Tag Overview <en-us_topic_0059888284>`.                                                                                                                                                                       |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **Create Now**.
