:original_name: en-us_topic_0045853755.html

.. _en-us_topic_0045853755:

Configuring Static Website Hosting
==================================

This section describes how to configure static website hosting for buckets and use bucket domain names to access static websites.

The static website hosting takes effect within two minutes after its configuration is complete.

Prerequisites
-------------

Web page files of the static website have been uploaded to a bucket.

The static website files hosted in the bucket are accessible to anonymous users.

Procedure
---------

#. In the bucket list, click the bucket to be operated. The **Overview** page of the bucket is displayed.

#. (**Optional**) If the static website files in the bucket are not accessible to anonymous users, perform this step to configure them to be accessible to anonymous users. If the static website files are already accessible to anonymous users, skip this step.

   Authorize anonymous users the permission to read files on the static website. For details, see :ref:`Authorizing Access Permissions to Anonymous Users <obs_03_0132>`.

   If the bucket contains only static website files, configure the **Public Read** policy for the bucket so that all files in it can be accessed publicly.

   a. Choose **Permissions** > **Bucket Policies**.

   b. In the **Standard Bucket Policies** area, select the **Public Read** policy for the bucket.

   c. Click **Public Read**. For details, see :ref:`Figure 1 <en-us_topic_0045853755__fig15186794193556>`. In the confirmation dialog box that is displayed, click **Yes**.

      .. _en-us_topic_0045853755__fig15186794193556:

      .. figure:: /_static/images/en-us_image_0000001226102917.png
         :alt: **Figure 1** Configuring the public read permission

         **Figure 1** Configuring the public read permission

#. In the **Basic Configurations** area, click the **Static Website Hosting** label. The **Static Website Hosting** page is displayed.

   Alternatively, you can choose **Basic Configurations** > **Static Website Hosting** from the navigation pane on the left.

#. Click **Configure Static Website Hosting**. The **Configure Static Website Hosting** dialog box is displayed.

#. Enable it by turning on the status switch.

#. Set **Hosting By** to **Current bucket**. For details, see :ref:`Figure 2 <en-us_topic_0045853755__fig1131112528711>`.

   .. _en-us_topic_0045853755__fig1131112528711:

   .. figure:: /_static/images/en-us_image_0000001226221521.png
      :alt: **Figure 2** Configuring static website hosting

      **Figure 2** Configuring static website hosting

#. Set the values of **Home Page** and **404 Error Page**.

   -  **Home Page**: specifies the default homepage of the static website. When OBS Console is used to configure static website hosting, only HTML web pages are supported. When APIs are used to configure static website hosting, OBS does not have such a restriction but the **Content-Type** of objects must be specified.

      OBS only allows files such as **index.html** in the root directory of a bucket to function as the default homepage. That is to say, do not set the default homepage with a multi-level directory structure (for example, **/page/index.html**).

   -  **404 Error Page**: specifies the error page returned when an error occurs during static website access. When OBS Console is used to configure static website hosting, only HTML, JPG, PNG, BMP, and WEBP files under the root directory are supported. When APIs are used to configure static website hosting, OBS does not have such a restriction but the **Content-Type** of objects must be specified.

#. **Optional**: In **Redirection Rules**, configure redirection rules. Requests that comply with the redirection rules are redirected to the specific host or page.

   A redirection rule is compiled in the JSON or XML format. Each rule contains a **Condition** and a **Redirect**. The parameters are described as follows:

   .. table:: **Table 1** Parameter description

      +-----------------------+-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Container             | Key                         | Description                                                                                                                                                                                                                                     |
      +=======================+=============================+=================================================================================================================================================================================================================================================+
      | Condition             | KeyPrefixEquals             | Object name prefix on which the redirection rule takes effect. When a request is sent for accessing an object, the redirection rule takes effect if the object name prefix matches the value specified for this parameter.                      |
      |                       |                             |                                                                                                                                                                                                                                                 |
      |                       |                             | For example, to redirect the request for object **ExamplePage.html**, set the **KeyPrefixEquals** to **ExamplePage.html**.                                                                                                                      |
      +-----------------------+-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                       | HttpErrorCodeReturnedEquals | HTTP error codes upon which the redirection rule takes effect. The specified redirection is applied only when the error code returned equals the value specified for this parameter.                                                            |
      |                       |                             |                                                                                                                                                                                                                                                 |
      |                       |                             | For example, if you want to redirect requests to **NotFound.html** when HTTP error code 404 is returned, set **HttpErrorCodeReturnedEquals** to **404** in **Condition**, and set **ReplaceKeyWith** to **NotFound.html** in **Redirect**.      |
      +-----------------------+-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Redirect              | Protocol                    | Protocol used for redirection The value can be **http** or **https**. If this parameter is not specified, the default value **http** is used.                                                                                                   |
      +-----------------------+-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                       | HostName                    | Host name to which the redirection is pointed. If this parameter is not specified, the request is redirected to the host from which the original request is initiated.                                                                          |
      +-----------------------+-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                       | ReplaceKeyPrefixWith        | Object name prefix on which the redirection rule takes effect                                                                                                                                                                                   |
      +-----------------------+-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                       | ReplaceKeyWith              | Object name on which the redirection rule takes effect                                                                                                                                                                                          |
      +-----------------------+-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                       | HttpRedirectCode            | HTTP status code returned to the redirection request. The default value is **301**, indicating that requests are permanently redirected to the location specified by **Redirect**. You can also set this parameter based on your service needs. |
      +-----------------------+-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   **Example of setting a redirection rule**

   -  Example 1: All requests for objects prefixed with **folder1/** are automatically redirected to pages prefixed with **target.html** on host **www.example.com** using HTTPS.

      .. code-block::

         [
             {
             "Condition": {
                 "KeyPrefixEquals": "folder1/"
                 },
             "Redirect":{
                 "Protocol": "https",
                 "HostName": "www.example.com",
                 "ReplaceKeyPrefixWith": "target.html"
                 }
             }
         ]

   -  Example 2: All requests for objects prefixed with **folder2/** are automatically redirected to objects prefixed with **folder/** in the same bucket.

      .. code-block::

         [
             {
             "Condition": {
                 "KeyPrefixEquals": "folder2/"
                 },
             "Redirect":{
                 "ReplaceKeyPrefixWith": "folder/"
                 }
             }
         ]

   -  Example 3: All requests for objects prefixed with **folder.html** are automatically redirected to the **folderdeleted.html** object in the same bucket.

      .. code-block::

         [
             {
             "Condition": {
                 "KeyPrefixEquals": "folder.html"
                 },
             "Redirect":{
                 "ReplaceKeyWith": "folderdeleted.html"
                 }
             }
         ]

   -  Example 4: If the HTTP status code 404 is returned, the request is automatically redirected to the page prefixed with **report-404/** on host **www.example.com**.

      For example, if you request the page **ExamplePage.html** but the HTTP 404 error is returned, the request will be redirected to the **report-404/ExamplePage.html** page on the **www.example.com**. If the 404 redirection rule is not specified, the default 404 error page configured in the previous step is returned when the HTTP 404 error occurs.

      .. code-block::

         [
             {
             "Condition": {
                 "HttpErrorCodeReturnedEquals": "404"
                 },
             "Redirect":{
                 "HostName": "www.example.com",
                 "ReplaceKeyPrefixWith": "report-404/"
                 }
             }
         ]

#. Click **OK**.

   After the static website hosting is effective in OBS, you can access the static website by using the URL provided by OBS.

   .. note::

      In some conditions, you may need to clear the browser cache before the expected results are displayed.
