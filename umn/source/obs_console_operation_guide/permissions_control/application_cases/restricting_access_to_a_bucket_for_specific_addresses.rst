:original_name: obs_03_0130.html

.. _obs_03_0130:

Restricting Access to a Bucket for Specific Addresses
=====================================================

You can configure a bucket policy to restrict access to a bucket for specific addresses. This example describes how to deny access from clients whose IP address is in the range of **114.115.1.0/24** to a bucket.

Procedure
---------

#. In the bucket list, click the bucket you want to operate to go to the **Objects** page.
#. In the navigation pane, choose **Permissions** > **Bucket Policies**.
#. Click **Create**.
#. Configure the following parameters in the **Create Bucket Policy** dialog box.

   .. table:: **Table 1** Restricting access to a bucket for specific addresses

      +-----------------------------------+----------------------------------------------------------------+
      | Parameter                         | Description                                                    |
      +===================================+================================================================+
      | Configuration method              | Choose **Visual Editor**.                                      |
      +-----------------------------------+----------------------------------------------------------------+
      | Policy Name                       | Enter a custom name.                                           |
      +-----------------------------------+----------------------------------------------------------------+
      | Effect                            | Deny                                                           |
      +-----------------------------------+----------------------------------------------------------------+
      | Principal                         | Select **All accounts**.                                       |
      +-----------------------------------+----------------------------------------------------------------+
      | Resources                         | Select **Entire bucket (including the objects in it)**.        |
      +-----------------------------------+----------------------------------------------------------------+
      | Actions                           | Select **Customize** and then **\*** (indicating all actions). |
      +-----------------------------------+----------------------------------------------------------------+
      | Conditions                        | -  **Conditional Operator**: **IpAddress**                     |
      |                                   | -  **Key**: **SourceIP**                                       |
      |                                   | -  **Value**: **114.115.1.0/24**                               |
      +-----------------------------------+----------------------------------------------------------------+

#. Click **Create** in the lower right corner.

Verification
------------

Initiate an access request from an IP address in the range of **114.115.1.0/24**. The access is denied. Initiate an access request from an IP address beyond the range of **114.115.1.0/24**. The access is allowed.
