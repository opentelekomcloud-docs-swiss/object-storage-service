:original_name: en-us_topic_0045853755.html

.. _en-us_topic_0045853755:

Configuring Static Website Hosting
==================================

You can configure static website hosting for a bucket and then use the bucket's domain name to access static websites hosted in the bucket.

It can take up to two minutes for the configuration of static website hosting to take effect.

Prerequisites
-------------

Web page files required for static website hosting have been uploaded to the specified bucket.

The static website files hosted in the bucket are accessible to anonymous users.

Static web page files in the Cold storage class have been restored. For more information, see :ref:`Restoring an Object from Cold Storage <obs_03_0320>`.

Procedure
---------

#. In the bucket list, click the bucket you want to operate to go to the **Objects** page.

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

#. In the navigation pane, choose **Basic Configurations** > **Static Website Hosting**.

#. Click **Configure Static Website Hosting**. The **Configure Static Website Hosting** dialog box is displayed.

#. Enable **Status**.

#. Set the hosting type to the current bucket. For details, see :ref:`Figure 1 <en-us_topic_0045853755__fig1131112528711>`.

   .. _en-us_topic_0045853755__fig1131112528711:

   .. figure:: /_static/images/en-us_image_0145846197.png
      :alt: **Figure 1** Configuring static website hosting

      **Figure 1** Configuring static website hosting

#. Configure the homepage and 404 error page.

   -  **Homepage**: specifies the default homepage of the static website. When OBS Console is used to configure static website hosting, only HTML web pages are supported.

      OBS only allows files such as **index.html** in the root directory of a bucket to function as the default homepage. Do not set the default homepage with a multi-level directory structure (for example, **/page/index.html**).

   -  **404 Error Page**: specifies the error page returned when an error occurs during static website access. When OBS Console is used to configure static website hosting, only HTML, JPG, PNG, BMP, and WebP files under the root directory are supported.

#. **Optional**: In **Redirection Rules**, configure redirection rules. Requests that comply with the redirection rules are redirected to the specific host or page.

   A redirection rule is compiled in the JSON or XML format. Each rule contains a **Condition** and a **Redirect**. The parameters are described in :ref:`Table 2 <en-us_topic_0045853755__table59166151447>`.

   .. _en-us_topic_0045853755__table59166151447:

   .. table:: **Table 2** Parameter description

      +-----------------------+-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Container             | Key                         | Description                                                                                                                                                                                                                                                                                                                                                       |
      +=======================+=============================+===================================================================================================================================================================================================================================================================================================================================================================+
      | Condition             | KeyPrefixEquals             | Object name prefix on which the redirection rule takes effect. When a request is sent for accessing an object, the redirection rule takes effect if the object name prefix matches the value specified for this parameter.                                                                                                                                        |
      |                       |                             |                                                                                                                                                                                                                                                                                                                                                                   |
      |                       |                             | For example, to redirect the request for object **ExamplePage.html**, set the **KeyPrefixEquals** to **ExamplePage.html**.                                                                                                                                                                                                                                        |
      +-----------------------+-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                       | HttpErrorCodeReturnedEquals | HTTP error codes upon which the redirection rule takes effect. The specified redirection is applied only when the error code returned equals the value specified for this parameter.                                                                                                                                                                              |
      |                       |                             |                                                                                                                                                                                                                                                                                                                                                                   |
      |                       |                             | For example, if you want to redirect requests to **NotFound.html** when HTTP error code 404 is returned, set **HttpErrorCodeReturnedEquals** to **404** in **Condition**, and set **ReplaceKeyWith** to **NotFound.html** in **Redirect**.                                                                                                                        |
      +-----------------------+-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Redirect              | Protocol                    | Protocol used for redirecting requests. The value can be **http** or **https**. If this parameter is not specified, the default value **http** is used.                                                                                                                                                                                                           |
      +-----------------------+-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                       | HostName                    | Host name to which the redirection is pointed. If this parameter is not specified, the request is redirected to the host from which the original request is initiated.                                                                                                                                                                                            |
      +-----------------------+-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                       | ReplaceKeyPrefixWith        | The object name prefix used in the redirection request. OBS replaces the value of **KeyPrefixEquals** with the value you specified here for **ReplaceKeyPrefixWith**.                                                                                                                                                                                             |
      |                       |                             |                                                                                                                                                                                                                                                                                                                                                                   |
      |                       |                             | For example, to redirect requests for **docs** (objects in the **docs** directory) to **documents** (objects in the **documents** directory), set **KeyPrefixEquals** to **docs** under **Condition** and **ReplaceKeyPrefixWith** to **documents** under **Redirect**. This way, requests for object **docs/a.html** will be redirected to **documents/a.html**. |
      +-----------------------+-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                       | ReplaceKeyWith              | The object name used in the redirection request. OBS replaces the entire object name in the request with the value you specified here for **ReplaceKeyWith**.                                                                                                                                                                                                     |
      |                       |                             |                                                                                                                                                                                                                                                                                                                                                                   |
      |                       |                             | For example, to redirect requests for all objects in the **docs** directory to **documents/error.html**, set **KeyPrefixEquals** to **docs** under **Condition** and **ReplaceKeyWith** to **documents/error.html** under **Redirect**. This way, requests for both objects **docs/a.html** and **docs/b.html** will be redirected to **documents/error.html**.   |
      +-----------------------+-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                       | HttpRedirectCode            | HTTP status code returned to the redirection request. The default value is **301**, indicating that requests are permanently redirected to the location specified by **Redirect**. You can also set this parameter based on your service needs.                                                                                                                   |
      +-----------------------+-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

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
