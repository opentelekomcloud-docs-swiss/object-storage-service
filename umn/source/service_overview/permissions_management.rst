:original_name: obs_03_0045.html

.. _obs_03_0045:

Permissions Management
======================

You can use Identity and Access Management (IAM) to manage OBS permissions and control access to your resources. IAM provides identity authentication, permissions management, and access control.

You can create IAM users for your employees, and assign permissions to these users on a principle of least privilege (PoLP) basis to control their access to specific resource types. For example, you can create IAM users for software developers and assign specific permissions to allow them to use OBS resources but prevent them from being able to delete resources or perform any high-risk operations.

If your account does not require individual IAM users for permissions management, skip this section.

OBS Permissions
---------------

By default, new IAM users do not have any permissions assigned. You can assign permissions to these users by adding them to one or more groups and attaching policies to the groups. IAM provides preset system policies that define common permissions for different services, such as full control access and read-only. You can directly use these preset policies.

OBS is a global service deployed and accessed without specifying any physical region. OBS permissions are assigned to users in the global project, and users do not need to switch regions when accessing OBS.

Policy Types

-  RBAC policy: An RBAC policy consists of permissions for an entire service. Users in a group with such a policy assigned are granted all the required permissions, including permissions for accessing and managing that service. RBAC policies do not support operation-specific permission control.
-  Fine-grained policy: A fine-grained policy consists of API-based permissions for operations on specific resource types. Fine-grained policies, as the name suggests, allow for more fine-grained control than RBAC policies. Users with such fine-grained permissions can only perform specific operations on services.

.. note::

   Due to data caching, an RBAC policy or a fine-grained policy involving OBS actions will take effect 10 to 15 minutes after it is attached to a user or a user group.

:ref:`Table 1 <obs_03_0045__table358116162418>` lists all system policies of OBS.

.. _obs_03_0045__table358116162418:

.. table:: **Table 1** OBS system policies

   +-----------------------+--------------------------------------------------------------------------------------+-----------------------+
   | Policy                | Description                                                                          | Policy Type           |
   +=======================+======================================================================================+=======================+
   | Tenant Administrator  | Allows you to perform any operation on all cloud resources under the account.        | RBAC policy           |
   |                       |                                                                                      |                       |
   |                       | OBS policies are configured under **Global service** > **OBS**.                      |                       |
   +-----------------------+--------------------------------------------------------------------------------------+-----------------------+
   | Tenant Guest          | Allows you to perform read-only operations on all cloud resources under the account. | RBAC policy           |
   |                       |                                                                                      |                       |
   |                       | OBS policies are configured under **Global service** > **OBS**.                      |                       |
   +-----------------------+--------------------------------------------------------------------------------------+-----------------------+
   | OBS Buckets Viewer    | Allows you to list buckets, and obtain basic bucket information and bucket metadata. | RBAC policy           |
   |                       |                                                                                      |                       |
   |                       | OBS policies are configured under **Global service** > **OBS**.                      |                       |
   +-----------------------+--------------------------------------------------------------------------------------+-----------------------+

The following table lists operations that can be performed under each set of OBS permission.

