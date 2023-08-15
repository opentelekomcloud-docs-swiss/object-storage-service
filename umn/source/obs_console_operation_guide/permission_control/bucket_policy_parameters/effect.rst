:original_name: obs_03_0115.html

.. _obs_03_0115:

Effect
======

A bucket policy can either allow or deny the access requests that match the configuration.

-  **Allow**: Indicates that access requests are allowed, if they match the configurations of the bucket policy.
-  **Deny**: Indicates that access requests are denied, if they match the configurations of the bucket policy.

When a bucket policy contains both the allow and deny effects, the deny effect prevails. The following figure shows the judgment process.


.. figure:: /_static/images/en-us_image_0168267011.png
   :alt: **Figure 1** Determining a bucket policy when the allow and deny statements conflict

   **Figure 1** Determining a bucket policy when the allow and deny statements conflict

#. A user initiates an access request.
#. OBS preferentially searches for deny (explicit deny) effects from bucket policies. If a deny statement is found, OBS directly rejects the access. The access request ends.
#. If there is no deny statement, OBS searches for allow statements.

   -  If an allow statement is found, OBS allows the access.
   -  If no allow statement is found, OBS rejects the access. The access request ends.

#. If an error occurs during the judgment, an error message is generated and returned to the user who initiates the access request.
