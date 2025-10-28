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

      +-----------------------------------+------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                    |
      +===================================+================================================================================================+
      | Key                               | Specifies the key of the tag. The value of the key can be self-defined or predefined by TMS.   |
      |                                   |                                                                                                |
      |                                   | Tag key constraints:                                                                           |
      |                                   |                                                                                                |
      |                                   | -  If there are multiple tags specified for an object, each tag key must be unique.            |
      |                                   | -  A tag key must contain 1 to 36 characters and be case sensitive.                            |
      |                                   | -  A tag key can't start or end with a space or contain the following characters: ``,/|<>=*\`` |
      +-----------------------------------+------------------------------------------------------------------------------------------------+
      | Value                             | Specifies the value of the tag. Tags of a bucket can have repetitive or blank values.          |
      |                                   |                                                                                                |
      |                                   | Tag value constraints:                                                                         |
      |                                   |                                                                                                |
      |                                   | -  A tag value can contain 0 to 43 characters and must be case sensitive.                      |
      |                                   | -  A tag value can't contain the following characters: ``,/|<>=*\``                            |
      +-----------------------------------+------------------------------------------------------------------------------------------------+

#. Click **OK**.

   It takes approximately 3 minutes for the tag to take effect.

Related Operations
------------------

In the tag list, click **Edit** to change the tag value or click **Delete** to remove the tag.
