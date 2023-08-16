:original_name: en-us_topic_0125560435.html

.. _en-us_topic_0125560435:

Authenticating a Request
========================

For authentication purposes you are issued an access key ID (AK) and a secret access key (SK) upon registration in OBS. A request sent to OBS can be authenticated using its **Authorization** header that contains a signature generated using the SK and request parameters. Before authentication, the names of buckets and objects are URL encoded and then authentication information begins to generate.

OBS supports two authentication modes: V2 authentication and V4 authentication. In OBS however, the recommended authentication mode is V4 as V2 authentication is more susceptible to security breaches. There are three differences between V2 and V4 authentication modes:

-  V4 authentication uses the HMAC-SHA256 algorithm to enhance security.
-  V4 authentication enables user data to incorporate into signature calculation.
-  Users can specify the header that is used for signature calculation in V4 authentication.

.. important::

   V4 authentication is recommended because V2 authentication is more susceptible to security breaches.

-  :ref:`AK and SK Generation <en-us_topic_0125560364>`
-  :ref:`V2 Common Request <en-us_topic_0125560243>`
-  :ref:`V2 Temporarily Authorized Request <en-us_topic_0125560431>`
-  :ref:`V4 Common Request <en-us_topic_0125560310>`
-  :ref:`V4 Temporarily Authorized Request <en-us_topic_0125560420>`
-  :ref:`V4 Browser-based Authorized POST Request <en-us_topic_0125560309>`

.. toctree::
   :maxdepth: 1
   :hidden: 

   ak_and_sk_generation
   v2_common_request
   v2_temporarily_authorized_request
   v4_common_request
   v4_temporarily_authorized_request
   v4_browser-based_authorized_post_request
