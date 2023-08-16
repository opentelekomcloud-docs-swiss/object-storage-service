:original_name: obs_faq_0136.html

.. _obs_faq_0136:

Why Can't I Find Certain Objects in a Bucket When I Searched for Them?
======================================================================

On OBS Console and OBS Browser and OBS Browser+, you can search for objects by object name prefix. For example, if you search for **test**, you will find all objects whose names start with **test**. However, if the keyword entered is in the middle or at the end of the object name, the search will not return those results. For example, the name of the object to be searched for is **testabc** and you enter **abc** in the search box, **testabc** will not be found. Only objects whose names start with the prefix **abc** are found.
