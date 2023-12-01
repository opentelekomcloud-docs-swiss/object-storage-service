:original_name: obs_03_0123.html

.. _obs_03_0123:

Configuring a Custom Bucket Policy
==================================

If you want to grant special permissions to specific users, you can configure custom bucket policies. If a standard bucket policy conflicts with a custom bucket policy, the authorization priority is given to the custom bucket policy and then the standard bucket policy.

Procedure
---------

#. In the bucket list, click the bucket you want to operate. The **Overview** page is displayed.

#. In the navigation pane, choose **Permissions**.

#. On the **Bucket Policies** tab page, configure a custom bucket policy according to your needs.

#. Click **Create Bucket Policy**. Select a proper policy mode as required. Valid values are as follows:

   -  **Read-only**: The authorized user will have the read permission on the bucket and objects. For subsequent operations, see :ref:`5 <obs_03_0123__li3552175452220>`.
   -  **Read and write**: The authorized user will have the read and write permissions on the bucket and objects. For subsequent operations, see :ref:`5 <obs_03_0123__li3552175452220>`.
   -  **Customized**: The authorized user will have the customized permissions on the bucket and objects. For detailed configuration, see :ref:`6 <obs_03_0123__li588503161565>`.

   .. note::

      Only one bucket policy mode can be configured at a time.

#. .. _obs_03_0123__li3552175452220:

   For the read-only and read and write modes, enter information about the authorized user in the following format and click **OK**.


   **Figure 1** Parameter settings of a custom bucket policy in the read-only or read and write mode

   |image1|

   .. table:: **Table 1** Parameters in bucket policies

      +-----------------------+--------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter             | Value                                                                                | Description                                                                                                                                    |
      +=======================+======================================================================================+================================================================================================================================================+
      | Principal             | -  **Include** or **Exclude**                                                        | Specifies users on whom this bucket policy takes effect.                                                                                       |
      |                       | -  **Current account** or **Other account**                                          |                                                                                                                                                |
      |                       |                                                                                      | -  **Include**: The policy takes effect on specified users.                                                                                    |
      |                       |                                                                                      | -  **Exclude**: The policy takes effect on all users except the specified ones.                                                                |
      +-----------------------+--------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
      | Resources             | -  **Include** or **Exclude**                                                        | Indicates the resource that a bucket policy applies to. With the read-only mode and read and write mode, the policy can only apply to objects. |
      |                       |                                                                                      |                                                                                                                                                |
      |                       | -  Input format:                                                                     | -  **Include**: The policy takes effect on the specified OBS resources.                                                                        |
      |                       |                                                                                      | -  **Exclude**: The policy takes effect on all OBS resources except the specified ones.                                                        |
      |                       |    Object: *Object name*                                                             |                                                                                                                                                |
      |                       |                                                                                      |                                                                                                                                                |
      |                       |    Object set: *Object name prefix*\ **\***, **\***\ *Object name suffix*, or **\*** |                                                                                                                                                |
      +-----------------------+--------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+

#. .. _obs_03_0123__li588503161565:

   For the customized mode, set parameters based on the site requirements and click **OK**.


   .. figure:: /_static/images/en-us_image_0000001226220197.png
      :alt: **Figure 2** Parameter settings of a custom bucket policy in the customized mode

      **Figure 2** Parameter settings of a custom bucket policy in the customized mode

   :ref:`Table 2 <obs_03_0123__table25824246144542>` describes each parameter.

   .. _obs_03_0123__table25824246144542:

   .. table:: **Table 2** Parameters for configuring a custom bucket policy

      +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------+
      | Parameter             | Value                                                                                                                                                                      | Description                                                                                                 |
      +=======================+============================================================================================================================================================================+=============================================================================================================+
      | Effect                | **Allow** or **Deny**                                                                                                                                                      | Effect of a bucket policy.                                                                                  |
      |                       |                                                                                                                                                                            |                                                                                                             |
      |                       |                                                                                                                                                                            | -  **Allow**: The policy allows the matched requests.                                                       |
      |                       |                                                                                                                                                                            | -  **Deny**: The policy denies the matched requests.                                                        |
      +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------+
      | Principal             | -  **Include** or **Exclude**                                                                                                                                              | Specifies users on whom this bucket policy takes effect.                                                    |
      |                       | -  **Current account** or **Other account**                                                                                                                                |                                                                                                             |
      |                       |                                                                                                                                                                            | -  **Include**: The policy takes effect on specified users.                                                 |
      |                       |                                                                                                                                                                            | -  **Exclude**: The policy takes effect on all users except the specified ones.                             |
      +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------+
      | Resources             | -  **Include** or **Exclude**                                                                                                                                              | Indicates the resource that a bucket policy applies to.                                                     |
      |                       |                                                                                                                                                                            |                                                                                                             |
      |                       | -  Resource input format:                                                                                                                                                  | -  **Include**: The policy takes effect on the specified OBS resources.                                     |
      |                       |                                                                                                                                                                            | -  **Exclude**: The policy takes effect on all OBS resources except the specified ones.                     |
      |                       |    Object: *Object name*                                                                                                                                                   |                                                                                                             |
      |                       |                                                                                                                                                                            | Relationship between resource types and actions:                                                            |
      |                       |    Object set: *Object name prefix*\ **\***, **\***\ *Object name suffix*, or **\***                                                                                       |                                                                                                             |
      |                       |                                                                                                                                                                            | -  When a resource is an object or an object set, only the actions related to the object can be configured. |
      |                       |    Blank: Indicates that the resource is the entire bucket.                                                                                                                | -  When the resource is a bucket, only the actions related to the bucket can be configured.                 |
      +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------+
      | Actions               | -  **Include** or **Exclude**                                                                                                                                              | Operations stated in the bucket policy.                                                                     |
      |                       | -  For details, see :ref:`Actions <obs_03_0051>`.                                                                                                                          |                                                                                                             |
      |                       |                                                                                                                                                                            | -  **Include**: The policy takes effect on specified actions.                                               |
      |                       |                                                                                                                                                                            | -  **Exclude**: The policy takes effect on all actions except the specified ones.                           |
      +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------+
      | Conditions            | -  **Conditional Operator**: See :ref:`Table 1 <obs_03_0120__table16670126115713>`.                                                                                        | Conditions under which the bucket policy takes effect                                                       |
      |                       | -  **Key**: See :ref:`Table 2 <obs_03_0120__table6707152645718>`, :ref:`Table 3 <obs_03_0120__table1972610267573>`, and :ref:`Table 4 <obs_03_0120__table14742526145718>`. |                                                                                                             |
      |                       | -  **Value**: The entered value is associated with the key.                                                                                                                |                                                                                                             |
      +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------+

.. |image1| image:: /_static/images/en-us_image_0000001747145065.png
