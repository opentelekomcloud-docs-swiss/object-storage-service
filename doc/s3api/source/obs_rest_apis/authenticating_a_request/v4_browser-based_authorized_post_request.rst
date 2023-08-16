:original_name: en-us_topic_0125560309.html

.. _en-us_topic_0125560309:

V4 Browser-based Authorized POST Request
========================================

OBS supports browser-based **POST** object uploading requests. The authentication information about these requests is uploaded by a form. :ref:`Table 1 <en-us_topic_0125560309__table27141505>` lists the mandatory parameters.

.. _en-us_topic_0125560309__table27141505:

.. table:: **Table 1** V4 POST uploading authentication parameters in the form

   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                         | Description                                                                                                                                                                                                                              |
   +===================================+==========================================================================================================================================================================================================================================+
   | Policy                            | The value of this parameter is a code in Base64 format. It is the code of the security policy of this request.                                                                                                                           |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | x-amz-algorithm                   | Indicates a signature algorithm. For a V4 signature, the value of the parameter is fixed to **AWS4-HMAC-SHA256**.                                                                                                                        |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | x-amz-credential                  | In addition to the **access key ID**, region and service information must be provided. The information must be the same as that used to calculate the **Signing Key**. The value of this parameter is expressed in the following format: |
   |                                   |                                                                                                                                                                                                                                          |
   |                                   | <your-access-key-id>/<date>/<AWS-region>/<AWS-service>/aws4_request.OBS region                                                                                                                                                           |
   |                                   |                                                                                                                                                                                                                                          |
   |                                   | The value is the same as that used for common authentication.                                                                                                                                                                            |
   |                                   |                                                                                                                                                                                                                                          |
   |                                   | Example:                                                                                                                                                                                                                                 |
   |                                   |                                                                                                                                                                                                                                          |
   |                                   | AKIAIOSFODNN7EXAMPLE/20150721/region-1/s3/aws4_request.                                                                                                                                                                                  |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | x-amz-date                        | Indicates the request generation time. It is in the ISO 8601 format. The value must be the same as that of the **x-am-date** field in the policy.                                                                                        |
   |                                   |                                                                                                                                                                                                                                          |
   |                                   | Example:                                                                                                                                                                                                                                 |
   |                                   |                                                                                                                                                                                                                                          |
   |                                   | 20150721T201207Z.                                                                                                                                                                                                                        |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | x-amz-signature                   | Indicates the HMAC-SHA256 hash value of the policy in V4.                                                                                                                                                                                |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Policy is a character string in JSON format and consists of two parts:

-  **expiration** (indicates the request expiration time).
-  **conditions** (indicates parameter restrictions in the form).

An example is as follows:

.. code-block::

   {
    "expiration": "2015-08-06T12:00:00.000Z",
    "conditions": [
      {"bucket": "bucketname"},
      ["starts-with", "$key", "user/user1/"],
      {"acl": "public-read"},
      {"success_action_redirect":
   "http://acl6.obs.example.com/successful_upload.html"},
      ["starts-with", "$Content-Type", "image/"],
      {"x-amz-meta-uuid": "14365123651274"},
      ["starts-with", "$x-amz-meta-tag", ""],
      {"x-amz-credential": "AKIAIOSFODNN7EXAMPLE/20150806/region-1/s3/aws4_request"},
      {"x-amz-algorithm": "AWS4-HMAC-SHA256"},
      {"x-amz-date": "20150806T000000Z" }
    ]
    }

:ref:`Table 2 <en-us_topic_0125560309__table42946954>` lists the mandatory parameters of Policy.

.. _en-us_topic_0125560309__table42946954:

.. table:: **Table 2** Mandatory parameters of Policy in V4 POST uploading requests

   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                         | Description                                                                                                                                                                                                                              |
   +===================================+==========================================================================================================================================================================================================================================+
   | x-amz-algorithm                   | Indicates the used signature algorithm. In V4, the value of the parameter is **AWS4-HMAC-SHA256**.                                                                                                                                       |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | x-amz-credential                  | In addition to the **access key ID**, region and service information must be provided. The information must be the same as that used to calculate the **Signing Key**. The value of this parameter is expressed in the following format: |
   |                                   |                                                                                                                                                                                                                                          |
   |                                   | <your-access-key-id>/<date>/<AWS-region>/<AWS-service>/aws4_request.                                                                                                                                                                     |
   |                                   |                                                                                                                                                                                                                                          |
   |                                   | Example:                                                                                                                                                                                                                                 |
   |                                   |                                                                                                                                                                                                                                          |
   |                                   | AKIAIOSFODNN7EXAMPLE/20150721/region-1/s3/aws4_request.                                                                                                                                                                                  |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | x-amz-date                        | Indicates the Start time of the validity period of **Signing Key**. The value is expressed in ISO 8601 format. The value must be the same as that of the **x-am-date** field in the Signing Key.                                         |
   |                                   |                                                                                                                                                                                                                                          |
   |                                   | Example:                                                                                                                                                                                                                                 |
   |                                   |                                                                                                                                                                                                                                          |
   |                                   | 20150721T201207Z                                                                                                                                                                                                                         |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

The signature calculation process of V4 POST uploading requests is similar to that of V4 common requests. The only difference lies in the **Policy** in the request used by **StringToSign** in V4. The **Policy** is obtained by Base64 encoding based on the original **Policy** character string. :ref:`Figure 1 <en-us_topic_0125560309__fig1971331315531>` shows the computing process.

.. _en-us_topic_0125560309__fig1971331315531:

.. figure:: /_static/images/en-us_image_0125560298.png
   :alt: **Figure 1** Signature calculation process of objects uploaded using V4 POST uploading requests

   **Figure 1** Signature calculation process of objects uploaded using V4 POST uploading requests
