:original_name: obs_03_0208.html

.. _obs_03_0208:

Access Keys (AK/SK)
===================

OBS uses an access key ID (AK) and secret access key (SK) to authenticate the identity of a requester.

The authentication can be based on a permanent AK and SK pair, or based on a temporary AK/SK pair and security token.

**Permanent AK/SK Pair**

You can create a pair of permanent AK and SK on the **My Credentials** page.

-  Access key ID (AK): indicates the ID of the access key. It is the unique ID associated with the SK. The AK and SK are used together to obtain an encrypted signature for a request.
-  Secret access key (SK): indicates the private key used together with its associated AK to cryptographically sign requests. The AK and SK are used together to identify a request sender to prevent the request from being modified.

**Temporary AK/SK Pair**

A temporary AK/SK pair and security token assigned by OBS comply with the principle of least privilege and are for temporarily accessing OBS. They are valid from 15 minutes to 24 hours, and need to be obtained again once they expire. If the security token is missing from your request, a 403 error will be returned.

-  Temporary AK: indicates the ID of a temporary access key. It is the unique ID associated with the SK. The AK and SK are used together to obtain an encrypted signature for a request.
-  Temporary SK: indicates the temporary private key used together with its associated temporary AK. The AK and SK are used together to identify a request sender to prevent the request from being modified.
-  Security token: indicates the token used together with the temporary AK and SK to access all resources of a specified account.

When using the following tools to access OBS resources, you need to use the AK/SK pair for security authentication.

.. table:: **Table 1** OBS resource management tools

   +--------------+-----------------------------------------------------------------+
   | Tool         | AK/SK Configuration                                             |
   +==============+=================================================================+
   | OBS Browser+ | Configure the AK and SK during account configuration.           |
   +--------------+-----------------------------------------------------------------+
   | APIs         | Add the AK/SK pair to the request when computing the signature. |
   +--------------+-----------------------------------------------------------------+

References
----------

For details about how to obtain a permanent AK/SK pair, see `Obtaining Access Keys (AK/SK) <https://docs.sc.otc.t-systems.com/api/obs/obs_04_0116.html>`__.

For details about how to obtain a temporary AK/SK pair and security token, see `Obtaining a Temporary AK/SK <https://docs.sc.otc.t-systems.com/api/iam/en-us_topic_0097949518.html>`__.
