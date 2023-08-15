:original_name: obs_03_0045.html

.. _obs_03_0045:

Permissions Management
======================

If you have OBS resources and you need to grant different access permissions to different user roles, you can leverage the Identity and Access Management (IAM) service for fine-grained permission control. IAM provides identity authentication, permissions management, and access control, helping you provide secure access to your cloud resources.

With IAM, you can use your account to create IAM users, and assign permissions to the users to control their access to specific resources. For example, if you have software developers and you want to grant them the permission to only access OBS but not delete OBS resources, you can create an IAM policy that only grants the developers the permission to access OBS.

If your service account does not have individual IAM users, please skip this section.

OBS Permissions
---------------

By default, new IAM users do not have any permissions assigned. You need to add a user to one or more user groups, and assign permission policies to the user groups. The user then inherits permissions from the user groups. This process is known as authorization. After authorization, the user can perform specific operations on cloud services based on permission policies. IAM provides preset system policies that define common permissions for different services.

OBS is a global service because it is available for all physical regions. OBS permissions are assigned to users in the Global project, and users do not need to switch the region when accessing OBS.

Policy Types

-  RBAC policy: An RBAC policy consists of permissions for an entire service. Users in a group with such a policy assigned are granted all the required permissions, including permissions for accessing and managing that service. RBAC policies do not support operation-specific permission control.
-  Fine-grained policy: A fine-grained policy consists of API-based permissions for operations on specific resource types. Fine-grained policies, as the name suggests, allow for more fine-grained control than RBAC policies. Users with such fine-grained permissions can only perform specific operations on services.

.. note::

   Due to data caching, an RBAC policy and fine-grained policy involving OBS actions will take effect 10 to 15 minutes after it is attached to a user and user group.

:ref:`Table 1 <obs_03_0045__table358116162418>` lists all system policies of OBS.

.. _obs_03_0045__table358116162418:

.. table:: **Table 1** OBS system policies

   +-----------------------+-----------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Policy                | Description                                                                                                           | Policy Type           |
   +=======================+=======================================================================================================================+=======================+
   | Tenant Administrator  | Operation permissions: any operation on all cloud resources owned by the account                                      | RBAC policy           |
   |                       |                                                                                                                       |                       |
   |                       | OBS policies are configured under **Global service** > **OBS**.                                                       |                       |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Tenant Guest          | Operation permissions: read-only access permission to all cloud resources owned by the account                        | RBAC policy           |
   |                       |                                                                                                                       |                       |
   |                       | OBS policies are configured under **Global service** > **OBS**.                                                       |                       |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------+-----------------------+
   | OBS Buckets Viewer    | Operation permissions: listing buckets, obtaining basic bucket information, and obtaining bucket metadata information | RBAC policy           |
   |                       |                                                                                                                       |                       |
   |                       | OBS policies are configured under **Global service** > **OBS**.                                                       |                       |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------+-----------------------+

The following table lists operations that can be performed under each set of OBS permission.

.. table:: **Table 2** Permissions and the allowed operations on OBS resources

   +-------------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Operation                                                   | Tenant Administrator Permission | Tenant Guest Permission | OBS Buckets Viewer                                                                |
   +=============================================================+=================================+=========================+===================================================================================+
   | Listing buckets                                             | Yes                             | Yes                     | Yes                                                                               |
   +-------------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Creating buckets                                            | Yes                             | No                      | No                                                                                |
   +-------------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Deleting buckets                                            | Yes                             | No                      | No                                                                                |
   +-------------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Obtaining basic bucket information                          | Yes                             | Yes                     | Yes                                                                               |
   |                                                             |                                 |                         |                                                                                   |
   |                                                             |                                 |                         | .. note::                                                                         |
   |                                                             |                                 |                         |                                                                                   |
   |                                                             |                                 |                         |    The statistics of used storage space and number of objects cannot be obtained. |
   +-------------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Controlling bucket access                                   | Yes                             | No                      | No                                                                                |
   +-------------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Managing bucket policies                                    | Yes                             | No                      | No                                                                                |
   +-------------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Listing objects                                             | Yes                             | Yes                     | Yes                                                                               |
   |                                                             |                                 |                         |                                                                                   |
   |                                                             |                                 |                         | No                                                                                |
   +-------------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Listing objects with multiple versions                      | Yes                             | Yes                     | No                                                                                |
   +-------------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Uploading files                                             | Yes                             | No                      | No                                                                                |
   +-------------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Creating folders                                            | Yes                             | No                      | No                                                                                |
   +-------------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Deleting files                                              | Yes                             | No                      | No                                                                                |
   +-------------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Deleting folders                                            | Yes                             | No                      | No                                                                                |
   +-------------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Downloading files                                           | Yes                             | Yes                     | No                                                                                |
   +-------------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Deleting files with multiple versions                       | Yes                             | No                      | No                                                                                |
   +-------------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Downloading files with multiple versions                    | Yes                             | Yes                     | No                                                                                |
   +-------------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Canceling the deletion of files                             | Yes                             | No                      | No                                                                                |
   +-------------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Deleting fragments                                          | Yes                             | No                      | No                                                                                |
   +-------------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Controlling object access                                   | Yes                             | No                      | No                                                                                |
   +-------------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Configuring object metadata                                 | Yes                             | No                      | No                                                                                |
   +-------------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Obtaining object metadata                                   | Yes                             | No                      | No                                                                                |
   +-------------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Managing versioning                                         | Yes                             | No                      | No                                                                                |
   +-------------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Managing logging                                            | Yes                             | No                      | No                                                                                |
   +-------------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Managing event notifications                                | Yes                             | No                      | No                                                                                |
   +-------------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Managing tags                                               | Yes                             | No                      | No                                                                                |
   +-------------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Managing lifecycle rules                                    | Yes                             | No                      | No                                                                                |
   +-------------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Managing static website hosting                             | Yes                             | No                      | No                                                                                |
   +-------------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Managing CORS rules                                         | Yes                             | No                      | No                                                                                |
   +-------------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Managing URL validation                                     | Yes                             | No                      | No                                                                                |
   +-------------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Appending objects                                           | Yes                             | No                      | No                                                                                |
   +-------------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Configuring an object ACL                                   | Yes                             | No                      | No                                                                                |
   +-------------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Configuring the ACL for an object of a specified version    | Yes                             | No                      | No                                                                                |
   +-------------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Obtaining object ACL information                            | Yes                             | Yes                     | No                                                                                |
   +-------------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Obtaining the ACL information of a specified object version | Yes                             | Yes                     | No                                                                                |
   +-------------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Uploading in the multipart mode                             | Yes                             | No                      | No                                                                                |
   +-------------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Listing uploaded parts                                      | Yes                             | Yes                     | No                                                                                |
   +-------------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+
   | Canceling multipart upload tasks                            | Yes                             | No                      | No                                                                                |
   +-------------------------------------------------------------+---------------------------------+-------------------------+-----------------------------------------------------------------------------------+

Managing OBS Resource Permissions
---------------------------------

Access to OBS buckets and objects can be controlled by IAM user permissions, bucket policies, and ACLs.

For more information, see :ref:`Overview <obs_03_0047>`.
