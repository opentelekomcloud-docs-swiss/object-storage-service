:original_name: obs_03_1055.html

.. _obs_03_1055:

Configuring a Bucket Policy
===========================

Bucket policies define the access control over resources (buckets and objects) in OBS.

Procedure
---------

#. Log in to OBS Browser+.

#. Select the bucket you want and choose **More** > **Bucket Policy**. The window shown in :ref:`Figure 1 <obs_03_1055__fig11715141135020>` is displayed.

   .. _obs_03_1055__fig11715141135020:

   .. figure:: /_static/images/en-us_image_0000002683558508.png
      :alt: **Figure 1** Configuring a bucket policy

      **Figure 1** Configuring a bucket policy

#. Enter a bucket policy in the following format.

   a. Grant permissions to an account. In the following example, the account with ID **783fc6652cf246c096ea836694f71855** is granted permission to obtain log management information for bucket **logging.bucket3**.

      .. code-block::

         {
             "Statement": [
                 {
                     "Sid": "testing",
                     "Effect": "Allow",
                     "Principal": {
                         "ID": [
                             "domain/783fc6652cf246c096ea836694f71855:user/*"
                         ]
                     },
                     "Action": [
                         "GetBucketLogging"
                     ],
                     "Resource": [
                         "logging.bucket3"
                     ]
                 }
             ]
         }

      :ref:`Table 1 <obs_03_1055__en-us_topic_0045829128_en-us_topic_0045829071_table11962936162855>` describes the parameters that you need to manually modify in the example above:

      .. _obs_03_1055__en-us_topic_0045829128_en-us_topic_0045829071_table11962936162855:

      .. table:: **Table 1** Parameter changes

         +--------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Item to Modify                       | Description                                                                                                                                                                                                                                                                                                   |
         +======================================+===============================================================================================================================================================================================================================================================================================================+
         | **GetBucketLogging**                 | Value of the **Action** field that indicates all OBS-supported actions in the policy. The value is a case-insensitive string. The value can contain a wildcard character (``*``), for example, **"Action":["List*", "Get*"]**, to apply all actions to the resources. You need to change the value as needed. |
         +--------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | **Allow**                            | Value of the **Effect** field that indicates whether the permission in the policy is allowed or denied. The value must be **Allow** or **Deny**.                                                                                                                                                              |
         +--------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | **logging.bucket3**                  | The bucket on which the policy works. You can change the bucket name as needed.                                                                                                                                                                                                                               |
         +--------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | **783fc6652cf246c096ea836694f71855** | ID of an account. You can change it as needed. You can obtain the account ID on the bucket's **Basic Information** page.                                                                                                                                                                                      |
         +--------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   b. Grant permissions to an IAM user. In the following example, the user (whose ID is **71f3901173514e6988115ea2c26d1999**) under the account (whose ID is **219d520ceac84c5a98b237431a2cf4c2**) is assigned the permission required to set log management for bucket **logging.bucket3**.

      .. code-block::

         {
             "Statement": [
                 {
                     "Sid": "testing",
                     "Effect": "Allow",
                     "Principal": {
                         "ID": [
                             "domain/219d520ceac84c5a98b237431a2cf4c2:user/71f3901173514e6988115ea2c26d1999"
                         ]
                     },
                     "Action": [
                         "PutBucketLogging"
                     ],
                     "Resource": [
                         "logging.bucket3"
                     ]
                 }
             ]
         }

      :ref:`Table 2 <obs_03_1055__en-us_topic_0045829128_en-us_topic_0045829071_table60255350163643>` describes the parameters that you need to manually modify in the example above:

      .. _obs_03_1055__en-us_topic_0045829128_en-us_topic_0045829071_table60255350163643:

      .. table:: **Table 2** Parameter changes

         +--------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Item to Modify                       | Description                                                                                                                                                                                                                                                                                                   |
         +======================================+===============================================================================================================================================================================================================================================================================================================+
         | **PutBucketLogging**                 | Value of the **Action** field that indicates all OBS-supported actions in the policy. The value is a case-insensitive string. The value can contain a wildcard character (``*``), for example, **"Action":["List*", "Get*"]**, to apply all actions to the resources. You need to change the value as needed. |
         +--------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | **Allow**                            | Value of the **Effect** field that indicates whether the permission in the policy is allowed or denied. The value must be **Allow** or **Deny**.                                                                                                                                                              |
         +--------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | **logging.bucket3**                  | The bucket on which the policy works. You can change the bucket name as needed.                                                                                                                                                                                                                               |
         +--------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | **219d520ceac84c5a98b237431a2cf4c2** | ID of an account. You can change it as needed.                                                                                                                                                                                                                                                                |
         |                                      |                                                                                                                                                                                                                                                                                                               |
         |                                      | You can click |image1| next to the target bucket to obtain the **Account ID** on the **Basic Information** page.                                                                                                                                                                                              |
         +--------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | **71f3901173514e6988115ea2c26d1999** | ID of a user under the account. You can change it as needed.                                                                                                                                                                                                                                                  |
         |                                      |                                                                                                                                                                                                                                                                                                               |
         |                                      | You can choose **My Credentials** from the username in the upper right corner of OBS Console to obtain the **IAM User ID**.                                                                                                                                                                                   |
         +--------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   For details about bucket policy parameters, see section "Bucket Policy Parameters" in the *Object Storage Service User Guide*.

.. |image1| image:: /_static/images/en-us_image_0000002713118361.png
