:original_name: obs_03_0331.html

.. _obs_03_0331:

Configuring Tags for a Bucket
=============================

You can add tags to a bucket when creating the bucket. For details, see :ref:`Creating a Bucket <obs_03_0306>`. Also you can add tags to a bucket after it has been created. This topic describes how to add tags to a bucket after it has been created.

Procedure
---------

#. In the bucket list, click the bucket to be operated. The **Overview** page of the bucket is displayed.

#. In the **Basic Configurations** area, click the **Tags** label. The **Tags** page is displayed.

   Alternatively, you can choose **Basic Configurations** > **Tags** in the navigation pane on the left.

#. Click **Add Tag**. The **Add Tag** dialog box is displayed.


   .. figure:: /_static/images/en-us_image_0000001226220863.png
      :alt: **Figure 1** Add Tag

      **Figure 1** Add Tag

#. Set the key and value based on :ref:`Table 1 <obs_03_0331__table4503491017244>`.

   .. _obs_03_0331__table4503491017244:

   .. table:: **Table 1** Parameter description

      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                         |
      +===================================+=====================================================================================================================================+
      | Key                               | Specifies the key of the tag. Each tag of a bucket has a unique key. The value of the key can be self-defined or predefined by TMS. |
      |                                   |                                                                                                                                     |
      |                                   | A tag key must comply with the following naming rules:                                                                              |
      |                                   |                                                                                                                                     |
      |                                   | -  Must contain 1 to 36 characters.                                                                                                 |
      |                                   | -  The value cannot start or end with a space or contain the following characters: **=*<>\\,|/**                                    |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------+
      | Value                             | Specifies the value of the tag. Tags of a bucket can have repetitive or blank values.                                               |
      |                                   |                                                                                                                                     |
      |                                   | The tag value must comply with the following naming rules:                                                                          |
      |                                   |                                                                                                                                     |
      |                                   | -  It ranges from 0 to 43 characters.                                                                                               |
      |                                   | -  Cannot contain the following characters: ``=*<>\,|/``                                                                            |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------+

#. Click **OK**.

   It takes approximately 3 minutes for the tag to take effect.

Related Operations
------------------

To modify the tag configuration, edit **Value** of the tag. You can also click **Delete** next to a tag to delete the tag.
