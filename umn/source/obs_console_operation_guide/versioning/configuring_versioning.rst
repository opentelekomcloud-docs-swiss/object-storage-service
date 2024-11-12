:original_name: obs_03_0327.html

.. _obs_03_0327:

Configuring Versioning
======================

Procedure
---------

#. In the bucket list, click the bucket you want to operate to go to the **Objects** page.

#. In the navigation pane, choose **Overview**.

#. In the **Basic Configurations** area, click **Versioning**.

#. Select **Enable**.


   .. figure:: /_static/images/en-us_image_0000001225982167.png
      :alt: **Figure 1** Configuring versioning

      **Figure 1** Configuring versioning

#. Click **OK** to enable versioning for the bucket.

#. Click an object to go to the object details page. On the **Versions** tab page, view all versions of the object.

.. _obs_03_0327__section29772226:

Related Operations
------------------

After versioning is configured for a bucket, you can go to the object details page, click the **Versions** tab, and then delete and download object versions, and extend the retention period of an object version.

#. In the bucket list, click the bucket you want to operate to go to the **Objects** page.
#. In the object list, click the object you want to go to the object details page.
#. On the **Versions** tab page, view all versions of the object.
#. Perform the following operations on object versions:

   a. Download a desired version of the object by clicking **Download** in the **Operation** column.

      .. note::

         If the version you want to download is in the Cold storage class, restore it first.

   b. Delete a version of the object by choosing **Delete** in the **Operation** column. If you delete the latest version, the most recent version will become the latest version.

      .. note::

         In a WORM-enabled bucket, if an object has no retention policy configured or its retention policy has expired, you can delete a desired object version on the object's **Versions** tab page. If an object version is within the retention period, it cannot be deleted.

   c. Locate the object version for which you want to extend the retention period, choose **Extend Retention Period**, and select a date. A retention period can only be extended, but not shortened.
