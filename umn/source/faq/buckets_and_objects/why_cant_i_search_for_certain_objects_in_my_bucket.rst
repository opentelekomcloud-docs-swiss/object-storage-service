:original_name: obs_faq_0136.html

.. _obs_faq_0136:

Why Can't I Search for Certain Objects in My Bucket?
====================================================

On OBS Console and OBS Browser and OBS Browser+, you can search for objects by object name prefix. For example, if you search for **test**, you will find all objects whose name starts with **test**. However, if the keyword entered is in the middle or at the end of the object name, the search will not return those results. For example, you want to search for **testabc** and you enter **abc** in the search box, **testabc** will not be found. Only objects whose name starts with the prefix **abc** will be found.
