:original_name: obs_03_0084.html

.. _obs_03_0084:

Configuring a Bucket Inventory
==============================

Procedure
---------

#. In the bucket list, click the bucket you want to operate to go to the **Objects** page.

#. In the navigation pane, choose **Inventories**. The inventory list is displayed.

#. Click **Create Inventory**. The **Create Inventory** dialog box is displayed.

#. Configure required parameters.

   .. table:: **Table 1** Parameters for configuring a bucket inventory

      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                 |
      +===================================+=============================================================================================================================================+
      | Inventory Name                    | Name of a bucket inventory                                                                                                                  |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
      | Filter                            | Filter of an inventory. You can enter an object name prefix for OBS to create an inventory for objects with the specified prefix.           |
      |                                   |                                                                                                                                             |
      |                                   | Currently, only a prefix can be used as a filter. If the filter is not specified, the inventory covers all objects in the bucket.           |
      |                                   |                                                                                                                                             |
      |                                   | If a bucket has multiple inventories, their filters cannot overlap with each other.                                                         |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
      | Save Inventory Files To           | Select a bucket (destination bucket) for saving generated inventory files. This bucket must be in the same region as the source bucket.     |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
      | Inventory File Name Prefix        | Prefix of the inventory file path.                                                                                                          |
      |                                   |                                                                                                                                             |
      |                                   | An inventory file will be saved in the following path: *Inventory file name prefix/Source bucket name/Inventory name/Date and time/files/*. |
      |                                   |                                                                                                                                             |
      |                                   | If this parameter is not specified, OBS automatically adds **BucketInventory** as the prefix to inventory file's path.                      |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
      | Frequency                         | How frequently inventory files are generated. It can be set to **Daily** or **Weekly**.                                                     |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
      | Status                            | Inventory status. You can enable or disable the generation of inventories.                                                                  |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **Next** to go to the **Configure Report** page.


   .. figure:: /_static/images/en-us_image_0000001225983381.png
      :alt: **Figure 1** Configuring the report

      **Figure 1** Configuring the report

#. Configure the report.

   .. table:: **Table 2** Parameters for configuring a report

      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                                                                                                                                                       |
      +===================================+===================================================================================================================================================================================================================================================================================================================================================================+
      | Inventory Format                  | Inventory files can only be saved in CSV format.                                                                                                                                                                                                                                                                                                                  |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Object Versions                   | Object versions that you want to list in an inventory file. It can be set to **Current version only** or **Include all versions**.                                                                                                                                                                                                                                |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Optional Fields                   | Object information fields that can be contained in an inventory file, including **Size**, **Last modified date**, **Storage class**, **ETag**, **Multipart upload**, **Encryption status**, and **Replication status**.                                                                                                                                           |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Send Notification                 | If there is a new inventory file generated, a notification will be sent to the email address or mobile number specified in the SMN topic.                                                                                                                                                                                                                         |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                   |
      |                                   | If you enable the notification function, an SMN event notification rule will be created in the bucket where inventory files are stored. You can view details about the rule on the **Event Notification** page of the bucket. If you disable the notification function or modify the SMN topic, the SMN event notification rule will also be deleted or modified. |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **Next** to confirm the bucket policy.

   OBS then automatically creates a bucket policy on the destination bucket to grant OBS permission to write inventory files to the bucket.

#. Click **Create**.
