:original_name: obs_03_0130.html

.. _obs_03_0130:

Restricting Access to a Bucket for Specific Addresses
=====================================================

You can configure a bucket policy to restrict access to a bucket for specific addresses. This example describes how to deny access from clients whose IP address is in the range of **114.115.1.0/24** to a bucket.

Procedure
---------

#. In the bucket list, click the bucket you want to operate to go to the **Objects** page.
#. In the navigation pane, choose **Permissions**.
#. Choose **Bucket Policies**.
#. Click **Create**.
#. Configure parameters listed in the table below.

   .. table:: **Table 1** Parameters for granting the object listing and upload permissions

      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------+
      | Parameter             |                       | Description                                                                                                              |
      +=======================+=======================+==========================================================================================================================+
      | Configuration method  |                       | Choose **Visual Editor**.                                                                                                |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------+
      | Policy Name           |                       | Enter a custom policy name.                                                                                              |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------+
      | Policy content        | Effect                | Select **Deny**.                                                                                                         |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------+
      |                       | Principal             | -  Select **Other accounts**.                                                                                            |
      |                       |                       | -  IAM users: Specify IAM users in the *Account ID*\ **/**\ *IAM user ID* format, with each IAM user on a separate line. |
      |                       |                       |                                                                                                                          |
      |                       |                       |    -  *Account ID*\ **/\*** indicates that permissions are granted to all IAM users under the account.                   |
      |                       |                       |    -  **\*/\*** indicates that permissions are granted to all anonymous users.                                           |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------+
      |                       | Resources             | Select **Entire bucket (including the objects in it)**.                                                                  |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------+
      |                       | Actions               | Select **Customize** and then **\*** (indicating all actions).                                                           |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------+
      |                       | Conditions            | -  **Key**: Select **SourceIp**.                                                                                         |
      |                       |                       | -  **Condition Operator**: Select **IpAddress**.                                                                         |
      |                       |                       | -  **Value**: Enter **114.115.1.0/24**.                                                                                  |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------+

#. Click **Create**.

Verification
------------

Initiate an access request from an IP address in the range of **114.115.1.0/24**. The access is denied. Initiate an access request from an IP address beyond the range of **114.115.1.0/24**. The access is allowed.
