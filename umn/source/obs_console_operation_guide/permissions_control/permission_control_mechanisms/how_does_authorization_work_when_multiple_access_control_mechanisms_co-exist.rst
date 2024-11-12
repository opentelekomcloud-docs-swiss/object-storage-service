:original_name: obs_03_0114.html

.. _obs_03_0114:

How Does Authorization Work When Multiple Access Control Mechanisms Co-Exist?
=============================================================================

-  Based on the principle of least privilege, the default access control result is always deny, and an explicit deny statement always take precedence over an allow statement.

   Suppose that IAM policies grant a user the access to an object, a bucket policy denies the user's access to that object, and there is no ACL configured. Then user's access to the object will be denied.

-  If no method specifies an allow statement, then the request will be denied by default. Only if no method specifies a deny statement and one or more methods specify an allow statement, will the request be allowed.

   For example, if a bucket has multiple bucket policies with allow statements, the adding of a new bucket policy with an allow statement will simply add the allowed permissions to the bucket, but the adding of a new bucket policy with a deny statement will result in a re-arrangement of the permissions. The deny statement will take precedence over allowed statements, even the denied permissions are allowed in other bucket policies.


.. figure:: /_static/images/en-us_image_0168203499.png
   :alt: **Figure 1** Authorization process

   **Figure 1** Authorization process

:ref:`Figure 2 <obs_03_0114__fig1251114133010>` is a matrix of the IAM policies, bucket policies, and ACLs (allow and deny effects).

.. _obs_03_0114__fig1251114133010:

.. figure:: /_static/images/en-us_image_0168203521.png
   :alt: **Figure 2** Matrix of the IAM policies, bucket policies, and ACLs (allow and deny effects)

   **Figure 2** Matrix of the IAM policies, bucket policies, and ACLs (allow and deny effects)
