:original_name: obs_faq_0037.html

.. _obs_faq_0037:

Why Are Fragments Generated?
============================

Fragments are incomplete data in buckets generated due to data upload failures.

Fragments are generated when multipart upload tasks fail. Such failures generally occur in the following scenarios:

-  The network is in poor conditions, and the connection to the OBS server is interrupted frequently.
-  The upload task is manually suspended.
-  The device is faulty.
-  The device is powered off suddenly.
