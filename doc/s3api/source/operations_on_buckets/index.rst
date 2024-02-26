:original_name: en-us_topic_0125560493.html

.. _en-us_topic_0125560493:

Operations on Buckets
=====================

The requests that are sent to OBS by users must comply with REST specifications and contain required header parameters. If a request is successfully processed, OBS returns a success response. If the request fails to be processed, OBS returns a message that contains the reason of the error. This chapter describes REST operations on buckets using the common header authorization. You can also use temporarily authorized requests described in section :ref:`V2 Temporarily Authorized Request <en-us_topic_0125560431>`.

-  :ref:`PUT Bucket <en-us_topic_0125560305>`
-  :ref:`List Buckets <en-us_topic_0125560308>`
-  :ref:`DELETE Bucket <en-us_topic_0125560472>`
-  :ref:`GET Bucket (List Objects) <en-us_topic_0125560237>`
-  :ref:`GET Bucket Object versions <en-us_topic_0125560273>`
-  :ref:`List Multipart Uploads <en-us_topic_0125560292>`
-  :ref:`HEAD Bucket <en-us_topic_0125560467>`
-  :ref:`GET Bucket location <en-us_topic_0125560404>`
-  :ref:`GET Bucket storage <en-us_topic_0125560293>`
-  :ref:`PUT Bucket quota <en-us_topic_0125560329>`
-  :ref:`GET Bucket quota <en-us_topic_0125560383>`
-  :ref:`PUT Bucket acl <en-us_topic_0125560468>`
-  :ref:`GET Bucket acl <en-us_topic_0125560314>`
-  :ref:`PUT Bucket logging <en-us_topic_0125560299>`
-  :ref:`GET Bucket logging <en-us_topic_0125560463>`
-  :ref:`PUT Bucket policy <en-us_topic_0125560316>`
-  :ref:`GET Bucket policy <en-us_topic_0125560369>`
-  :ref:`DELETE Bucket policy <en-us_topic_0125560427>`
-  :ref:`PUT Bucket lifecycle <en-us_topic_0125560423>`
-  :ref:`GET Bucket lifecycle <en-us_topic_0125560497>`
-  :ref:`DELETE Bucket lifecycle <en-us_topic_0125560506>`
-  :ref:`PUT Bucket website <en-us_topic_0125560321>`
-  :ref:`GET Bucket website <en-us_topic_0125560494>`
-  :ref:`DELETE Bucket website <en-us_topic_0125560295>`
-  :ref:`PUT Bucket versioning <en-us_topic_0125560444>`
-  :ref:`GET Bucket versioning <en-us_topic_0125560345>`
-  :ref:`PUT Bucket CORS <en-us_topic_0125560238>`
-  :ref:`GET Bucket CORS <en-us_topic_0125560258>`
-  :ref:`DELETE Bucket CORS <en-us_topic_0125560432>`
-  :ref:`PUT Bucket Notification <en-us_topic_0125560248>`
-  :ref:`GET Bucket Notification <en-us_topic_0125560442>`
-  :ref:`OPTIONS Bucket <en-us_topic_0125560464>`
-  :ref:`PUT Bucket tagging <en-us_topic_0125560290>`
-  :ref:`GET Bucket tagging <en-us_topic_0125560249>`
-  :ref:`DELETE Bucket tagging <en-us_topic_0125560426>`
-  :ref:`PUT Bucket Inventory <en-us_topic_0000001243677443>`
-  :ref:`GET Bucket Inventory <en-us_topic_0000001198597564>`
-  :ref:`List Bucket Inventory <en-us_topic_0000001198437590>`
-  :ref:`DELETE Bucket Inventory <en-us_topic_0000001243597437>`
-  :ref:`Configuring a Default WORM Policy for a Bucket <en-us_topic_0000001806313033>`
-  :ref:`Obtaining the Default WORM Policy of a Bucket <en-us_topic_0000001759314566>`

.. toctree::
   :maxdepth: 1
   :hidden: 

   put_bucket
   list_buckets
   delete_bucket
   get_bucket_list_objects
   get_bucket_object_versions
   list_multipart_uploads
   head_bucket
   get_bucket_location
   get_bucket_storage
   put_bucket_quota
   get_bucket_quota
   put_bucket_acl
   get_bucket_acl
   put_bucket_logging
   get_bucket_logging
   put_bucket_policy
   get_bucket_policy
   delete_bucket_policy
   put_bucket_lifecycle
   get_bucket_lifecycle
   delete_bucket_lifecycle
   put_bucket_website
   get_bucket_website
   delete_bucket_website
   put_bucket_versioning
   get_bucket_versioning
   put_bucket_cors
   get_bucket_cors
   delete_bucket_cors
   put_bucket_notification
   get_bucket_notification
   options_bucket
   put_bucket_tagging
   get_bucket_tagging
   delete_bucket_tagging
   put_bucket_inventory
   get_bucket_inventory
   list_bucket_inventory
   delete_bucket_inventory
   configuring_a_default_worm_policy_for_a_bucket
   obtaining_the_default_worm_policy_of_a_bucket
