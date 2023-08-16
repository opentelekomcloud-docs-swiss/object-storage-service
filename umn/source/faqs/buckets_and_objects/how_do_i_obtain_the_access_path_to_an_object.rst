:original_name: obs_faq_0031.html

.. _obs_faq_0031:

How Do I Obtain the Access Path to an Object?
=============================================

Object access paths use the following format: **https://**\ *{bucket name}*\ **.**\ *{domain name}*\ **/**\ *{object name}*.

You can combine a path manually or use the tools in the following table to obtain it.

.. table:: **Table 1** How to obtain an object URL

   +--------------+------------------------------------------------------------------------------------------------------------------------------------+
   | Tool         | Object URL                                                                                                                         |
   +==============+====================================================================================================================================+
   | OBS Console  | Click the object and copy the URL for the detailed information of the object.                                                      |
   +--------------+------------------------------------------------------------------------------------------------------------------------------------+
   | OBS Browser+ | Click the **Attribute** button of the object and then you can copy the URL displayed in the detailed information about the object. |
   +--------------+------------------------------------------------------------------------------------------------------------------------------------+
   | API          | Not supported                                                                                                                      |
   +--------------+------------------------------------------------------------------------------------------------------------------------------------+

.. note::

   If the object access path is user-assembled, you need to escape the object name by referring to the URL encoding rules.
