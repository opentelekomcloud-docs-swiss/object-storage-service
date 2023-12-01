:original_name: obs_03_0110.html

.. _obs_03_0110:

IAM Policies
============

You can create IAM users under a registered cloud service account, and then use IAM policies to control users' access permissions to cloud resources.

IAM policies define the actions that can be performed on your cloud resources. In other words, IAM policies specify what actions are allowed or denied.

IAM policies with OBS permissions take effect on all OBS buckets and objects. To grant an IAM user the permission to operate OBS resources, you need to assign one or more OBS permission sets to the user group to which the user belongs.

For details about OBS permissions controlled by IAM policies, see :ref:`Permissions Management <obs_03_0045>`.

IAM policies Application Scenarios
----------------------------------

IAM policies are used to authorize IAM users under an account.

-  Controlling permissions to cloud resources as a whole under an account
-  Controlling permissions to all OBS buckets and objects under an account

.. _obs_03_0110__section9268135516548:

Policy Structure and Syntax
---------------------------

A policy consists of a version and statements. Each policy can have multiple statements.


.. figure:: /_static/images/en-us_image_0170580428.png
   :alt: **Figure 1** Policy structure

   **Figure 1** Policy structure

.. code-block::

   {
         "Version": "1.1",
         "Statement": [
               {
                     "Effect": "Allow",
                     "Action": [
                           "obs:bucket:ListAllMybuckets",
                           "obs:bucket:HeadBucket",
                           "obs:bucket:ListBucket",
                           "obs:bucket:GetBucketLocation"
                     ]
               }
         ]
   }

.. table:: **Table 1** Policy syntax parameters

   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                         | Description                                                                                                                                                                                                                                                                                                                                          |
   +===================================+======================================================================================================================================================================================================================================================================================================================================================+
   | Version                           | The version number of a policy.                                                                                                                                                                                                                                                                                                                      |
   |                                   |                                                                                                                                                                                                                                                                                                                                                      |
   |                                   | -  **1.0**: RBAC policies. An RBAC policy consists of permissions for an entire service. Users in a group with such a policy assigned are granted all of the permissions required for that service.                                                                                                                                                  |
   |                                   | -  **1.1**: Fine-grained policies. A fine-grained policy consists of API-based permissions for operations on specific resource types. Fine-grained policies, as the name suggests, allow for more fine-grained control than RBAC policies. Users with such fine-grained permissions can only perform authorized operations on specific services.     |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Statement                         | Permissions defined by a policy, including **Effect** and **Action**.                                                                                                                                                                                                                                                                                |
   |                                   |                                                                                                                                                                                                                                                                                                                                                      |
   |                                   | -  **Effect**                                                                                                                                                                                                                                                                                                                                        |
   |                                   |                                                                                                                                                                                                                                                                                                                                                      |
   |                                   |    The valid values for **Effect** are **Allow** and **Deny**. System policies contain only **Allow** statements. For custom policies containing both **Allow** and **Deny** statements, the **Deny** statements take precedence.                                                                                                                    |
   |                                   |                                                                                                                                                                                                                                                                                                                                                      |
   |                                   | -  **Action**                                                                                                                                                                                                                                                                                                                                        |
   |                                   |                                                                                                                                                                                                                                                                                                                                                      |
   |                                   |    Permissions of specific operations on resources in the format of *Service name*:*Resource type*:*Operation*. A policy can contain one or more permissions. The wildcard (``*``) is allowed to indicate all of the services, resource types, or operations depending on its location in the action. OBS has two resource types: bucket and object. |
   |                                   |                                                                                                                                                                                                                                                                                                                                                      |
   |                                   |    For details about actions, see the topics of "Bucket-Related Actions" and "Object-Related Actions" in the "IAM Permissions Policies and Supported Actions" section of the *OBS API Reference*.                                                                                                                                                    |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Authentication of IAM policies
------------------------------

The authentication of IAM policies starts from the Deny statements. The following figure shows the authentication logic for resource access.


.. figure:: /_static/images/en-us_image_0170555653.png
   :alt: **Figure 2** Authentication logic

   **Figure 2** Authentication logic

.. note::

   The actions in each policy are in the OR relationship.

#. A user accesses the system and makes an operation request.
#. The system evaluates all the permission policies assigned to the user.
#. In these policies, the system looks for explicit deny permissions. If the system finds an explicit deny that applies, it returns a decision of Deny, and the authentication ends.
#. If no explicit deny is found, the system looks for allow permissions that would apply to the request. If the system finds an explicit allow permission that applies, it returns a decision of Allow, and the authentication ends.
#. If no explicit allow permission is found, IAM returns a decision of Deny, and the authentication ends.
