:original_name: obs_03_0139.html

.. _obs_03_0139:

Can Deleted Data Be Recovered?
==============================

-  Versioning enabled for a bucket:

   -  If the **Historical Versions** button is disabled, a deleted object is not displayed in the object list. After the button is enabled, the current object version with a delete marker and the deleted object (also the historical object version) are displayed in the object list. In this case, you can click **Permanently Delete** in the **Operation** column of the current object version with a delete marker to recover the deleted object.

      .. note::

         If you delete an object from a versioning-enabled bucket, instead of deleting the object permanently, OBS inserts a delete marker, which becomes the current object version. The deleted object becomes the historical version. After that, if you enable the **Historical Versions** button above the object list, you can see the current object version with a delete marker and the deleted object that has become a historical version.

   -  If the **Historical Versions** button is enabled, you choose **More** > **Permanently Delete** in the **Operation** column of an object version other than the current one with a delete marker to permanently delete the object. The deleted object cannot be recovered.

-  If versioning is disabled for a bucket, deleted objects cannot be recovered.
