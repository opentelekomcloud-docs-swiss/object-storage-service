:original_name: en-us_topic_0066088957.html

.. _en-us_topic_0066088957:

Configuring Redirection
=======================

You can redirect all requests for a bucket to another bucket or URL by configuring redirection rules.

Prerequisites
-------------

Web page files required for static website hosting have been uploaded to the specified bucket.

The static website files hosted in the bucket are accessible to anonymous users.

Static web page files in the Cold storage class have been restored. For more information, see :ref:`Restoring an Object from Cold Storage <obs_03_0320>`.

Procedure
---------

#. In the bucket list, click the bucket you want to operate to go to the **Objects** page.

#. In the navigation pane, choose **Basic Configurations** > **Static Website Hosting**.

#. Click **Configure Static Website Hosting**. The **Configure Static Website Hosting** dialog box is displayed.

#. Enable **Status**.

#. Set **Hosting By** to **Redirection**, and enter the access domain name or URL of the bucket to which requests are redirected.


   .. figure:: /_static/images/en-us_image_0000002134970296.png
      :alt: **Figure 1** Configuring redirection

      **Figure 1** Configuring redirection

#. Click **OK**.

#. In the bucket list, click the bucket to which requests for the static website are redirected.

#. (**Optional**) If the static website files in the bucket are not accessible to everyone, perform this step. If they are already accessible to everyone, skip this step.

   To grant required permissions, see :ref:`Granting Anonymous Users Permission to Access Objects <obs_03_0132>`.

   If the bucket contains only static website files, configure the **Object Read-Only** policy for the bucket, so that all files in it are publicly accessible.

   a. Choose **Permissions** > **Bucket Policies**.
   b. Click **Create**.
   c. Configure bucket policy information.

      .. table:: **Table 1** Parameters for configuring a public read policy

         +-----------------------+-----------------------+------------------------------------------------------------------------------+
         | Parameter             |                       | Description                                                                  |
         +=======================+=======================+==============================================================================+
         | Configuration method  |                       | **Visual Editor** and **JSON** are available. Choose **Visual Editor** here. |
         +-----------------------+-----------------------+------------------------------------------------------------------------------+
         | Policy Name           |                       | Enter a custom policy name.                                                  |
         +-----------------------+-----------------------+------------------------------------------------------------------------------+
         | Policy content        | Effect                | Select **Allow**.                                                            |
         +-----------------------+-----------------------+------------------------------------------------------------------------------+
         |                       | Principals            | Select **All accounts**.                                                     |
         +-----------------------+-----------------------+------------------------------------------------------------------------------+
         |                       | Resources             | -  Select **Specified objects**.                                             |
         |                       |                       | -  Set the resource path to **\*** (indicating all objects in the bucket).   |
         +-----------------------+-----------------------+------------------------------------------------------------------------------+
         |                       | Actions               | -  Choose **Use a template**.                                                |
         |                       |                       | -  Select **Object Read-Only**.                                              |
         +-----------------------+-----------------------+------------------------------------------------------------------------------+

   d. Click **Create**. The bucket policy is created.

#. **Verification**: Input the access domain name of the bucket in the web browser and press **Enter**. The bucket or URL to which requests are redirected will be displayed.

   .. note::

      In some conditions, you may need to clear the browser cache before the expected results are displayed.
