:original_name: obs_03_1050.html

.. _obs_03_1050:

Configuring a Lifecycle Rule
============================

Configure a lifecycle rule for a bucket to manage objects in the bucket.

Procedure
---------

#. Log in to OBS Browser+.
#. Select the bucket you want and choose **More** > **Lifecycle Rules**.
#. Click **Create**.
#. Configure related parameters.

   -  **Status**: Select **Enable** to enable this lifecycle rule after the configuration.
   -  **Rule Name**: Enter a rule name that is no longer than 255 characters.
   -  **Applies To**: By selecting **Object name prefix**, the lifecycle rule will apply to objects with the specified prefix contained in their name. You can also select **Bucket** for the lifecycle rule to apply to all objects in the bucket.

   .. note::

      -  If **Object name prefix** is selected and the specified prefix overlaps with the prefix in an existing lifecycle rule, OBS considers the two rules as the same rule and does not allow you to create this rule. For example, if there is a rule with prefix **abc** in the system, another rule whose prefix contains **abc** cannot be configured.
      -  If there is already a lifecycle rule whose **Applies To** is set to **Object name prefix**, you cannot configure a new rule with **Applies To** set to **Bucket**.
      -  If there is already a lifecycle rule whose **Applies To** is set to **Bucket**, you cannot configure a new rule with **Applies To** set to **Object name prefix**.

   -  You can use a lifecycle rule to define how many days after their last update eligible objects are automatically transitioned to the Warm or Cold storage class, or are automatically deleted upon expiration.

      -  **Transition to** **Warm**: This rule transitions the eligible objects to the Warm storage class if the conditions are met.
      -  **Transition to** **Cold**: This rule transitions the eligible objects to the Cold storage class if the conditions are met.
      -  **Expiration Time**: This determines when an object will expire and then be deleted, or the day after which objects matching the rule will be deleted.

#. Click **OK** to save the lifecycle rule.

Related Operations
------------------

After the configuration is complete, you can edit, delete, enable, or disable the configured rule if necessary.
