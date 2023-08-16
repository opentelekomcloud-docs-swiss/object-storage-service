:original_name: obs_faq_0027.html

.. _obs_faq_0027:

What Are the Application Scenarios of Lifecycle Management?
===========================================================

Lifecycle management applies to the following scenarios:

-  Some periodically uploaded files need only to be retained for one week or one month, and can be deleted once they have expired.

If you want to delete a large number of objects from a bucket, you can configure a lifecycle rule to implement automatic deletion upon expiration or schedule the time for automatic deletion. On the **Lifecycle Rule** page, create rules and configure parameters by referring to :ref:`Table 1 <obs_faq_0027__table115262311380>`:

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

One day later, objects in the bucket are successfully deleted based on the rule. If you do not need this lifecycle rule, you can disable it or delete it.
