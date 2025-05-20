:original_name: obs_03_0312.html

.. _obs_03_0312:

Viewing Basic Information of a Bucket
=====================================

On OBS Console, you can view details about a bucket, including basic bucket information and configurations. You can also export all buckets of the current account and view their basic information in the exported Excel file.

Viewing Bucket Details
----------------------

#. In the bucket list, click the bucket you want to operate to go to the **Objects** page.

#. In the navigation pane, choose **Overview**.

#. On the top of the page, view the bucket information, including the bucket name, storage class, region, and creation time.


   .. figure:: /_static/images/en-us_image_0000002136286606.png
      :alt: **Figure 1** Bucket information

      **Figure 1** Bucket information

   .. table:: **Table 1** Bucket information

      +---------------+--------------------------------------------------------------------------------+
      | Item          | Description                                                                    |
      +===============+================================================================================+
      | Bucket name   | Name of the bucket                                                             |
      +---------------+--------------------------------------------------------------------------------+
      | Storage class | Storage class of the bucket, which can be **Standard**, **Warm**, or **Cold**. |
      +---------------+--------------------------------------------------------------------------------+
      | Region        | Region where the bucket is located                                             |
      +---------------+--------------------------------------------------------------------------------+
      | Created       | Creation time of the bucket                                                    |
      +---------------+--------------------------------------------------------------------------------+

#. In the **Basic Information** area, view the number of objects, used capacity, bucket version, and account ID.


   .. figure:: /_static/images/en-us_image_0000002172177161.png
      :alt: **Figure 2** Bucket's basic information

      **Figure 2** Bucket's basic information

   .. table:: **Table 2** Parameters in the Basic Information area

      +-----------------------------------+------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                          |
      +===================================+======================================================================================================+
      | Objects                           | The total number of objects (including folders and all object versions) stored in a bucket           |
      +-----------------------------------+------------------------------------------------------------------------------------------------------+
      | Used Capacity                     | Total storage space occupied by objects of all versions in the bucket                                |
      |                                   |                                                                                                      |
      |                                   | .. note::                                                                                            |
      |                                   |                                                                                                      |
      |                                   |    If usage statistics is available for the bucket, storage usage data is not displayed here.        |
      +-----------------------------------+------------------------------------------------------------------------------------------------------+
      | Bucket Version                    | Version number of the bucket.                                                                        |
      +-----------------------------------+------------------------------------------------------------------------------------------------------+
      | Account ID                        | Unique identity of the bucket owner. It is the same as **Domain ID** on the **My Credentials** page. |
      +-----------------------------------+------------------------------------------------------------------------------------------------------+

#. In the **Domain Name Details** area, view information about the endpoint, access domain name, and static website hosting domain name. You can also perform related operations by clicking buttons in the **Operation** column.


   .. figure:: /_static/images/en-us_image_0000002171455381.png
      :alt: **Figure 3** Domain name details of the bucket

      **Figure 3** Domain name details of the bucket

#. In the **Basic Configurations** area, view the basic configurations of the bucket, including logging, server-side encryption, WORM retention, and versioning. You can click a card to make required configurations.


   .. figure:: /_static/images/en-us_image_0000002136138984.png
      :alt: **Figure 4** Basic configurations of the bucket

      **Figure 4** Basic configurations of the bucket

Exporting a Bucket List
-----------------------

#. Go to the bucket list.

#. Click **Export** in the upper left corner of the bucket list to export all buckets.


   .. figure:: /_static/images/en-us_image_0000002112504678.png
      :alt: **Figure 5** Exporting all buckets

      **Figure 5** Exporting all buckets

#. Select the buckets to be exported and click **Export** in the upper left corner of the bucket list.


   .. figure:: /_static/images/en-us_image_0000002112506422.png
      :alt: **Figure 6** Exporting the selected buckets

      **Figure 6** Exporting the selected buckets

#. Obtain the bucket list in Excel, which is automatically downloaded to your local computer.

   The file lists all the buckets of the current account and includes the following information: bucket name, storage class, region, used capacity, object quantity, bucket version, and bucket creation time.
