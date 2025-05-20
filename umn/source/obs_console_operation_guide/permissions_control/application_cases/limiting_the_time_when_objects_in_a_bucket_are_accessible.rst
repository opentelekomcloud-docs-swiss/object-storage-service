:original_name: obs_03_0131.html

.. _obs_03_0131:

Limiting the Time When Objects in a Bucket Are Accessible
=========================================================

You can configure the bucket policy to limit the time when objects in a bucket are accessible. In the following example, the access time window is from 2019-03-26T12:00:00Z to 2019-03-26T15:00:00Z.

Procedure
---------

#. In the bucket list, click the bucket you want to operate to go to the **Objects** page.
#. In the navigation pane, choose **Permissions** > **Bucket Policies**.
#. Click **Create**.
#. Configure the following parameters in the **Create Bucket Policy** dialog box.

   .. table:: **Table 1** Parameters for limiting the time when objects in the bucket are accessible

      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                      |
      +===================================+==================================================================================================================================+
      | Configuration method              | Choose **Visual Editor**.                                                                                                        |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
      | Policy Name                       | Enter a custom name.                                                                                                             |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
      | Effect                            | Allow                                                                                                                            |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
      | Principal                         | Select **All accounts**.                                                                                                         |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
      | Resources                         | Select **Entire bucket (including the objects in it)**.                                                                          |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
      | Actions                           | Select **Customize** and then **\*** (indicating all actions).                                                                   |
      |                                   |                                                                                                                                  |
      |                                   | .. note::                                                                                                                        |
      |                                   |                                                                                                                                  |
      |                                   |    Selecting **\*** may cause resources to be deleted. To avoid this risk, select **Get\*** that indicates all read permissions. |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
      | Conditions                        | -  Condition 1:                                                                                                                  |
      |                                   |                                                                                                                                  |
      |                                   |    -  Condition Operator: DateGreaterThan                                                                                        |
      |                                   |    -  Key: CurrentTime                                                                                                           |
      |                                   |    -  Value: 2019-03-26T12:00:00Z (UTC format)                                                                                   |
      |                                   |                                                                                                                                  |
      |                                   | -  Condition 2:                                                                                                                  |
      |                                   |                                                                                                                                  |
      |                                   |    -  Condition Operator: DateLessThan                                                                                           |
      |                                   |    -  Key: CurrentTime                                                                                                           |
      |                                   |    -  Value: 2019-03-26T15:00:00Z (UTC format)                                                                                   |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------+

#. Click **Create** in the lower right corner.

Verification
------------

During the specified time period, any user can access the specified resources in the bucket. Outside the specified time period, only the bucket owner can access the bucket.
