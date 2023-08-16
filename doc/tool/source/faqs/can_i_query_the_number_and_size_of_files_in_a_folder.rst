:original_name: obs_03_1038.html

.. _obs_03_1038:

Can I Query the Number and Size of Files in a Folder?
=====================================================

Take Linux OS as an example. Run the **./obsutil ls obs://bucket-test/test/ -du -limit=0** command to query the size of the **test** folder in bucket **bucket-test**.

.. code-block::

   ./obsutil ls obs://bucket-test/test/ -du -limit=0

   Start at 2023-03-16 06:40:18.2773873 +0000 UTC

   Listing objects .

   Remove the -du parameter to view more information
   [DU] Total prefix [test/] size: 990.85MB
