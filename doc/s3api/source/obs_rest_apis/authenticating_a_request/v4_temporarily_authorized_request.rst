:original_name: en-us_topic_0125560420.html

.. _en-us_topic_0125560420:

V4 Temporarily Authorized Request
=================================

The authentication information in V4 temporarily authorized requests is delivered using the query parameters. The URL of V4 temporary authentication has six mandatory query parameters unlike V2 authentication. The following is an example of a V4 temporarily authorized request.

.. code-block::

   https://bucketname.obs.example.com/test.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIOSFODNN7EXAMPLE%2F20150524%2Fregion-1%2Fs3%2Faws4_request&X-Amz-Date=20150524T000000Z&X-Amz-Expires=86400&X-Amz-SignedHeaders=host&X-Amz-Signature=<signature-value>

:ref:`Table 1 <en-us_topic_0125560420__table43771375>` lists the six mandatory query parameters.

.. _en-us_topic_0125560420__table43771375:

.. table:: **Table 1** Six mandatory query parameters

   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                         | Description                                                                                                                                                                                                                                                                      |
   +===================================+==================================================================================================================================================================================================================================================================================+
   | X-Amz-Algorithm                   | Indicates the AWS signature algorithm.                                                                                                                                                                                                                                           |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | X-Amz-Credential                  | In addition to the **access key ID**, region and service information must be provided. The information must be the same as that used to calculate the **Signing Key**. The value of this parameter is expressed in the following format:                                         |
   |                                   |                                                                                                                                                                                                                                                                                  |
   |                                   | <your-access-key-id>/<date>/<AWS-region>/<AWS-service>/aws4_request.OBS region                                                                                                                                                                                                   |
   |                                   |                                                                                                                                                                                                                                                                                  |
   |                                   | The value is the same as that used for common authentication.                                                                                                                                                                                                                    |
   |                                   |                                                                                                                                                                                                                                                                                  |
   |                                   | Example:                                                                                                                                                                                                                                                                         |
   |                                   |                                                                                                                                                                                                                                                                                  |
   |                                   | AKIAIOSFODNN7EXAMPLE/20150721/region-1/s3/aws4_request                                                                                                                                                                                                                           |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | X-Amz-Date                        | Indicates the request generation time. It is in the ISO 8601 format. The value must be the same as that used for signature calculation.                                                                                                                                          |
   |                                   |                                                                                                                                                                                                                                                                                  |
   |                                   | Example:                                                                                                                                                                                                                                                                         |
   |                                   |                                                                                                                                                                                                                                                                                  |
   |                                   | 20150721T201207Z                                                                                                                                                                                                                                                                 |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | X-Amz-Expires                     | Indicates the URL expiration time. The value is an integer expressed in seconds such as 86,400 seconds (24 hours). It ranges from 1 to 604,800 (7 days). The maximum validity period of the URL is 7 days because the validity period for **Signing Key** calculation is 7 days. |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | X-Amz-SignedHeaders               | Indicates the header list for signature calculation. The HTTP host header is mandatory. All headers that start with **x-amz-\*** must be used to calculate signatures and contained in the header list. All request headers must be included to ensure security.                 |
   |                                   |                                                                                                                                                                                                                                                                                  |
   |                                   | .. warning::                                                                                                                                                                                                                                                                     |
   |                                   |                                                                                                                                                                                                                                                                                  |
   |                                   |    If headers contain *gzip*, *no-cache*, *chunked*, *identity*, *keep-alive*, *bytes*, and *close*, please use lowercase letters. Otherwise, you will receive a **SignatureDoesNotMatch** error response.                                                                       |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | X-Amz-Signature                   | Indicates the signature of a request.                                                                                                                                                                                                                                            |
   |                                   |                                                                                                                                                                                                                                                                                  |
   |                                   | Example:                                                                                                                                                                                                                                                                         |
   |                                   |                                                                                                                                                                                                                                                                                  |
   |                                   | 733255ef022bec3f2a8701cd61d4b371f3f28c9f193a1f02279211d48d5193d7                                                                                                                                                                                                                 |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

:ref:`Figure 1 <en-us_topic_0125560420__fig11837114385216>` shows the signature computing process of V4 temporarily authorized requests.

.. _en-us_topic_0125560420__fig11837114385216:

.. figure:: /_static/images/en-us_image_0125560454.png
   :alt: **Figure 1** Signature calculation process of V4 temporarily authorized requests

   **Figure 1** Signature calculation process of V4 temporarily authorized requests

The signature calculation process of V4 temporarily authorized requests is the same as that of V4 common requests. The only difference lies in the **Hashed Payload** value that is used to calculate the signature of **Canonical Request**. The **Hashed Payload** value is the fixed character string: **UNSIGNED-PAYLOAD**.
