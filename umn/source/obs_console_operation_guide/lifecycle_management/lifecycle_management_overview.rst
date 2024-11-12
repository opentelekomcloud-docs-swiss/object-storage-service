:original_name: en-us_topic_0045853659.html

.. _en-us_topic_0045853659:

Lifecycle Management Overview
=============================

Lifecycle management means periodically deleting objects in a bucket or transitioning between object storage classes by configuring rules.


.. figure:: /_static/images/en-us_image_0138955590.png
   :alt: **Figure 1** Lifecycle management

   **Figure 1** Lifecycle management

You may configure lifecycle rules to:

-  Periodically delete logs that are only meant to be retained for a specific period of time (a week or a month).
-  Transition documents that are seldom accessed to the Warm or Cold storage class or delete them.

You can define lifecycle rules for your scenarios similar to those mentioned above to better manage your objects.

You can configure lifecycle rules for objects that will no longer be frequently accessed to transition them to the Warm or Cold storage class as needed. This can help reduce costs on storage. In short, transition basically means that the object storage class is altered without copying the object. You can also manually change the storage class of an object on the Objects page. For details, see :ref:`Uploading an Object <en-us_topic_0045853663>`.

Lifecycle rules have the following key elements:

-  Policy

   You can specify an object name prefix to apply a lifecycle rule to a set of objects. You can also apply a lifecycle rule to the entire bucket (including the objects in it).

-  Time

   You can specify the number of days after which objects that have been last updated and meet specified conditions are automatically transitioned to Warm or Cold, or are expired and then deleted.

   -  Transition to Warm: This defines the number of days since the last object update after which objects meeting specified conditions are automatically transitioned to the Warm storage class.
   -  Transition to Cold: This defines the number of days since the last object update after which objects meeting specified conditions are automatically transitioned to the Cold storage class.
   -  Expiration time: This defines the number of days since the last object update after which objects meeting specified conditions are automatically expired and then deleted.

-  Expiration time

   You can specify the number of days since the last object update after which objects meeting specified conditions are automatically expired and then deleted.

Objects can be transitioned to Warm at least 30 days after their last update. If you configure to transition objects first to Warm and then Cold, the objects must stay Warm at least 30 days before they can be transitioned to Cold. For example, if you configure to transition objects to Warm 33 days after their last update, the objects can be transitioned to Cold at least 63 days after their last update. If transition to Cold is used, but transition to Warm is not, there is no limit on the number of days for transition. The number set for expiration time must be larger than that specified for any of the transition operations.
