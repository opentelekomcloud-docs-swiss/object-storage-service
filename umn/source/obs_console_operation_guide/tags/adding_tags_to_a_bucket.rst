:original_name: obs_03_0331.html

.. _obs_03_0331:

Adding Tags to a Bucket
=======================

When creating a bucket, you can add tags to it. For details, see :ref:`Creating a Bucket <obs_03_0306>`. You can also add tags to a bucket after it has been created. This section describes how to add tags to an existing bucket.

Procedure
---------

#. In the bucket list, click the bucket you want to operate to go to the **Objects** page.

#. In the navigation pane, choose **Basic Configurations** > **Tagging**.

#. Click **Add Tag**. The **Add Tag** dialog box is displayed.


   .. figure:: /_static/images/en-us_image_0000001226220863.png
      :alt: **Figure 1** Add Tag

      **Figure 1** Add Tag

#. Set the key and value based on :ref:`Table 1 <obs_03_0331__table13674114016216>`.

   .. _obs_03_0331__table13674114016216:

   .. table:: **Table 1** Parameter description

      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                         |
      +===================================+=====================================================================================================================================+
      | Key                               | Specifies the key of the tag. Each tag of a bucket has a unique key. The value of the key can be self-defined or predefined by TMS. |
      |                                   |                                                                                                                                     |
      |                                   | A tag key must comply with the following naming rules:                                                                              |
      |                                   |                                                                                                                                     |
      |                                   | -  Must contain 1 to 36 characters.                                                                                                 |
      |                                   | -  Only digits, letters, underscores (_), hyphens (-) are allowed.                                                                  |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------+
      | Value                             | Specifies the value of the tag. Tags of a bucket can have repetitive or blank values.                                               |
      |                                   |                                                                                                                                     |
      |                                   | The tag value must comply with the following naming rules:                                                                          |
      |                                   |                                                                                                                                     |
      |                                   | -  Must contain 0 to 43 characters.                                                                                                 |
      |                                   | -  Only digits, letters, underscores (_), hyphens (-) are allowed.                                                                  |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------+

#. Click **OK**.

   It takes approximately 3 minutes for the tag to take effect.

Related Operations
------------------

In the tag list, click **Edit** to change the tag value or click **Delete** to remove the tag.
