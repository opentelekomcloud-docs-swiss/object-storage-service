:original_name: en-us_topic_0045853659.html

.. _en-us_topic_0045853659:

Lifecycle Management Overview
=============================

Lifecycle management means periodically deleting objects in a bucket by configuring rules.

Lifecycle management applies to the following scenarios:

-  Some periodically uploaded files need only to be retained for one week or one month, and can be deleted once they have expired.

You can define lifecycle rules for identifying objects and manage lifecycles of the objects based on the rules.

Lifecycle rules have two key elements:

-  Configuration policy:

   You can also specify the prefix of object names so that objects whose names have this prefix are restricted by the rules. You can configure a lifecycle rule for a bucket so that all objects in the bucket can be restricted by the lifecycle rule.

-  Expiration time: You can specify the number of days after which objects are automatically deleted or the day after which an object that matches with a rule is deleted.
