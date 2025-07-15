:original_name: en-us_topic_0125560489.html

.. _en-us_topic_0125560489:

Operations on Objects
=====================

The requests that are sent to OBS by users must comply with REST specifications and contain required header parameters. If a request is successfully processed, OBS returns a success response. If the request fails to be processed, OBS returns a message that contains the reason of the error. This chapter describes REST operations on objects using the common header authorization. You can also use temporarily authorized requests described in section :ref:`V2 Temporarily Authorized Request <en-us_topic_0125560431>`.

-  :ref:`PUT Object <en-us_topic_0125560399>`
-  :ref:`POST Object <en-us_topic_0125560263>`
-  :ref:`GET Object <en-us_topic_0125560336>`
-  :ref:`PUT Object - Copy <en-us_topic_0125560348>`
-  :ref:`DELETE Object <en-us_topic_0125560459>`
-  :ref:`DELETE Multiple Objects <en-us_topic_0125560366>`
-  :ref:`HEAD Object <en-us_topic_0125560379>`
-  :ref:`PUT Object acl <en-us_topic_0125560460>`
-  :ref:`GET Object acl <en-us_topic_0125560291>`
-  :ref:`Initiate Multipart Upload <en-us_topic_0125560339>`
-  :ref:`Upload Part <en-us_topic_0125560486>`
-  :ref:`Upload Part - Copy <en-us_topic_0125560361>`
-  :ref:`List Parts <en-us_topic_0125560266>`
-  :ref:`Complete Multipart Upload <en-us_topic_0125560338>`
-  :ref:`Abort Multipart Upload <en-us_topic_0125560402>`
-  :ref:`OPTIONS Object <en-us_topic_0125560261>`
-  :ref:`POST Object restore <en-us_topic_0125560388>`
-  :ref:`Configuring WORM Retention for an Object <en-us_topic_0000001806154009>`

.. toctree::
   :maxdepth: 1
   :hidden: 

   put_object
   post_object
   get_object
   put_object_copy
   delete_object
   delete_multiple_objects
   head_object
   put_object_acl
   get_object_acl
   initiate_multipart_upload
   upload_part
   upload_part_copy
   list_parts
   complete_multipart_upload
   abort_multipart_upload
   options_object
   post_object_restore
   configuring_worm_retention_for_an_object
