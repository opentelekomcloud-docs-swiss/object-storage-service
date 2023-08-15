:original_name: obs_03_1034.html

.. _obs_03_1034:

How Can I Locate Common Network Errors?
=======================================

Accessing OBS using OBS Browser+ is usually affected by your network quality. If there are network fluctuations, your access may time out or your upload/download will fail. If such faults occur, an error message will be displayed in the upper right corner or on the task management page. You can also view log files **basic.log** and **obssdk.log** to check whether the network is abnormal. To obtain the log path, choose **Settings** > **Basic Configurations** > **Log Path**. Common errors include **connect ETIMEDOUT** and **premature end of Content-Length delimiter message body (expected:** *xxxxx*\ **, actual:**\ *xxxxxx*\ **)**.

Solutions:

#. Ping the bucket domain name (*bucketName.domain name*) to check the network connectivity. If the network is disconnected, rectify your local network first.
#. If the network is normal, but basic operations such as listing and bucket creation occasionally time out, it may be caused by network fluctuations. In this case, try your operation again.
#. **premature end of Content-Length delimiter message body (expected:** *xxxxx*\ **, actual:**\ *xxxxxx*\ **)** is a common error during upload and download operations, because there are occasional network fluctuations. OBS Browser+ supports resumable transfer, so you can retry the upload and download tasks that fail due to network errors. If upload and download tasks fail frequently due to network errors, reduce the value of **Max. Number of Concurrent Tasks**.

   .. note::

      -  If you want to further analyze the cause of upload or download failures, capture packets on OBS Browser+ to check whether there is packet loss or other network problems on the entire network link. To capture packets on OBS Browser+, you are advised to select **Other object storage services** for **Service** during the login and manually specify an endpoint starting with **http://**, because network packets will be encrypted for transmission if the HTTPS protocol is used.
