:original_name: obs_faq_0020.html

.. _obs_faq_0020:

Does OBS Support Batch Deletion of Objects?
===========================================

The following table lists the batch deletion support for different OBS tools.

.. table:: **Table 1** Support for batch deletion by different OBS tools

   +--------------+---------------------------------------------------------------------------------------------------------------------------------------+
   | Tool         | Batch Deletion                                                                                                                        |
   +==============+=======================================================================================================================================+
   | OBS Console  | Supported. A maximum of 100 objects can be deleted at a time. If you are deleting a folder, only one folder can be deleted at a time. |
   +--------------+---------------------------------------------------------------------------------------------------------------------------------------+
   | OBS Browser+ | Supported. Files and folders can be deleted in a batch, and the number of files and folders to be deleted is not limited.             |
   +--------------+---------------------------------------------------------------------------------------------------------------------------------------+
   | APIs         | Supported. A maximum of 1,000 objects can be deleted at a time.                                                                       |
   +--------------+---------------------------------------------------------------------------------------------------------------------------------------+

.. note::

   The batch deletion performance is negatively correlated with the number of objects in a single request. When it comes to QPS, deleting *N* objects is counted as *N* operations. If a large number of objects named with prefixes in lexicographic order are deleted, lots of requests may be concentrated in a specific partition, which results in hot access. This limits the request rate in the hot partition and increases access latency.

   To address this problem, you can reduce the number of objects in a single batch deletion request, initiate more concurrent requests, and name objects with random prefixes.
