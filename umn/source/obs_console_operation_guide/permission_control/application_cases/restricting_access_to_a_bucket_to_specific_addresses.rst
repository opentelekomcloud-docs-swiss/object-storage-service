:original_name: obs_03_0130.html

.. _obs_03_0130:

Restricting Access to a Bucket to Specific Addresses
====================================================

You can configure a bucket policy to restrict access to a bucket to specified addresses. This example describes how to deny access from clients whose IP address is in the range of **114.115.1.0/24** to a bucket.

Procedure
---------

#. In the bucket list, click the bucket you want to operate. The **Overview** page is displayed.
#. In the navigation pane, choose **Permissions**.
#. Choose **Bucket Policies** > **Custom Bucket Policies**.
#. Click **Create Bucket Policy**. The **Create Bucket Policy** dialog box is displayed.
#. Configure parameters listed in the table below.

   .. table:: **Table 1** Restricting access to a bucket to specified addresses

      +-----------------------------------+------------------------------------------------------------------------------------------------+
      | Parameter                         | Value                                                                                          |
      +===================================+================================================================================================+
      | Policy Mode                       | **Customized**                                                                                 |
      +-----------------------------------+------------------------------------------------------------------------------------------------+
      | Effect                            | Deny                                                                                           |
      +-----------------------------------+------------------------------------------------------------------------------------------------+
      | Principal                         | -  **Include** > **Other account**                                                             |
      |                                   | -  If the account ID is set to **\***, the policy setting takes effect on all anonymous users. |
      |                                   | -  Leave the user ID blank.                                                                    |
      +-----------------------------------+------------------------------------------------------------------------------------------------+
      | Resources                         | -  **Include**                                                                                 |
      |                                   | -  Leave the field blank, indicating the policy takes effect on the entire bucket.             |
      +-----------------------------------+------------------------------------------------------------------------------------------------+
      | Actions                           | -  **Include**                                                                                 |
      |                                   | -  Select the asterisk (*), indicating all actions are involved.                               |
      +-----------------------------------+------------------------------------------------------------------------------------------------+
      | Conditions                        | -  **Conditional Operator**: **IpAddress**                                                     |
      |                                   | -  **Key**: **SourceIP**                                                                       |
      |                                   | -  **Value**: **114.115.1.0/24**                                                               |
      +-----------------------------------+------------------------------------------------------------------------------------------------+

#. Click **OK**.

Verification
------------

Initiate an access request from an IP address in the range of **114.115.1.0/24**. The access is denied. Initiate an access request from an IP address beyond the range of **114.115.1.0/24**. The access is allowed.
