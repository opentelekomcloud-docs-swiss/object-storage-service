:original_name: en-us_topic_0066088957.html

.. _en-us_topic_0066088957:

Configuring Redirection
=======================

You can redirect all requests for a bucket to another bucket or URL by configuring redirection rules.

Prerequisites
-------------

Web page files required for static website hosting have been uploaded to the specified bucket.

The static website files hosted in the bucket are accessible to anonymous users.

Procedure
---------

#. In the bucket list, click the bucket you want to operate. The **Overview** page is displayed.

#. In the **Basic Configurations** area, click **Static Website Hosting**. The **Static Website Hosting** page is displayed.

   Alternatively, you can choose **Basic Configurations** > **Static Website Hosting** from the navigation pane on the left.

#. Click **Configure Static Website Hosting**. The **Configure Static Website Hosting** dialog box is displayed.

#. Enable it by turning on the status switch.

#. Set **Hosting By** to **Redirection**, and enter the access domain name or URL of the bucket to which requests are redirected.


   .. figure:: /_static/images/en-us_image_0000001226261557.png
      :alt: **Figure 1** Configuring redirection

      **Figure 1** Configuring redirection

#. Click **OK**.

#. In the bucket list, click the bucket to which requests for the static website are redirected.

#. (**Optional**) If the static website files in the bucket are not accessible to anonymous users, perform this step. If they are already accessible to everyone, skip this step.

   Grant the read permission for static website files to anonymous users. For details, see :ref:`Granting Anonymous Users Permission to Access Objects <obs_03_0132>`.

   If the bucket contains only static website files, configure the **Public Read** policy for the bucket so that all files in it can be accessed publicly.

   a. Choose **Permissions** > **Bucket Policies**.

   b. In the **Standard Bucket Policies** area, select the **Public Read** policy for the bucket.

   c. Click **Public Read**. For details, see :ref:`Figure 2 <en-us_topic_0066088957__en-us_topic_0045853755_fig15186794193556>`. In the confirmation dialog box that is displayed, click **Yes**.

      .. _en-us_topic_0066088957__en-us_topic_0045853755_fig15186794193556:

      .. figure:: /_static/images/en-us_image_0000001226102917.png
         :alt: **Figure 2** Configuring the public read permission

         **Figure 2** Configuring the public read permission

#. **Verification**: Input the access domain name of the bucket in the web browser and press **Enter**. The bucket or URL to which requests are redirected will be displayed.

   .. note::

      In some conditions, you may need to clear the browser cache before the expected results are displayed.
