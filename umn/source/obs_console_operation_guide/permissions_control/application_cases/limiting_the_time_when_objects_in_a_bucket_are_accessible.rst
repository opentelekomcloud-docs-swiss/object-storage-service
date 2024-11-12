:original_name: obs_03_0131.html

.. _obs_03_0131:

Limiting the Time When Objects in a Bucket Are Accessible
=========================================================

You can configure the bucket policy to limit the time when objects in a bucket are accessible. In the following example, the access time window is from 2019-03-26T12:00:00Z to 2019-03-26T15:00:00Z.

Procedure
---------

#. In the bucket list, click the bucket you want to operate to go to the **Objects** page.

#. In the navigation pane, choose **Permissions**.

#. Choose **Bucket Policies** and click **Create**.


   .. figure:: /_static/images/en-us_image_0000002049514480.png
      :alt: **Figure 1** Creating a bucket policy

      **Figure 1** Creating a bucket policy

#. Configure parameters listed in the table below.

   .. table:: **Table 1** Parameters for granting permission to access a bucket

      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Value                                                                                                                                 |
      +===================================+=======================================================================================================================================+
      | Configuration method              | Choose **Visual Editor**.                                                                                                             |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------+
      | Policy Name                       | Enter a policy name.                                                                                                                  |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------+
      | Effect                            | **Allow**                                                                                                                             |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------+
      | Principal                         | -  Select **Other accounts**.                                                                                                         |
      |                                   | -  IAM users: Specify IAM users in the *Account ID*\ **/**\ *IAM user ID* format, with each IAM user on a separate line.              |
      |                                   |                                                                                                                                       |
      |                                   |    -  *Account ID*\ **/\*** indicates that permissions are granted to all IAM users under the account.                                |
      |                                   |    -  **\*/\*** indicates that permissions are granted to all anonymous users.                                                        |
      |                                   |                                                                                                                                       |
      |                                   | .. note::                                                                                                                             |
      |                                   |                                                                                                                                       |
      |                                   |    You can obtain the account ID and IAM user ID from the **My Credentials** page.                                                    |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------+
      | Resources                         | Select **Entire bucket (including the objects in it)**.                                                                               |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------+
      | Actions                           | Select **Customize** and click **Select Actions**. In the displayed dialog box, select **Get\*** that indicates all read permissions. |
      |                                   |                                                                                                                                       |
      |                                   | .. caution::                                                                                                                          |
      |                                   |                                                                                                                                       |
      |                                   |    CAUTION:                                                                                                                           |
      |                                   |    Selecting **\*** (indicating all actions) may cause resources to be deleted.                                                       |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------+
      | Conditions                        | -  **Key**: Select **CurrentTime**.                                                                                                   |
      |                                   | -  **Condition Operator**: Select **DateGreaterThan**.                                                                                |
      |                                   | -  **Value**: Enter **2019-03-26T12:00:00Z** (UTC).                                                                                   |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------+
      | Conditions                        | -  **Key**: Select **CurrentTime**.                                                                                                   |
      |                                   | -  **Condition Operator**: Select **DateLessThan**.                                                                                   |
      |                                   | -  **Value**: Enter **2019-03-26T15:00:00Z** (UTC).                                                                                   |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------+

   .. note::

      The preceding two conditions must be configured in the same bucket policy.

#. Click **Create**.

Verification
------------

During the specified time period, any user can access the specified resources in the bucket. Outside the specified time period, only the bucket owner can access the bucket.
