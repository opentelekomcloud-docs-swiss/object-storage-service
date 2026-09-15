:original_name: obs_03_1044.html

.. _obs_03_1044:

Managing Fragments
==================

Context
-------

Data is uploaded to OBS using multipart upload. In the event of some situations, data uploads usually fail and generate fragments. You need to clear these fragments to free up storage space. The situations include but are not limited to the following:

-  The network is in poor condition, and connection to the OBS server is frequently interrupted.
-  The upload task is manually suspended.
-  The device is faulty.
-  The device is suddenly powered off.

With fragment management, you can clear fragments that are generated due to data upload failures.

.. important::

   Deleted fragments cannot be recovered. Before deleting fragments, ensure that all multipart uploads are complete, or deleting fragments may cause uploads to fail.

Procedure
---------

#. Log in to OBS Browser+.

#. Select the bucket you want and click **Fragments**.

#. In the **Fragments** window, select the unwanted fragments and click **Delete** above the list. You can also click **Delete All** above the list to delete all fragments. Click |image1| in the upper right corner to refresh the fragment list, as shown in :ref:`Figure 1 <obs_03_1044__fig855244105918>`.

   .. _obs_03_1044__fig855244105918:

   .. figure:: /_static/images/en-us_image_0000002683558494.png
      :alt: **Figure 1** Fragment management

      **Figure 1** Fragment management

#. In the displayed **Warning** dialog box, confirm the delete information and click **Yes**.

#. Click **Yes**.

   The **Fragments** window is displayed. You can close this window to go back to the OBS Browser+ homepage.

.. |image1| image:: /_static/images/en-us_image_0000002713278207.png
