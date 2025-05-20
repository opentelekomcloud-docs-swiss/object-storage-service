:original_name: obs_03_0313.html

.. _obs_03_0313:

Searching for a Bucket
======================

On OBS Console, you can search for buckets by bucket name, storage class, and region.

.. note::

   Currently, bucket search by tag is not supported.

Procedure
---------

#. Click the search box above the bucket list, select **Bucket Name**, **Storage Class**, or **Region** from the level-1 drop-down list, and then the option you need from the corresponding level-2 drop-down list. Alternatively, after selecting an option from the level-1 drop-down list, you can enter a keyword in the search box and then select what you want from the level-2 drop-down list.

   For example, if you want to search for bucket **test**, click the search box, select **Bucket Name** and then **test**. Alternatively, after selecting **Bucket Name**, enter **test** in the search box, and all buckets whose names contain **test** are displayed in the level-2 drop-down list. Then, select **test** and click **OK**.


   .. figure:: /_static/images/en-us_image_0000002136379984.png
      :alt: **Figure 1** Searching for buckets

      **Figure 1** Searching for buckets

   .. note::

      -  You can search for buckets based on combinations of different filter criteria.

         -  If the filter criteria are of different types, they are in intersection logic.
         -  If the filter criteria are of the same type, they are in union logic.

      -  After a keyword is entered in the search box, all buckets whose name, storage class, or region contains the specified keyword are displayed in the drop-down list. Click the option you want. Then, all the buckets meeting the search criteria are displayed in the bucket list.

#. Enter a keyword in the search box and press **Enter**.

   All buckets whose name, storage class, or region contains the searched keyword will be displayed in the bucket list.

   For example, if you enter **test** in the search box and press **Enter**, all buckets whose name, storage class, or region contains keyword **test** are displayed in the bucket list.


   .. figure:: /_static/images/en-us_image_0000002112749382.png
      :alt: **Figure 2** Searching for buckets

      **Figure 2** Searching for buckets

Related Operations
------------------

In the bucket list, click |image1| next to the bucket name, storage class, region, used capacity, number of objects, or creation time to sort buckets.

.. |image1| image:: /_static/images/en-us_image_0000002112750646.png
