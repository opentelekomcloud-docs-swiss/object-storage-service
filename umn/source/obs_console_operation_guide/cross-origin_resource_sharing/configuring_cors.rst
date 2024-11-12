:original_name: en-us_topic_0066036542.html

.. _en-us_topic_0066036542:

Configuring CORS
================

This section describes how to use CORS in HTML5 to implement cross-origin access.

Prerequisites
-------------

Static website hosting has been configured. For details, see :ref:`Configuring Static Website Hosting <en-us_topic_0045853755>`.

Procedure
---------

#. In the bucket list, click the bucket you want to operate to go to the **Objects** page.

#. In the navigation pane, choose **Overview**.

#. In the **Basic Configurations** area, click **CORS Rules**. The **CORS Rules** page is displayed.

   Alternatively, you can choose **Basic Configurations** > **CORS Rules** in the navigation pane.

#. Click **Create**. The **Create CORS Rule** dialog box is displayed.

   .. note::

      A bucket can have a maximum of 100 CORS rules configured.


   .. figure:: /_static/images/en-us_image_0000001180503470.png
      :alt: **Figure 1** Creating a CORS rule

      **Figure 1** Creating a CORS rule

#. In the **CORS Rule** dialog box, configure **Allowed Origin**, **Allowed Method**, **Allowed Header**, **Exposed Header**, and **Cache Duration (s)**.

   .. table:: **Table 1** Parameters in CORS rules

      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                              |
      +===================================+==========================================================================================================================================================================================+
      | Allowed Origin                    | Mandatory                                                                                                                                                                                |
      |                                   |                                                                                                                                                                                          |
      |                                   | Specifies the origins from which requests can access the bucket.                                                                                                                         |
      |                                   |                                                                                                                                                                                          |
      |                                   | Multiple matching rules are allowed. One rule occupies one line, and allows one wildcard character (**\***) at most. An example is given as follows:                                     |
      |                                   |                                                                                                                                                                                          |
      |                                   | .. code-block::                                                                                                                                                                          |
      |                                   |                                                                                                                                                                                          |
      |                                   |    http://rds.example.com                                                                                                                                                                |
      |                                   |    https://*.vbs.example.com                                                                                                                                                             |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Allowed Method                    | Mandatory                                                                                                                                                                                |
      |                                   |                                                                                                                                                                                          |
      |                                   | Specifies the allowed request methods for buckets and objects.                                                                                                                           |
      |                                   |                                                                                                                                                                                          |
      |                                   | The methods include Get, Post, Put, Delete, and Head.                                                                                                                                    |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Allowed Header                    | Optional                                                                                                                                                                                 |
      |                                   |                                                                                                                                                                                          |
      |                                   | Specifies the allowed headers in cross-origin requests.                                                                                                                                  |
      |                                   |                                                                                                                                                                                          |
      |                                   | Only CORS requests matching the allowed headers are valid.                                                                                                                               |
      |                                   |                                                                                                                                                                                          |
      |                                   | You can enter multiple allowed headers (one per line) and each line can contain one wildcard character (``*``) at most. Spaces and special characters including **&:<** are not allowed. |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Exposed Header                    | Optional                                                                                                                                                                                 |
      |                                   |                                                                                                                                                                                          |
      |                                   | Specifies the exposed headers in CORS responses, providing additional information for clients.                                                                                           |
      |                                   |                                                                                                                                                                                          |
      |                                   | By default, a browser can access only headers **Content-Length** and **Content-Type**. If the browser wants to access other headers, you need to configure them in this parameter.       |
      |                                   |                                                                                                                                                                                          |
      |                                   | You can enter multiple exposed headers (one per line). Spaces and special characters including **\*&:<** are not allowed.                                                                |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Cache Duration (s)                | Mandatory                                                                                                                                                                                |
      |                                   |                                                                                                                                                                                          |
      |                                   | Specifies the duration that your browser can cache CORS responses, expressed in seconds. The default value is **100**.                                                                   |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **OK**.

   Message "The CORS rule created successfully." is displayed. The CORS configuration will take effect within two minutes.

   Then, only the addresses specified in **Allowed Origin** can access the OBS bucket over the methods specified in **Allowed Method**. Suppose you need to configure a CORS rule for bucket **testbucket** and you set **Allowed Origin** to **https://www.example.com**, **Allowed Method** to **GET**, **Allowed Header** and **Exposed Header** both to **\***, and **Cache Duration (s)** to **100**. Then, only GET requests from **https://www.example.com** are allowed to access bucket **testbucket**. In addition, there are no limits put on headers in the requests, and the client where the requests are from can cache the CORS response for 100 seconds.
