:original_name: obs_03_0319.html

.. _obs_03_0319:

Accessing an Object Using Its URL
=================================

If you set the permission for an object to allow anonymous users to read it, anonymous users can access the object through the URL that you shared.

Prerequisites
-------------

A read permission has been set for anonymous users. For details about how to enable the permission, see :ref:`Authorizing Access Permissions to Anonymous Users <obs_03_0132>`.

Procedure
---------

#. In the bucket list, click the bucket to be operated. The **Overview** page of the bucket is displayed.

#. In the navigation pane, click **Objects**.

#. Click the object to be shared. The object information is displayed on the top part of the page. The **Link** displays the shared link of the object. For details, see :ref:`Figure 1 <obs_03_0319__fig36534596192426>`.

   Anonymous users can access the object by clicking the URL. The object URL is in the format of **https://**\ *bucket name*.\ *domain name*/*directory level*/*object name*. If the object resides in the root directory of the bucket, its URL does not contain the directory level.

   .. _obs_03_0319__fig36534596192426:

   .. figure:: /_static/images/en-us_image_0000001180979114.png
      :alt: **Figure 1** Object link

      **Figure 1** Object link

   .. note::

      -  The method of using a browser to access objects varies depending on the object type. You can directly open **.txt** and **.html** files using a browser. However, when you open **.exe** and **.dat** files using a browser, the files are automatically downloaded to your local computer.
