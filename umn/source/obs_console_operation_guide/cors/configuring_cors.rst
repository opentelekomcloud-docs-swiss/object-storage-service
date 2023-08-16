:original_name: en-us_topic_0066036542.html

.. _en-us_topic_0066036542:

Configuring CORS
================

This section describes how to use CORS in HTML5 to implement cross-origin access.

Prerequisites
-------------

Static website hosting has been configured. For details about how to configure static website hosting, see :ref:`Configuring Static Website Hosting <en-us_topic_0045853755>`.

Procedure
---------

#. In the bucket list, click the bucket to be operated. The **Overview** page of the bucket is displayed.

#. On the right of the **Overview** page, select **CORS Rules** in the **Basic Configurations** area. The **CORS Rules** page is displayed.

   Alternatively, you can choose **Basic Configurations** > **CORS Rules** in the navigation pane.

#. Click **Create**. The **Create CORS Rule** dialog box is displayed.

   .. note::

      A bucket can have a maximum of 100 CORS rules configured.


   .. figure:: /_static/images/en-us_image_0000001180503470.png
      :alt: **Figure 1** Creating a CORS rule

      **Figure 1** Creating a CORS rule

#. In the **CORS Rule** dialog box, configure **Allowed Origin**, **Allowed Method**, **Allowed Header**, **Exposed Header**, and **Cache Duration (s)**.

   .. table:: **Table 1** Parameters in CORS rules

      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                 |
      +===================================+=============================================================================================================================================================================================+
      | Allowed Origin                    | Mandatory                                                                                                                                                                                   |
      |                                   |                                                                                                                                                                                             |
      |                                   | Requests from this origin can access the bucket.                                                                                                                                            |
      |                                   |                                                                                                                                                                                             |
      |                                   | Multiple matching rules are allowed. One rule occupies one line, and allows one wildcard character (**\***) at most. Example:                                                               |
      |                                   |                                                                                                                                                                                             |
      |                                   | .. code-block::                                                                                                                                                                             |
      |                                   |                                                                                                                                                                                             |
      |                                   |    http://rds.example.com                                                                                                                                                                   |
      |                                   |    https://*.vbs.example.com                                                                                                                                                                |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Allowed Method                    | Mandatory                                                                                                                                                                                   |
      |                                   |                                                                                                                                                                                             |
      |                                   | Specifies the acceptable operation type of buckets and objects.                                                                                                                             |
      |                                   |                                                                                                                                                                                             |
      |                                   | The methods include Get, Post, Put, Delete, and Head.                                                                                                                                       |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Allowed Header                    | Optional                                                                                                                                                                                    |
      |                                   |                                                                                                                                                                                             |
      |                                   | Specifies the allowed header of cross-origin requests.                                                                                                                                      |
      |                                   |                                                                                                                                                                                             |
      |                                   | Only CORS requests matching the allowed header are valid.                                                                                                                                   |
      |                                   |                                                                                                                                                                                             |
      |                                   | You can enter multiple allowed headers (one per line) and each line can contain one wildcard character (``*``) at most. Spaces and special characters including **&:<** are not allowed.    |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Exposed Header                    | Optional                                                                                                                                                                                    |
      |                                   |                                                                                                                                                                                             |
      |                                   | Specifies the exposed header in CORS responses, providing additional information for clients.                                                                                               |
      |                                   |                                                                                                                                                                                             |
      |                                   | By default, a browser can access only headers **Content-Length** and **Content-Type**. If the browser wants to access other headers, you need to configure those headers in this parameter. |
      |                                   |                                                                                                                                                                                             |
      |                                   | You can enter multiple exposed headers (one per line). Spaces and special characters including **\*&:<** are not allowed.                                                                   |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Cache Duration (s)                | Mandatory                                                                                                                                                                                   |
      |                                   |                                                                                                                                                                                             |
      |                                   | Specifies the duration that your browser can cache CORS responses, expressed in seconds. The default value is **100**.                                                                      |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **OK**.

   A message is displayed indicating that CORS configuration of the bucket is successful. The configuration of CORS takes effect within two minutes.

   After CORS is successfully configured, only the addresses specified in **Allowed Origin** can access a bucket in OBS using the method specified in **Allowed Method**. For example, you can configure CORS parameters of bucket **testbucket** as follows:

   -  **Allowed Origin**: **https://www.example.com**
   -  **Allowed Method**: **GET**
   -  **Allowed Header**: \*
   -  **Exposed Header**: \*
   -  **Cache Duration (s)**: **100**

   If so, OBS only allows GET requests from **https://www.example.com** to access bucket **testbucket**, without restrictions on request headers. The client can cache CORS responses for 100 seconds.
