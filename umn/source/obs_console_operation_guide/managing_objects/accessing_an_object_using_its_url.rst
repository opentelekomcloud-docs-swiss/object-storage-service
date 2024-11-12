:original_name: obs_03_0319.html

.. _obs_03_0319:

Accessing an Object Using Its URL
=================================

You can grant anonymous users the read permission for an object so they can access the object using the shared object URL.

Prerequisites
-------------

Anonymous users have the read permission for the object. For details about permission granting, see :ref:`Granting Anonymous Users Permission to Access Objects <obs_03_0132>`.

.. note::

   Encrypted objects cannot be shared.

Procedure
---------

#. In the bucket list, click the bucket you want to operate to go to the **Objects** page.

#. Click the object to be shared. The object information is displayed on the top part of the page. You can find the link for accessing the object in the **Link** area, as shown in :ref:`Figure 1 <obs_03_0319__fig36534596192426>`.

   Anonymous users can access the object by clicking this link. An object link (URL) is in the format of **https://**\ *Bucket name*.\ *Domain name*/*Directory level*/*Object name*. If the object is in the root directory of the bucket, its URL does not contain any directory level.

   .. _obs_03_0319__fig36534596192426:

   .. figure:: /_static/images/en-us_image_0000001180979114.png
      :alt: **Figure 1** Object link

      **Figure 1** Object link