.. table:: **Table 2** Permissions and the allowed operations on OBS resources

   +----------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Operation                                                | Tenant Administrator Permission | Tenant Guest Permission | OBS Buckets Viewer                                                                |
   +==========================================================+=================================+=========================+===================================================================================+
   | Listing buckets                                          | Supported                       | Supported               | Supported                                                                         |
   +----------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Creating buckets                                         | Supported                       | Not supported           | Not supported                                                                     |
   +----------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Deleting buckets                                         | Supported                       | Not supported           | Not supported                                                                     |
   +----------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Obtaining basic bucket information                       | Supported                       | Supported               | Supported                                                                         |
   |                                                          |                                 |                         |                                                                                   |
   |                                                          |                                 |                         | .. note::                                                                         |
   |                                                          |                                 |                         |                                                                                   |
   |                                                          |                                 |                         |    The statistics of used storage space and number of objects cannot be obtained. |
   +----------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Controlling bucket access                                | Supported                       | Not supported           | Not supported                                                                     |
   +----------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Managing bucket policies                                 | Supported                       | Not supported           | Not supported                                                                     |
   +----------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Changing bucket storage classes                          | Supported                       | Not supported           | Not supported                                                                     |
   +----------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Listing objects                                          | Supported                       | Supported               | Supported                                                                         |
   |                                                          |                                 |                         |                                                                                   |
   |                                                          |                                 |                         | Not supported                                                                     |
   +----------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Listing objects with multiple versions                   | Supported                       | Supported               | Not supported                                                                     |
   +----------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Uploading files                                          | Supported                       | Not supported           | Not supported                                                                     |
   +----------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Creating folders                                         | Supported                       | Not supported           | Not supported                                                                     |
   +----------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Deleting objects                                         | Supported                       | Not supported           | Not supported                                                                     |
   +----------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Deleting folders                                         | Supported                       | Not supported           | Not supported                                                                     |
   +----------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Downloading objects                                      | Supported                       | Supported               | Not supported                                                                     |
   +----------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Deleting object versions                                 | Supported                       | Not supported           | Not supported                                                                     |
   +----------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Downloading object versions                              | Supported                       | Supported               | Not supported                                                                     |
   +----------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Changing object storage classes                          | Supported                       | Not supported           | Not supported                                                                     |
   +----------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Restoring objects                                        | Supported                       | Not supported           | Not supported                                                                     |
   +----------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Undeleting objects                                       | Supported                       | Not supported           | Not supported                                                                     |
   +----------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Deleting fragments                                       | Supported                       | Not supported           | Not supported                                                                     |
   +----------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Controlling object access                                | Supported                       | Not supported           | Not supported                                                                     |
   +----------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Configuring object metadata                              | Supported                       | Not supported           | Not supported                                                                     |
   +----------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Obtaining object metadata                                | Supported                       | Not supported           | Not supported                                                                     |
   +----------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Managing versioning                                      | Supported                       | Not supported           | Not supported                                                                     |
   +----------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Managing logging                                         | Supported                       | Not supported           | Not supported                                                                     |
   +----------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Managing event notifications                             | Supported                       | Not supported           | Not supported                                                                     |
   +----------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Managing tags                                            | Supported                       | Not supported           | Not supported                                                                     |
   +----------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Managing lifecycle rules                                 | Supported                       | Not supported           | Not supported                                                                     |
   +----------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Managing static website hosting                          | Supported                       | Not supported           | Not supported                                                                     |
   +----------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Managing CORS rules                                      | Supported                       | Not supported           | Not supported                                                                     |
   +----------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Managing URL validation                                  | Supported                       | Not supported           | Not supported                                                                     |
   +----------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Appending data to objects                                | Supported                       | Not supported           | Not supported                                                                     |
   +----------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Configuring an object ACL                                | Supported                       | Not supported           | Not supported                                                                     |
   +----------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Configuring the ACL for an object of a specified version | Supported                       | Not supported           | Not supported                                                                     |
   +----------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Obtaining object ACL information                         | Supported                       | Supported               | Not supported                                                                     |
   +----------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Obtaining the ACL of a specific object version           | Supported                       | Supported               | Not supported                                                                     |
   +----------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Initiating a multipart upload                            | Supported                       | Not supported           | Not supported                                                                     |
   +----------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Listing uploaded parts                                   | Supported                       | Supported               | Not supported                                                                     |
   +----------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Canceling multipart uploads                              | Supported                       | Not supported           | Not supported                                                                     |
   +----------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+

OBS Resource Permissions Management
-----------------------------------

Access to OBS buckets and objects can be controlled by IAM user permissions, bucket policies, and ACLs.

For more information, see :ref:`Overview <obs_03_0047>`.
