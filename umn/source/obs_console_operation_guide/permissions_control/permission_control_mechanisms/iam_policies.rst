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


.. figure:: /_static/images/en-us_image_0209418410.png
   :alt: **Figure 1** Policy structure

   **Figure 1** Policy structure

Policy syntax example:

.. code-block::

   {
       "Version": "1.1",
       "Statement": [
                   {
               "Effect": "Allow",
               "Action": [
                   "obs:bucket:HeadBucket",
                   "obs:bucket:ListBucket",
                   "obs:bucket:GetBucketLocation"
               ],
               "Resource": [
                   "obs:*:*:bucket:*"
               ],
               "Condition": {
                   "StringEndWithIfExsits": {
                       "g:UserName": ["specialCharacter"]
                   },
                   "Bool": {
                       "g:MFAPresent": ["true"]
                   }
               }
           }
       ]
   }

.. table:: **Table 1** Policy syntax parameters

   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                         | Description                                                                                                                                                                                                                                                                                                                                                                             |
   +===================================+=========================================================================================================================================================================================================================================================================================================================================================================================+
   | Version                           | The version number of a policy.                                                                                                                                                                                                                                                                                                                                                         |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                         |
   |                                   | -  **1.0**: RBAC policies. An RBAC policy consists of permissions for an entire service. Users in a group with such a policy assigned are granted all of the permissions required for that service.                                                                                                                                                                                     |
   |                                   | -  **1.1**: Fine-grained policies. A fine-grained policy consists of API-based permissions for operations on specific resource types. Fine-grained policies, as the name suggests, allow for more fine-grained control than RBAC policies. Users with such fine-grained permissions can only perform authorized operations on specific services.                                        |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Statement                         | Permissions defined by a policy, including **Effect**, **Action**, **Resource**, and **Condition**. **Condition** is optional.                                                                                                                                                                                                                                                          |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                         |
   |                                   | -  **Effect**                                                                                                                                                                                                                                                                                                                                                                           |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                         |
   |                                   |    The valid values for **Effect** are **Allow** and **Deny**. System policies contain only **Allow** statements. For custom policies containing both **Allow** and **Deny** statements, the **Deny** statements take precedence.                                                                                                                                                       |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                         |
   |                                   | -  **Action**                                                                                                                                                                                                                                                                                                                                                                           |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                         |
   |                                   |    Permissions of specific operations on resources in the format of *Service name*:*Resource type*:*Operation*. A policy can contain one or more permissions. The wildcard (``*``) is allowed to indicate all of the services, resource types, or operations depending on its location in the action. OBS has two resource types: bucket and object.                                    |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                         |
   |                                   |    For details about actions, see the topics of "Bucket Actions" and "Object Actions" in the "IAM Policies and Supported Actions" section of the *Object Storage Service API Reference*.                                                                                                                                                                                                |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                         |
   |                                   | -  **Resource**                                                                                                                                                                                                                                                                                                                                                                         |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                         |
   |                                   |    Resources on which the policy takes effect in the format of *Service name*:*Region*:*Domain ID*:*Resource type*:*Resource path*. The wildcard (``*``) is allowed to indicate all of the services, regions, resource types, or resource paths depending on its location in the action. In the JSON view, if **Resource** is not specified, the policy takes effect for all resources. |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                         |
   |                                   |    The value of **Resource** supports uppercase (A to Z), lowercase (a to z) letters, digits (0 to 9), and the following characters: -_*./\\. If the value contains invalid characters, use the wildcard character (``*``).                                                                                                                                                             |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                         |
   |                                   |    OBS is a global service. Therefore, set **Region** to **\***. **Domain ID** indicates the ID of the resource owner. Set it to **\*** to indicate the ID of the account to which the resources belong.                                                                                                                                                                                |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                         |
   |                                   |    Examples:                                                                                                                                                                                                                                                                                                                                                                            |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                         |
   |                                   |    -  **obs:*:*:bucket:\***: all OBS buckets                                                                                                                                                                                                                                                                                                                                            |
   |                                   |    -  **obs:*:*:object:my-bucket/my-object/\***: all objects in the **my-object** directory of the **my-bucket** bucket                                                                                                                                                                                                                                                                 |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                         |
   |                                   | -  **Condition**                                                                                                                                                                                                                                                                                                                                                                        |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                         |
   |                                   |    Conditions for the policy to take effect (Optional). Format: *Condition operator*:*{Condition key:[Value 1, Value 2]}*                                                                                                                                                                                                                                                               |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                         |
   |                                   |    The condition includes the global service condition name and cloud service condition name. The condition names supported by OBS are the same as those in the bucket policy. When configuring in IAM, add **obs:**. For details, see :ref:`Conditions <obs_03_0120>`.                                                                                                                 |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                         |
   |                                   |    The value of **Condition** can contain only uppercase (A to Z), lowercase (a to z) letters, digits (0 to 9), and the following characters: ``-,./_@#$%&.`` If the value contains unsupported characters, consider using the condition operator for fuzzy match, such as StringLike and StringStartWith.                                                                              |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                         |
   |                                   |    Examples:                                                                                                                                                                                                                                                                                                                                                                            |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                         |
   |                                   |    -  **StringEndWithIfExists":{"g:UserName":["specialCharacter"]}**: The statement is valid for users whose names end with **specialCharacter**.                                                                                                                                                                                                                                       |
   |                                   |    -  **"StringLike":{"obs:prefix":["private/"]}**: When listing objects in a bucket, you need to set prefix to **private/** or include **private/**.                                                                                                                                                                                                                                   |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

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
