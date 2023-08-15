:original_name: obs_03_0075.html

.. _obs_03_0075:

Configuring an Object Policy
============================

An object policy applies to a specific object, which is also part of a bucket policy. The resource of an object policy is the selected object, and the actions and conditions are the object related actions and conditions configured in the bucket policy.

Procedure
---------

#. In the bucket list, click the bucket to be operated. The **Overview** page of the bucket is displayed.

#. In the navigation pane, click **Objects**.

#. On the right of the object to be operated, choose **More** > **Configure Object Policy**. The **Configure Object Policy** dialog box is displayed.

#. Select a proper policy mode as required. Valid options are as follows:

   -  Read-only mode: The authorized user has the read permission to the object. For follow-up procedure, see :ref:`5 <obs_03_0075__li3552175452220>`.
   -  Read and write mode: The authorized user has the read and write permissions to the object. For follow-up procedure, see :ref:`5 <obs_03_0075__li3552175452220>`.
   -  Customized: The authorized user will be granted with customized permissions to the object. For detailed configuration, see :ref:`6 <obs_03_0075__li588503161565>`.

   .. note::

      You can configure only one object policy at a time.

#. .. _obs_03_0075__li3552175452220:

   For read-only and read and write modes, enter information about the authorized user in the following format and click **OK**.

   .. table:: **Table 1** Object policy parameters in read-only or read and write mode

      +-----------------------+---------------------------------------------+-----------------------------------------------------------------------------------------------------------------+
      | Parameter             | Value                                       | Description                                                                                                     |
      +=======================+=============================================+=================================================================================================================+
      | Principal             | -  **Include** or **Exclude**               | Indicates the user that the object policy applies to.                                                           |
      |                       | -  **Current account** or **Other account** |                                                                                                                 |
      |                       |                                             | -  **Include**: Specifies the user on whom the bucket policy statement takes effect.                            |
      |                       |                                             | -  **Exclude**: Specifies that on all users except the specified user the bucket policy statement takes effect. |
      +-----------------------+---------------------------------------------+-----------------------------------------------------------------------------------------------------------------+
      | Resources             | **Include** or **Exclude**                  | Resources on which the object policy takes effect.                                                              |
      |                       |                                             |                                                                                                                 |
      |                       |                                             | -  **Include**: Indicates that the policy takes effect only on the specified OBS resources.                     |
      |                       |                                             | -  **Exclude**: Indicates that the bucket policy takes effect on all OBS resources except the specified ones.   |
      +-----------------------+---------------------------------------------+-----------------------------------------------------------------------------------------------------------------+

#. .. _obs_03_0075__li588503161565:

   For the customized mode, set parameters based on the site requirements and click **OK**.

   .. table:: **Table 2** Object policy parameters in the custom mode

      +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------+
      | Parameter             | Value                                                                                                                                | Description                                                                                                      |
      +=======================+======================================================================================================================================+==================================================================================================================+
      | Effect                | **Allow** or **Deny**                                                                                                                | Effect of the object policy.                                                                                     |
      |                       |                                                                                                                                      |                                                                                                                  |
      |                       |                                                                                                                                      | -  **Allow**: Indicates that access requests are allowed, if they match the configurations of the bucket policy. |
      |                       |                                                                                                                                      | -  **Deny**: Indicates that access requests are denied, if they match the configurations of the bucket policy.   |
      +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------+
      | Principal             | -  **Include** or **Exclude**                                                                                                        | Specifies users on whom this object policy takes effect.                                                         |
      |                       | -  **Current account** or **Other account**                                                                                          |                                                                                                                  |
      |                       |                                                                                                                                      | -  **Include**: Specifies the user on whom the bucket policy statement takes effect.                             |
      |                       |                                                                                                                                      | -  **Exclude**: Specifies that on all users except the specified user the bucket policy statement takes effect.  |
      +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------+
      | Resources             | -  **Include** or **Exclude**                                                                                                        | Resources on which the object policy takes effect.                                                               |
      |                       |                                                                                                                                      |                                                                                                                  |
      |                       |                                                                                                                                      | -  **Include**: Indicates that the policy takes effect only on the specified OBS resources.                      |
      |                       |                                                                                                                                      | -  **Exclude**: Indicates that the bucket policy takes effect on all OBS resources except the specified ones.    |
      +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------+
      | Actions               | -  **Include** or **Exclude**                                                                                                        | Operation stated in the object policy.                                                                           |
      |                       | -  For details about the actions, see :ref:`Actions Related to Objects <obs_03_0051__section387654045518>`.                          |                                                                                                                  |
      |                       |                                                                                                                                      | -  **Include**: Specifies the actions on which the bucket policy takes effect.                                   |
      |                       |                                                                                                                                      | -  **Exclude**: Specifies that on all except the specified actions the bucket policy takes effect.               |
      +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------+
      | Conditions            | -  **Condition Operator**: For details, see :ref:`Table 1 <obs_03_0120__table16670126115713>`.                                       | Condition for an object policy to take effect.                                                                   |
      |                       | -  **Key**: For details, see :ref:`Table 2 <obs_03_0120__table6707152645718>` and :ref:`Table 4 <obs_03_0120__table14742526145718>`. |                                                                                                                  |
      |                       | -  **Value**: The entered value is associated with the key.                                                                          |                                                                                                                  |
      +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------+

#. Click **OK**.

   After the object policy is configured successfully, it is displayed in the list under **Custom Bucket Policies**.
