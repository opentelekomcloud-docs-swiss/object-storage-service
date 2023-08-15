:original_name: obs_03_0084.html

.. _obs_03_0084:

Configure a Bucket Inventory
============================

Procedure
---------

#. In the bucket list, click the bucket to be operated. The **Overview** page of the bucket is displayed.

#. In the navigation pane on the left, click **Inventories**. The page with the list of inventories is displayed.

#. Click **Create Inventory**. The **Create Inventory** dialog box is displayed.

#. Set the required parameters.

   .. table:: **Table 1** Parameters for configuring a bucket inventory

      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                          |
      +===================================+======================================================================================================================================================================+
      | Inventory Name                    | Name of a bucket inventory                                                                                                                                           |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Filter                            | Filtering condition of an inventory. You can enter an object name prefix, then the inventory generated will cover objects whose names begin with the same prefix.    |
      |                                   |                                                                                                                                                                      |
      |                                   | An inventory can only filter objects by a specified prefix. If the filter is not specified, the inventory covers the entire bucket.                                  |
      |                                   |                                                                                                                                                                      |
      |                                   | If a bucket has multiple inventories, overlaps between the inventory filters are not allowed.                                                                        |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Save Inventory Files To           | Select a bucket where the generated inventory files are stored. This bucket and the source bucket must be in the same region.                                        |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Inventory File Name Prefix        | Prefix of the storage path of the inventory files.                                                                                                                   |
      |                                   |                                                                                                                                                                      |
      |                                   | Once an inventory file is generated, its saving path is in the following format: *Inventory file name prefix/Source bucket name/Inventory name/Date and time/files/* |
      |                                   |                                                                                                                                                                      |
      |                                   | If this parameter is not specified, the system automatically adds the prefix **BucketInventory** to an inventory file.                                               |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Frequency                         | The frequency when inventory files are generated. It can be set to **Daily** or **Weekly**.                                                                          |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Status                            | Status of the configured inventory. You can enable or disable it to make the configuration effective or ineffective.                                                 |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **Next** to go to the **Configure Report** page.


   .. figure:: /_static/images/en-us_image_0000001225983381.png
      :alt: **Figure 1** Configuring the report

      **Figure 1** Configuring the report

#. Configure the report.

   .. table:: **Table 2** Report related parameters

      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                                                                                                                                                                                        |
      +===================================+====================================================================================================================================================================================================================================================================================================================================================================================================+
      | Inventory Format                  | Inventory files can be saved only in the CSV format.                                                                                                                                                                                                                                                                                                                                               |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Object Versions                   | Object versions that you want to list in an inventory file. It can be set to **Current version only** or **Include all versions**.                                                                                                                                                                                                                                                                 |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Optional Fields                   | Indicates object information fields that can be contained in an inventory file. Value options: **Size**, **Last modified date**, **Etag**, **Multipart upload**, and **Replication status**                                                                                                                                                                                                        |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Send Notification                 | When a new inventory file is generated, a notification message is sent to the email address or mobile number specified in the SMN topic.                                                                                                                                                                                                                                                           |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                                                    |
      |                                   | If you enable the notification function, an SMN event notification rule will be created in the bucket where inventory files are stored. You can view details about the rule on the **SMN** tab page of the **Event Notification** configuration of the bucket. If you disable the notification function or modify the SMN topic, the SMN event notification rule will also be deleted or modified. |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **Next** to confirm the bucket policy.

   A bucket policy is created on the bucket where inventory files are to be stored to allow inventory files be written to the bucket.

#. Click **Create**.
