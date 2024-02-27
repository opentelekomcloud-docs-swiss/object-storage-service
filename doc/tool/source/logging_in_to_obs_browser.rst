:original_name: obs_03_1004.html

.. _obs_03_1004:

Logging In to OBS Browser+
==========================

OBS Browser+ supports login using a permanent AK.

.. note::

   #. If a proxy is required for access, choose **More** > **Settings** > **Network** on the login page to configure the proxy before login.
   #. OBS Browser+ does not support login using a temporary AK/SK pair and a security token.

Permanent AK Login
------------------

In AK-based login mode, access keys (AK and SK) are used for login authentication. You need to enter the AK and SK for login.

|image1|

.. table:: **Table 1** Login parameters

   +-----------------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                         | Mandatory (Yes/No)    | Description                                                                                                                                                                                                                                         |
   +===================================+=======================+=====================================================================================================================================================================================================================================================+
   | Account Name                      | Yes                   | Account names are used to differentiate login accounts of OBS Browser+, which do not have to be the same as your cloud service account.                                                                                                             |
   +-----------------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Service                           | Yes                   | Support for the default OBS or other object storage services compatible with OBS.                                                                                                                                                                   |
   |                                   |                       |                                                                                                                                                                                                                                                     |
   |                                   |                       | -  **OBS (default)**: Selecting this option allows operations on buckets in all regions available on OBS.                                                                                                                                           |
   |                                   |                       | -  **Other object storage services**: With this option selected, you need to specify the corresponding service address (endpoint of the object storage service), either the global or regional domain name.                                         |
   +-----------------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Server Address                    | Yes                   | OBS backend address                                                                                                                                                                                                                                 |
   +-----------------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access Key ID & Secret Access Key | Yes                   | AK login leverages the access key authentication mechanism of IAM. You can click **Obtain Access Keys** on the login page to jump to the IAM console and create access keys. More information about access keys (AK and SK) is provided as follows: |
   |                                   |                       |                                                                                                                                                                                                                                                     |
   |                                   |                       | -  An access key ID (AK) defines a user that accesses the OBS system. An AK belongs to only one user, but one user can have multiple AKs. OBS identifies users through access key IDs.                                                              |
   |                                   |                       | -  A secret access key (SK) is the key used by users to access OBS. It is the authentication information generated based on the AK and the request header. An SK matches an AK, and they group into a pair.                                         |
   +-----------------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access Path                       | No                    | You can enter a frequently used path in the text box, so that you will be directed to the path upon login. Example: obs://bucketName/folder01/                                                                                                      |
   +-----------------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Remember my access keys           | No                    | If you select this option, the access keys (both AK and SK) are saved. You do not need to enter the access keys upon next login. To avoid account information leakage, deselect this option on a temporary computer.                                |
   +-----------------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. note::

   -  OBS Browser+ can keep the login information of up to 100 accounts.
   -  If a proxy is required to access your network environment, configure the network proxy before login.

.. |image1| image:: /_static/images/en-us_image_0000001198508245.png
