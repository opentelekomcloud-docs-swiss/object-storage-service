:original_name: en-us_topic_0045853659.html

.. _en-us_topic_0045853659:

Lifecycle Management Overview
=============================

Lifecycle management means periodically deleting objects in a bucket by configuring rules.

You may configure lifecycle rules to:

-  Periodically delete logs that are only meant to be retained for a specific period of time (a week or a month).

You can define lifecycle rules for identifying objects and manage lifecycles of the objects based on the rules.

Lifecycle rules have two key elements:

-  Configuration policy:

   You can also specify the prefix of object names so that objects whose names have this prefix are restricted by the rules. You can configure a lifecycle rule for a bucket so that all objects in the bucket can be restricted by the lifecycle rule.

-  Expiration time: You can specify the number of days after which objects are automatically deleted or the day after which an object that matches with a rule is deleted.
