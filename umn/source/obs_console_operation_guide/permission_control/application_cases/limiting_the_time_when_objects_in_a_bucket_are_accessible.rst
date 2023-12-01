:original_name: obs_03_0131.html

.. _obs_03_0131:

Limiting the Time When Objects in a Bucket Are Accessible
=========================================================

You can configure the bucket policy to limit the time when objects in a bucket are accessible. In the following example, the access time window is from 2019-03-26T12:00:00Z to 2019-03-26T15:00:00Z.

Procedure
---------

#. In the bucket list, click the bucket you want to operate. The **Overview** page is displayed.

#. In the navigation pane, choose **Permissions**.

#. Choose **Bucket Policies** > **Custom Bucket Policies**.

#. Click **Create Bucket Policy**. The **Create Bucket Policy** dialog box is displayed.


   .. figure:: /_static/images/en-us_image_0000001180502386.png
      :alt: **Figure 1** Creating a custom bucket policy

      **Figure 1** Creating a custom bucket policy

#. Configure parameters listed in the table below.

   .. table:: **Table 1** Parameters for granting permission to access a bucket

      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Value                                                                                                                                                                                                                      |
      +===================================+============================================================================================================================================================================================================================+
      | Policy Mode                       | **Customized**                                                                                                                                                                                                             |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Effect                            | **Allow**                                                                                                                                                                                                                  |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Principal                         | -  **Include**                                                                                                                                                                                                             |
      |                                   | -  Select **Other account**, and enter an asterisk (*) as the account ID, indicating all anonymous users.                                                                                                                  |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Resources                         | -  **Include**                                                                                                                                                                                                             |
      |                                   | -  Set the resource name to **\***, indicating all resources in the bucket.                                                                                                                                                |
      |                                   |                                                                                                                                                                                                                            |
      |                                   | .. note::                                                                                                                                                                                                                  |
      |                                   |                                                                                                                                                                                                                            |
      |                                   |    This example only grants permissions for resources in the bucket. If you also want to grant permission for the bucket (for example, the permission to list objects in the bucket), create another custom bucket policy. |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Actions                           | -  **Include**                                                                                                                                                                                                             |
      |                                   | -  Select **\*** as the action name, which indicates all action permissions.                                                                                                                                               |
      |                                   |                                                                                                                                                                                                                            |
      |                                   | .. note::                                                                                                                                                                                                                  |
      |                                   |                                                                                                                                                                                                                            |
      |                                   |    Selecting **\*** may cause resources to be deleted. To avoid this risk, select **Get\*** that indicates all read permissions.                                                                                           |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Conditions                        | -  Condition Operator: DateGreaterThan                                                                                                                                                                                     |
      |                                   | -  Key: CurrentTime                                                                                                                                                                                                        |
      |                                   | -  Value: 2019-03-26T12:00:00Z (UTC format)                                                                                                                                                                                |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Conditions                        | -  Condition Operator: DateLessThan                                                                                                                                                                                        |
      |                                   | -  Key: CurrentTime                                                                                                                                                                                                        |
      |                                   | -  Value: 2019-03-26T15:00:00Z (UTC format)                                                                                                                                                                                |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   .. note::

      The preceding two conditions must be configured in the same bucket policy.

#. Click **OK**.

Verification
------------

During the specified time period, any user can access the specified resources in the bucket. Outside the specified time period, only the bucket owner can access the bucket.
