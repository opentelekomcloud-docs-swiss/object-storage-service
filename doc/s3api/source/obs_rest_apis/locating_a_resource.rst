:original_name: en-us_topic_0125560479.html

.. _en-us_topic_0125560479:

Locating a Resource
===================

In REST, specific network information or data on a network is represented by a resource, which is identified with a uniform resource identifier (URI). Clients on a network can locate resources using unified resource locator (URL).

In OBS, a resource can be a bucket, object, or specific resource related to a bucket or object. These resources are identified by a URL and can be operated after requests are sent using the URL.

The following provides a common URL format. The parameters in brackets ([ ]) are optional.

**protocol://[\ bucket.\ ]\ domain[:port][/object][?param]**

:ref:`Table 1 <en-us_topic_0125560479__table6854763>` describes URL parameters.

.. _en-us_topic_0125560479__table6854763:

.. table:: **Table 1** URL parameters

   +-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Parameter             | Description                                                                                                                                                                                                                                                                                                                                                               | Remarks               |
   +=======================+===========================================================================================================================================================================================================================================================================================================================================================================+=======================+
   | protocol              | Indicates the protocol used for sending requests. Available values are HTTP and HTTPS.                                                                                                                                                                                                                                                                                    | Mandatory             |
   |                       |                                                                                                                                                                                                                                                                                                                                                                           |                       |
   |                       | You can specify HTTPS to ensure secure access to resources.                                                                                                                                                                                                                                                                                                               |                       |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | bucket                | Indicates the path of a bucket. Each path identifies a unique bucket in OBS.                                                                                                                                                                                                                                                                                              | Optional              |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | domain                | Domain name or IP address of the server for saving resources.                                                                                                                                                                                                                                                                                                             | Mandatory             |
   |                       |                                                                                                                                                                                                                                                                                                                                                                           |                       |
   |                       | .. important::                                                                                                                                                                                                                                                                                                                                                            |                       |
   |                       |                                                                                                                                                                                                                                                                                                                                                                           |                       |
   |                       |    NOTICE:                                                                                                                                                                                                                                                                                                                                                                |                       |
   |                       |    The name of the host in this document is used as an example. Please refer to the actual information when accessing OBS. Obtain this value from `Regions and Endpoints <https://docs.sc.otc.t-systems.com/en-us/endpoint/index.html>`__.                                                                                                                                |                       |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | port                  | Indicates the port enabled for protocols used for sending requests. The value varies with software server deployment. If the value is not specified, default ports are enabled. Normally, ports **80** and **443** are enabled by default for HTTP and HTTPS, respectively. In the OBS, ports **80** and **443** are enabled by default for HTTP and HTTPS, respectively. | Optional              |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | object                | Indicates the path of an object.                                                                                                                                                                                                                                                                                                                                          | Optional              |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | param                 | Indicates the specific resource related to a bucket or object. If this parameter is not specified, the bucket or object itself is operated.                                                                                                                                                                                                                               | Optional              |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

.. important::

   The recommended protocol is HTTPS, because HTTP security is inefficient.

   HTTPS supports TLS1.1 and TLS1.2, but not TLS1.0.

Basic Concepts Involved in Regions and Domain Name-based Access
---------------------------------------------------------------

The following table describes the concepts involved in regions and domain name-based access, for example, global domain name.

.. table:: **Table 2** Basic concepts

   +-----------------------+----------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Concept               | Example                                                  | Description                                                                                                                                                            |
   +=======================+==========================================================+========================================================================================================================================================================+
   | Global domain name    | obs.example.com                                          | Unique global domain name of the multi-region cluster. The domain name serves as the unified access point of OBS in the cluster.                                       |
   +-----------------------+----------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Region type           | Default region                                           | Regions are divided into the default region and non-default region. There is only one default region in a multi-region cluster. Other regions are non-default regions. |
   +-----------------------+----------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Region name           | region2                                                  | Name of the default region or a non-default region.                                                                                                                    |
   +-----------------------+----------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Region domain name    | region2.example.com                                      | Each region can have a domain name, which serves as the access point of OBS in the region.                                                                             |
   +-----------------------+----------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Virtual hosting style | mybucket.region2.example.com or mybucket.obs.example.com | The virtual hosting style is a style where buckets are accessed as hosts.                                                                                              |
   +-----------------------+----------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

In cross-region interaction, requests may be redirected. The system will handle all requests from client, but not all of the requests will be recorded in metering file. (eg. 301 redirect request.)

It does not incur re-metering problems. (If users access the global firstly and then jump to a local bucket, there is only one Charging Data Record.)

OBS supports virtual hosting-style access to all regions.

If you want to use virtual hosting-style access, the correct URI is **http://mybucket.region2.example.com** or **http://mybucket.obs.example.com**.
