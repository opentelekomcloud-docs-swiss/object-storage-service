:original_name: obs_03_0121.html

.. _obs_03_0121:

Configuring Fine-Grained Policies
=================================

Custom policies can be created to supplement the system-defined policies of OBS.

Procedure
---------

#. Log in to the IAM management console.
#. In the navigation pane on the left, click **Policies**.
#. On the page that is displayed, click **Create Custom Policy**.
#. On the **Create Custom Policy** page, set the following parameters:

   .. table:: **Table 1** Custom policy parameters

      +-----------------------------------+------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                              |
      +===================================+==========================================================================================+
      | Policy Name                       | Only letters, digits, and the following special characters are allowed: -_.,             |
      +-----------------------------------+------------------------------------------------------------------------------------------+
      | Scope                             | Select the scope based on the service properties. OBS is a global-level service.         |
      +-----------------------------------+------------------------------------------------------------------------------------------+
      | Description                       | (Optional) Brief description about the policy                                            |
      +-----------------------------------+------------------------------------------------------------------------------------------+
      | Policy Information                | After you select a template, you can customize the content.                              |
      |                                   |                                                                                          |
      |                                   | For details, see :ref:`Policy Structure and Syntax <obs_03_0110__section9268135516548>`. |
      +-----------------------------------+------------------------------------------------------------------------------------------+

   .. note::

      A custom policy can contain multiple authorization items. In addition to the authorization items related to OBS, it can also contain authorization items related other services. But the other services must be at the same project level as OBS.

#. Click **OK** to complete the configuration.
#. Grant fine-grained permissions to a user group and add a user to the user group, so that the user can have the granted permissions. For details, see :ref:`Creating an IAM User and Granting OBS Permissions <obs_03_0122>`.
