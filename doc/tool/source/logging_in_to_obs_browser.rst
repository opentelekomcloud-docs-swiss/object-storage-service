:original_name: obs_03_1004.html

.. _obs_03_1004:

Logging In to OBS Browser+
==========================

You can log in to OBS Browser+ to access OBS and perform operations on buckets and objects. You can also log in to OBS Browser+ to access other object storage services compatible with OBS.

Cloud users and users of other service providers can use a permanent AK/SK pair to log in to OBS Browser+.

For details, see :ref:`Table 1 <obs_03_1004__table18482104332410>`.

.. _obs_03_1004__table18482104332410:

.. table:: **Table 1** OBS Browser+ login methods

   +---------------------------------------------------+-------------------------------------------------------------------------------------------+----------------------------------+
   | Service                                           | Method                                                                                    | Scenario                         |
   +===================================================+===========================================================================================+==================================+
   | OBS                                               | :ref:`Login with a Permanent AK/SK Pair <obs_03_1004__s6eee9c5cf28244198d6c28ef50ce2276>` | You have a permanent AK/SK pair. |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------+----------------------------------+
   | Other object storage services compatible with OBS |                                                                                           |                                  |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------+----------------------------------+

Prerequisites
-------------

-  You have configured a proxy (if needed) by choosing **More** > **Settings** > **Network** on the login page.

Using OBS Browser+ to Access OBS
--------------------------------

The following explains how to log in to OBS Browser+ to access OBS.

.. _obs_03_1004__s6eee9c5cf28244198d6c28ef50ce2276:

Login with a Permanent AK/SK Pair
---------------------------------

In AK/SK login, you need to enter the AK and SK.

.. note::

   #. OBS Browser+ does not support login using a temporary AK/SK pair and a security token.

|image1|

.. table:: **Table 2** Login parameters

   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Mandatory (Yes/No)    | Description                                                                                                                                                                                                 |
   +=======================+=======================+=============================================================================================================================================================================================================+
   | Account Name          | Yes                   | It is user-defined and is a unique identifier that is different from the cloud service accounts you use to log in to OBS Browser+.                                                                          |
   |                       |                       |                                                                                                                                                                                                             |
   |                       |                       | An account name contains 3 to 63 characters, and cannot contain the following special characters: \\ : \* ? ' < > \| ! @ # $ % ^ ~                                                                          |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Service               | Yes                   | **OBS (default)** is selected by default. Selecting this option allows access to buckets in all regions where OBS is available.                                                                             |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Server Address        | Yes                   | OBS backend address                                                                                                                                                                                         |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access Key ID         | Yes                   | You can click **Obtain Access Keys** on the login page to jump to the IAM console and create access keys.                                                                                                   |
   |                       |                       |                                                                                                                                                                                                             |
   | &                     |                       | -  An access key ID (AK) defines a user that accesses the OBS system. An AK belongs to only one user, but one user can have multiple AKs. OBS identifies users through access key IDs.                      |
   |                       |                       | -  A secret access key (SK) is the key used by users to access OBS. It is the authentication information generated based on the AK and the request header. An SK matches an AK, and they group into a pair. |
   | Secret Access Key     |                       |                                                                                                                                                                                                             |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Access Path           | No                    | Enter the path of a bucket or object. After login, you can only see the specified bucket or object.                                                                                                         |
   |                       |                       |                                                                                                                                                                                                             |
   |                       |                       | Example: **obs://bucket/folder**                                                                                                                                                                            |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. note::

   OBS Browser+ can keep the login information of up to 100 accounts.

.. |image1| image:: /_static/images/en-us_image_0000002002871337.png
