:original_name: obs_03_0333.html

.. _obs_03_0333:

Application Example: Configuring SMN-Enabled Event Notification
===============================================================

Background Information
----------------------

An enterprise has a large number of files to archive but it does not want to cost much on storage resources. Therefore, the enterprise subscribes to OBS for storing the files and expects that every operation performed on OBS can trigger an event notification, which is sent to an employee of the company by email.

Procedure
---------

#. Log in to OBS Console as an enterprise user.

#. .. _obs_03_0333__li29947515:

   Create a bucket.

   Click **Create Bucket** on the upper right corner of the page. Select **Region**, enter the bucket name, and click **Create Now**.


   .. figure:: /_static/images/en-us_image_0000001226220995.png
      :alt: **Figure 1** Creating a bucket

      **Figure 1** Creating a bucket

#. .. _obs_03_0333__li44157757145057:

   Create a folder.

   Click the bucket created in :ref:`Step 2 <obs_03_0333__li29947515>` to go to the **Overview** page. Choose **Objects** > **Create Folder**, enter the folder name, and click **OK**. For details, see :ref:`Figure 2 <obs_03_0333__fig28070790193136>`. In the following example, **SMN** is the folder name.

   .. _obs_03_0333__fig28070790193136:

   .. figure:: /_static/images/en-us_image_0000001180502786.png
      :alt: **Figure 2** Creating a folder

      **Figure 2** Creating a folder

#. In the upper left corner of the page, click |image1| and choose **Simple Message Notification**. On the displayed SMN page, create a topic.

   In the following example, **TestTopic** is the SMN topic and the notifications are sent via email.

   Use SMN to create a notification topic for OBS as follows:

   a. Create an SMN topic.
   b. Add subscription.
   c. Modify the topic policy. Select **OBS** under **Services that can publish messages** on the **Modify Topic Policy** page.

   For details, see :ref:`Table 1 <en-us_topic_0066088963__aobs_console_0039_mmccppss_table01>`.

#. Go back to OBS Console.

#. Configure an event notification rule.

   a. In the bucket list, click the bucket that you have created in :ref:`2 <obs_03_0333__li29947515>`.

   b. In the navigation pane on the left, choose **Basic Configurations** > **Event Notification**. The **Event Notification** page is displayed.

   c. Click **Create**. The **Create Event Notification** dialog box is displayed.

   d. Configure the parameters. See :ref:`Figure 3 <obs_03_0333__fig377201314360>` for details. For an enterprise account, the specified user in the account will be notified about all specified operations on the **SMN** folder in the **testbucket** bucket. For details about parameters, see :ref:`Table 1 <en-us_topic_0066088963__aobs_console_0039_mmccppss_table01>`.

      .. note::

         -  A folder path ends with a slash (/). Therefore, if you want to configure the event notification for operations on folders and you need to filter folders by suffix, the suffix must also end with a slash (/).
         -  If neither the **Prefix** nor the **Suffix** is configured, the event notification rule applies to all objects in the bucket.

      .. _obs_03_0333__fig377201314360:

      .. figure:: /_static/images/en-us_image_0000001226261025.png
         :alt: **Figure 3** Adding an event notification rule

         **Figure 3** Adding an event notification rule

Verification
------------

#. Log in to OBS Console as an enterprise user.

#. .. _obs_03_0333__li38214839153354:

   Upload the **test.txt** file to the folder created in :ref:`Step 3 <obs_03_0333__li44157757145057>`.

   After the file is uploaded, an employee receives an email. Keyword **ObjectCreated:Post** in the email indicates that the object is successfully uploaded.

#. Delete the **test.txt** file uploaded in :ref:`Step 2 <obs_03_0333__li38214839153354>`.

   After the file is successfully deleted, an employee will receive an email. Keyword **ObjectRemoved:Delete** in the email indicates that the object is successfully deleted.

.. |image1| image:: /_static/images/en-us_image_0000001196392484.png
