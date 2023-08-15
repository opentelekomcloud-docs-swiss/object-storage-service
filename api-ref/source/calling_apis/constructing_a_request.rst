:original_name: obs_04_0007.html

.. _obs_04_0007:

Constructing a Request
======================

This section describes the structure of a REST API request.

Request URI
-----------

OBS uses URI to locate specific buckets, objects, and their parameters. Use URIs when you want to operate resources.

The following provides a common URI format. The parameters in square brackets [ ] are optional.

**protocol://[\ bucket.\ ]\ domain[:port][/object][?param]**

.. table:: **Table 1** URI parameters

   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Parameter             | Description                                                                                                                                                                                                                                                                                                                   | Mandatory             |
   +=======================+===============================================================================================================================================================================================================================================================================================================================+=======================+
   | protocol              | Protocol used for sending requests, which can be either HTTP or HTTPS. HTTPS is a protocol that ensures secure access to resources. OBS supports both HTTP and HTTPS.                                                                                                                                                         | Yes                   |
   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | bucket                | Resource path of a bucket, identifying only one bucket in OBS                                                                                                                                                                                                                                                                 | No                    |
   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | domain                | Domain name or IP address of the server for saving resources                                                                                                                                                                                                                                                                  | Yes                   |
   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | port                  | Port enabled for protocols used for sending requests. The value varies with software server deployment. If no port number is specified, the protocol uses the default value. Each transmission protocol has its default port number. For example, HTTP uses port number **80** and HTTPS uses port number **443** by default. | No                    |
   |                       |                                                                                                                                                                                                                                                                                                                               |                       |
   |                       | In OBS, HTTP port number is **80** and that of HTTPS is **443**.                                                                                                                                                                                                                                                              |                       |
   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | object                | An object path used in the request                                                                                                                                                                                                                                                                                            | No                    |
   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | param                 | A specific resource contained by a bucket or object. Default value of this parameter indicates that the bucket or object itself is obtained.                                                                                                                                                                                  | No                    |
   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

.. important::

   All API requests except those for the bucket list must contain the bucket name. Based on the DNS resolution performance and reliability, OBS requires that the bucket name must be placed in front of the **domain** when a request carrying a bucket name is constructed to form a third-level domain name, also mentioned as virtual hosting access domain name.

   For example, you have a bucket named **test-bucket** in the **a1** region, and you want to access the ACL of an object named **test-object** in the bucket. The correct URL is **https://test-bucket.obs.a1.example.com/test-object?acl**.

Request Method
--------------

HTTP methods, which are also called operations or actions, specify the type of operations that you are requesting.

.. table:: **Table 2** HTTP request methods supported by the OBS

   +---------+-----------------------------------------------------------------------------------------------------------------------------------------+
   | Method  | Description                                                                                                                             |
   +=========+=========================================================================================================================================+
   | GET     | Requests the server to return a specific resource, for example, a bucket list or object.                                                |
   +---------+-----------------------------------------------------------------------------------------------------------------------------------------+
   | PUT     | Requests the server to update a specific resource, for example, creating a bucket or uploading an object.                               |
   +---------+-----------------------------------------------------------------------------------------------------------------------------------------+
   | POST    | Requests the server to add a resource or perform a special operation, for example, part uploading or merging.                           |
   +---------+-----------------------------------------------------------------------------------------------------------------------------------------+
   | DELETE  | Requests the server to delete specified resources, for example, an object.                                                              |
   +---------+-----------------------------------------------------------------------------------------------------------------------------------------+
   | HEAD    | Requests the server to return the digest of a specific resource, for example, object metadata.                                          |
   +---------+-----------------------------------------------------------------------------------------------------------------------------------------+
   | OPTIONS | The request server checks whether the user has the operation permission for a resource. The CORS needs to be configured for the bucket. |
   +---------+-----------------------------------------------------------------------------------------------------------------------------------------+

Request Headers
---------------

Refers to optional and additional request fields, for example a field required by a specific URI or HTTP method. For details about the fields of common request headers, see :ref:`Table 3 <obs_04_0007__table25197309>`.

.. _obs_04_0007__table25197309:

.. table:: **Table 3** Common request headers

   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------+------------------------+
   | Header                | Description                                                                                                                   | Mandatory              |
   +=======================+===============================================================================================================================+========================+
   | Authorization         | Signature information contained in a request message                                                                          | Conditionally required |
   |                       |                                                                                                                               |                        |
   |                       | Type: string                                                                                                                  |                        |
   |                       |                                                                                                                               |                        |
   |                       | No default value.                                                                                                             |                        |
   |                       |                                                                                                                               |                        |
   |                       | Conditional: optional for anonymous requests and required for other requests.                                                 |                        |
   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------+------------------------+
   | Content-Length        | The message length (excluding headers) defined in RFC 2616                                                                    | Conditionally required |
   |                       |                                                                                                                               |                        |
   |                       | Type: string                                                                                                                  |                        |
   |                       |                                                                                                                               |                        |
   |                       | No default value.                                                                                                             |                        |
   |                       |                                                                                                                               |                        |
   |                       | Conditional: required for PUT requests and those requests that load XML content.                                              |                        |
   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------+------------------------+
   | Content-Type          | The content type of the requested resource, for example, **text**/**plain**                                                   | No                     |
   |                       |                                                                                                                               |                        |
   |                       | Type: string                                                                                                                  |                        |
   |                       |                                                                                                                               |                        |
   |                       | No default value.                                                                                                             |                        |
   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------+------------------------+
   | Date                  | Time when a request is initiated, for example, **Wed, 27 Jun 2018 13:39:15 +0000**.                                           | Conditionally required |
   |                       |                                                                                                                               |                        |
   |                       | Type: string                                                                                                                  |                        |
   |                       |                                                                                                                               |                        |
   |                       | No default value.                                                                                                             |                        |
   |                       |                                                                                                                               |                        |
   |                       | Conditional: optional for anonymous requests or those requests containing header **x-obs-date**, required for other requests. |                        |
   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------+------------------------+
   | Host                  | The host address. For example, **bucketname.obs.\ region.example.com**.                                                       | Yes                    |
   |                       |                                                                                                                               |                        |
   |                       | Type: string                                                                                                                  |                        |
   |                       |                                                                                                                               |                        |
   |                       | No default value.                                                                                                             |                        |
   +-----------------------+-------------------------------------------------------------------------------------------------------------------------------+------------------------+

(Optional) Request Body
-----------------------

A request body is generally sent in a structured format (for example, JSON or XML). It corresponds to **Content-Type** in the request header and is used to transfer content other than the request header. If the request body contains Chinese characters, these characters must be coded in UTF-8.

The request body varies according to the APIs. Certain APIs do not require the request body, such as the GET and DELETE APIs.

Sending a Request
-----------------

There are two methods to initiate requests based on the constructed request messages:

-  cURL

   cURL is a command-line tool used to perform URL operations and transmit information. cURL acts as an HTTP client that can send HTTP requests to the server and receive response messages. cURL is applicable to API debugging. For more information about cURL, visit https://curl.haxx.se/. cURL cannot calculate signatures. When cURL is used, only anonymous public OBS resources can be accessed.

-  Coding

   You can use code to make API calls, and to assemble, send, and process request messages.
