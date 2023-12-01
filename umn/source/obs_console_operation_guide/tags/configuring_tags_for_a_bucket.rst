:original_name: obs_03_0331.html

.. _obs_03_0331:

Configuring Tags for a Bucket
=============================

When creating a bucket, you can add tags to it. For details, see :ref:`Creating a Bucket <obs_03_0306>`. You can also add tags to a bucket after it has been created. This topic describes how to add tags to an existing bucket.

Procedure
---------

#. In the bucket list, click the bucket you want to operate. The **Overview** page is displayed.

#. In the **Basic Configurations** area, click **Tags**.

   Alternatively, you can choose **Basic Configurations** > **Tags** in the navigation pane.

#. Click **Add Tag**. The **Add Tag** dialog box is displayed.


   .. figure:: /_static/images/en-us_image_0000001226220863.png
      :alt: **Figure 1** Add Tag

      **Figure 1** Add Tag

#. Set the key and value based on :ref:`Table 1 <obs_03_0331__table4503491017244>`.

   .. _obs_03_0331__table4503491017244:

   .. table:: **Table 1** Parameter description

      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                             |
      +===================================+=========================================================================================================================+
      | Tag key                           | Key of a tag. Tag keys for the same bucket must be unique. You can customize tags or select the ones predefined on TMS. |
      |                                   |                                                                                                                         |
      |                                   | A tag key:                                                                                                              |
      |                                   |                                                                                                                         |
      |                                   | -  Must contain 1 to 36 characters and be case sensitive.                                                               |
      |                                   | -  Cannot start or end with a space or contain the following characters: ``=*<>\,|/``                                   |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------+
      | Tag value                         | Value of a tag. A tag value can be repetitive or left blank.                                                            |
      |                                   |                                                                                                                         |
      |                                   | A tag value:                                                                                                            |
      |                                   |                                                                                                                         |
      |                                   | -  Can contain 0 to 43 characters and must be case sensitive.                                                           |
      |                                   | -  Cannot contain the following characters: ``=*<>\,|/``                                                                |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------+

#. Click **OK**.

   It takes approximately 3 minutes for the tag to take effect.

Related Operations
------------------

In the tag list, click **Edit** to change the tag value or click **Delete** to remove the tag.
