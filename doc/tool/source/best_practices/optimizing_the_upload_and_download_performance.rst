:original_name: obs_03_1079.html

.. _obs_03_1079:

Optimizing the Upload and Download Performance
==============================================

By default, OBS Browser+ uploads or downloads files or objects larger than 50 MB using multipart upload and download. To configure relevant parameters, choose **Settings** > **Basic Configurations**.

.. table:: **Table 1**

   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                         | Description                                                                                                                                                                                               |
   +===================================+===========================================================================================================================================================================================================+
   | Max. Number of Concurrent Tasks   | The maximum number of tasks that can run concurrently. The value ranges from 1 to 50 and the default value is **3**.                                                                                      |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Max. Concurrent Parts             | The maximum number of parts that can be concurrently uploaded or downloaded in a task. The value ranges from 1 to 50 and the default value is **3**.                                                      |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Auto select part size             | This option is selected by default, which automatically sets the size for each part based on the source file or object size.                                                                              |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Upload Part Size                  | Threshold for triggering multipart upload. If the size of the file to be uploaded is larger than the configured threshold, the file will be uploaded in multipart mode. The default value is 50 MB.       |
   |                                   |                                                                                                                                                                                                           |
   |                                   | .. note::                                                                                                                                                                                                 |
   |                                   |                                                                                                                                                                                                           |
   |                                   |    -  To configure this parameter, you must deselect **Auto select part size**.                                                                                                                           |
   |                                   |    -  This parameter value ranges from 9 MB to 5 GB.                                                                                                                                                      |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Download Part Size                | Threshold for triggering multipart download. If the size of the file to be downloaded is larger than the configured threshold, the file will be downloaded in multipart mode. The default value is 50 MB. |
   |                                   |                                                                                                                                                                                                           |
   |                                   | .. note::                                                                                                                                                                                                 |
   |                                   |                                                                                                                                                                                                           |
   |                                   |    -  To configure this parameter, you must deselect **Auto select part size**.                                                                                                                           |
   |                                   |    -  This parameter value ranges from 9 MB to 5 GB.                                                                                                                                                      |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

In most cases, multipart tasks not only speed up transfer, but also support resumable transfer of failed tasks. By default, the part size of a multipart task can be automatically adjusted by selecting **Auto select part size**. In practice, you can adjust the part size based on factors such as the file size and network conditions, to further improve upload and download performance and ensure the efficient and successful completion of tasks.

If you have a large number of **small files** (each is usually several MB) to be uploaded or downloaded, set **Max. Number of Concurrent Tasks** to a larger value for better performance. In this case, adjusting the concurrent parts allowed and the part size may be ineffective because the files are too small to reach the threshold of these parameters.

If you want to upload or download **large files**, set **Upload Part Size**, **Download Part Size**, and **Max. Concurrent Parts** to a larger value for better performance.

.. caution::

   -  Due to limiting resources, if there are too many concurrent tasks (calculated from **Max. Number of Concurrent Tasks** x **Max. Concurrent Parts**), the upload and download performance may deteriorate because of resource switchover and preemption between threads. To avoid this, adjust the corresponding parameter values based on the actual file size and network condition.
   -  If the client network is poor, you can reduce the size of parts to be uploaded or downloaded and the total number of concurrent tasks to avoid task failures caused by the network fluctuation.
