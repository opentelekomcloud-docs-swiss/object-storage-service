:original_name: obs_03_0208.html

.. _obs_03_0208:

Access Keys (AK/SK)
===================

OBS uses access keys to authenticate the identity of a request sender.

Access keys comprise two parts: an access key ID (AK) and a secret access key (SK). AKs are used together with SKs to sign requests cryptographically, ensuring that the requests are confidential, complete, and correct.

The authentication can be based on a permanent AK and SK pair, or based on a temporary AK/SK pair and security token.

**Permanent AK/SK Pairs**

You can create a pair of permanent AK and SK on the **My Credentials** page.

-  Access key ID (AK): It is a unique identifier associated with a secret access key and is used to identify the sender of a request.
-  Secret access key (SK): It is used in combination with the access key ID to sign requests. It can prevent requests from being tampered with and ensures the confidentiality and integrity of the requests.

**Temporary AK/SK Pairs**

A temporary AK/SK pair and security token assigned by OBS comply with the principle of least privilege and are for temporarily accessing OBS. They are valid from 15 minutes to 24 hours, and need to be obtained again once they expire. If the security token is missing from your request, a 403 error will be returned.

-  Temporary access key ID (AK): It is a unique identifier associated with a temporary secret access key and is used to identify the sender of a request.
-  Temporary secret access key (SK): It is used in combination with the temporary access key ID to sign requests. It can prevent requests from being tampered with and ensures the confidentiality and integrity of the requests.
-  Security token: It is used together with the temporary AK and SK to access all resources of a specified account.

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

`Obtaining Permanent Access Keys (AK/SK) <https://docs.sc.otc.t-systems.com/api/obs/obs_04_0116.html>`__

`Obtaining a Temporary AK/SK Pair <https://docs.sc.otc.t-systems.com/api/iam/en-us_topic_0097949518.html>`__
