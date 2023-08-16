:original_name: obs_03_0080.html

.. _obs_03_0080:

Granting an IAM User with the Operation Permissions for a Specified Bucket
==========================================================================

Create an IAM user under in an account. The IAM user has no permission to any resource before it is added to any user group. The bucket owner (root account) or other accounts and IAM users, who have the permission to set bucket policies, can configure bucket policies to grant the bucket operation permissions to IAM users.

The following is an example about how to authorize an IAM user with the bucket access and object upload permissions.

Procedure
---------

#. In the bucket list, click the bucket to be operated. The **Overview** page of the bucket is displayed.
#. In the navigation pane on the left, click **Permissions** to go to the permission management page.
#. Choose **Bucket Policies** > **Custom Bucket Policies**.
#. Click **Create Bucket Policy**. The **Create Bucket Policy** dialog box is displayed.
#. Set the following parameters to authorize the IAM user with the permission to access the bucket (listing objects in the bucket).

   .. table:: **Table 1** Parameters for authorizing the permission to access a specified bucket

      +-----------------------------------+-------------------------------------------------------------------------+
      | Parameter                         | Value                                                                   |
      +===================================+=========================================================================+
      | Policy Mode                       | **Customized**                                                          |
      +-----------------------------------+-------------------------------------------------------------------------+
      | Effect                            | **Allow**                                                               |
      +-----------------------------------+-------------------------------------------------------------------------+
      | Principal                         | -  **Include**                                                          |
      |                                   | -  Select **Current account** and select the IAM user to be authorized. |
      +-----------------------------------+-------------------------------------------------------------------------+
      | Resources                         | -  **Include**                                                          |
      |                                   | -  Leave it blank.                                                      |
      +-----------------------------------+-------------------------------------------------------------------------+
      | Actions                           | -  **Include**                                                          |
      |                                   | -  ListBucket                                                           |
      +-----------------------------------+-------------------------------------------------------------------------+

#. Click **OK**.
#. Click **Create Bucket Policy**. The **Create Bucket Policy** dialog box is displayed.
#. Set the following parameters to authorize the IAM user with the permission to upload objects to the bucket.

   .. note::

      Before authorizing the IAM user with the permission to operate objects, ensure that the user has the permission to access the bucket.

   .. table:: **Table 2** Parameters for authorizing the permission to upload objects

      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Value                                                                                                                                                                                                         |
      +===================================+===============================================================================================================================================================================================================+
      | Policy Mode                       | **Customized**                                                                                                                                                                                                |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Effect                            | **Allow**                                                                                                                                                                                                     |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Principal                         | -  **Include**                                                                                                                                                                                                |
      |                                   | -  Select **Current account** and select the IAM user to be authorized.                                                                                                                                       |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Resources                         | -  **Include**                                                                                                                                                                                                |
      |                                   | -  Resource name: **\***                                                                                                                                                                                      |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Actions                           | -  **Include**                                                                                                                                                                                                |
      |                                   | -  PutObject                                                                                                                                                                                                  |
      |                                   |                                                                                                                                                                                                               |
      |                                   | .. note::                                                                                                                                                                                                     |
      |                                   |                                                                                                                                                                                                               |
      |                                   |    In this example, only the permission to upload objects is granted. You can select multiple actions and granting other operation permissions to the IAM user The asterisk (``*``) indicates all operations. |
      |                                   |                                                                                                                                                                                                               |
      |                                   |    For details about the supported actions, see :ref:`Actions <obs_03_0051>`.                                                                                                                                 |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **OK**.
