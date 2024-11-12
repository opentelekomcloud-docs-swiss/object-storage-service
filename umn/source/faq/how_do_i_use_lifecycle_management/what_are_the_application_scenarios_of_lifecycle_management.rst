:original_name: obs_faq_0027.html

.. _obs_faq_0027:

What Are the Application Scenarios of Lifecycle Management?
===========================================================

You may configure lifecycle rules to:

-  Periodically delete logs that are only meant to be retained for a specific period of time (a week or a month).
-  Transition documents that are seldom accessed to the Warm or Cold storage class or delete them.

If you want to delete a large number of objects from a bucket, you can configure a lifecycle rule to automatically delete the expired objects. :ref:`Table 1 <obs_faq_0027__table115262311380>` lists the parameters for configuring such a lifecycle rule on OBS Console.

.. _obs_faq_0027__table115262311380:

.. table:: **Table 1** Parameters for deletion upon expiration

   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------+
   | Parameter                         | Value                                                                                                             |
   +===================================+===================================================================================================================+
   | Status                            | Enable                                                                                                            |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------+
   | Rule Name                         | Example: **rule-delete**                                                                                          |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------+
   | Applies To                        | You can apply the deletion rule to the entire bucket or to objects that share the same name prefix in the bucket. |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------+
   | Current Version                   | Expiration Time                                                                                                   |
   |                                   |                                                                                                                   |
   |                                   | Days: 1                                                                                                           |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------+
   | Historical Version                | Expiration Time                                                                                                   |
   |                                   |                                                                                                                   |
   |                                   | Days: 1                                                                                                           |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------+

One day later, objects in the bucket are successfully deleted based on the rule. If you no longer need this lifecycle rule, you can disable it or delete it.
