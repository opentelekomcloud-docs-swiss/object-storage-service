:original_name: obs_03_0344.html

.. _obs_03_0344:

OBS Console Couldn't Be Opened in Internet Explorer 9
=====================================================

Question
--------

Why OBS Console cannot be opened in Internet Explorer 9, even if the address of OBS Console can be pinged?

Answer
------

Confirm whether **Use SSL** and **Use TLS** are selected in **Internet Options**. If not, do as follows and try again:

#. Open Internet Explorer 9.

#. Click **Tools** in the upper right corner and choose **Internet Options** > **Advanced**. Then select **Use SSL 2.0**, **Use SSL 3.0**, **Use TLS 1.0**, **Use TLS 1.1**, and **Use TLS 1.2**, as shown in :ref:`Figure 1 <obs_03_0344__fig3632690019428>`.

   .. _obs_03_0344__fig3632690019428:

   .. figure:: /_static/images/en-us_image_0129288861.png
      :alt: **Figure 1** Internet Options

      **Figure 1** Internet Options

#. Click **OK**.
