:original_name: obs_03_0130.html

.. _obs_03_0130:

Restricting Bucket Access to a Specified Address
================================================

You can configure a bucket policy to authorize a specified address the permission to access the bucket. This example shows how to deny a client access whose source IP address is within the range of 114.115.1.0/24.

Procedure
---------

#. In the bucket list, click the bucket to be operated. The **Overview** page of the bucket is displayed.
#. In the navigation pane on the left, click **Permissions** to go to the permission management page.
#. Choose **Bucket Policies** > **Custom Bucket Policies**.
#. Click **Create Bucket Policy**. The **Create Bucket Policy** dialog box is displayed.
#. Configure the parameters according to the following table:

   .. table:: **Table 1** Parameters for authorizing the permission to access a specified bucket

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

Initiate an access request from an IP address within the range of 114.115.1.0/24. The access is denied. Initiate an access request from an IP address outside the range of 114.115.1.0/24. The access is allowed.
