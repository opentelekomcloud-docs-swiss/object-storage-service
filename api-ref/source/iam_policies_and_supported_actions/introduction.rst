:original_name: obs_04_0110.html

.. _obs_04_0110:

Introduction
============

This chapter describes fine-grained permissions management for your OBS using Identity and Access Management (IAM). If your account does not require individual IAM users, skip this chapter.

By default, new IAM users do not have any permissions assigned. You need to add a user to one or more groups, and attach IAM policies to these groups. The user then inherits permissions from the groups it is a member of. This process is called authorization. After authorization, the user can perform specified operations on OBS based on the IAM policies.

For details about user policies related to OBS, see the topic of "User Permissions" in the "Service Overview" section of *OBS User Guide*. For details about the syntax structure and examples of IAM policies, see the topic of "IAM Policy" in the section "Permission Control" > "Permission Control Mechanisms" in the "Console Operation Guide" of *OBS User Guide*.

There are fine-grained policies and role-based access control (RBAC) policies. An RBAC policy consists of permissions for an entire service. Users in a group with such a policy assigned are granted all of the permissions required for that service. A fine-grained policy consists of API-based permissions for operations on specific resource types. Fine-grained policies, as the name suggests, allow for more fine-grained control than RBAC policies.

.. note::

   -  If you want to allow or deny the access to an API, fine-grained authorization is a good choice.
   -  Because of the cache, it takes about 13 minutes for the RBAC policy to take effect after being granted to users and user groups. After a fine-grained OBS policy is granted, it takes about 5 minutes for the policy to take effect.

An account has all of the permissions required to call all APIs, but IAM users must have the required permissions specifically assigned. The permissions required for calling an API are determined by the actions supported by the API. Only users who have been granted permissions allowing the actions can call the API successfully. For example, if an IAM user needs to create buckets using an API, the user must have been granted permissions that allow the **obs:bucket:CreateBucket** action.

Supported Actions
-----------------

Operations supported by a fine-grained policy are specific to APIs. The following describes the headers of the actions provided in this chapter:

-  Permissions: defined by actions in a custom policy.
-  APIs: REST APIs that can be called by a custom policy.
-  Actions: added to a custom policy to control permissions for specific operations.

OBS supports the following actions that can be defined in a custom policy:

-  :ref:`Bucket-related actions <obs_04_0111>` include actions supported by all OBS bucket-related APIs, such as the APIs for listing all buckets, creating and deleting buckets, setting bucket policies, setting bucket event notification, and setting bucket logging.
-  :ref:`Object-related actions <obs_04_0112>` include APIs for uploading, downloading, and deleting objects.
