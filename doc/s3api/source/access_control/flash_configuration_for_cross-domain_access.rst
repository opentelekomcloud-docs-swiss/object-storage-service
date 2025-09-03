:original_name: en-us_topic_0125560477.html

.. _en-us_topic_0125560477:

Flash Configuration for Cross-Domain Access
===========================================

By default, OBS system is configured to support cross-domain access using the root domain name. This allows access from all domains, so clients are likely to be attacked.

To address this issue, you can create a **crossdomain.xml** file with specific rules in the bucket for each client, and add **Security.loadPolicyFile(http://bucket.obs.example.com/crossdomain.xml)** in the file's flash code to prevent attacks.

The following is an example of the **crossdomain.xml** file:

.. code-block::

   <?xml version="1.0"?>
   <cross-domain-policy>
   <allow-access-from domain="*" to-ports="80,443" secure="false"/>
   <site-control permitted-cross-domain-policies="master-only" />
   </cross-domain-policy>

**crossdomain.xml** needs to comply with the XML syntax rules, and there is only one root node **cross-domain-policy** without any attribute. The root node can contain only the following sub-nodes: site-control, allow-access-from, allow-access-from-identity, and allow-http-request-headers-from. The following table lists description about sub-nodes.

.. table:: **Table 1**

   +-------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Sub-node                            | Description                                                                                                                                                                                                      |
   +=====================================+==================================================================================================================================================================================================================+
   | **site-control**                    | Checks the attribute value and determines whether other policy files can be loaded.                                                                                                                              |
   |                                     |                                                                                                                                                                                                                  |
   |                                     | The attribute value can be:                                                                                                                                                                                      |
   |                                     |                                                                                                                                                                                                                  |
   |                                     | **none**: **loadPolicyFile** cannot be used to load any policy file.                                                                                                                                             |
   |                                     |                                                                                                                                                                                                                  |
   |                                     | **master-only**: Only the master policy file [default] can be used.                                                                                                                                              |
   |                                     |                                                                                                                                                                                                                  |
   |                                     | **by-content-type**: Only **loadPolicyFile** can be used to load the file whose **Content-Type** is **text/x-cross-domain-policy** over HTTP/HTTPS as the cross-domainpolicy file.                               |
   |                                     |                                                                                                                                                                                                                  |
   |                                     | **by-ftp-filename**: Only **loadPolicyFile** can be used to load file **crossdomain.xml** over FTP as the cross-domain policy file.                                                                              |
   |                                     |                                                                                                                                                                                                                  |
   |                                     | **all**: **loadPolicyFile** can be used to load any file of the target domain as the cross-domain policy file.                                                                                                   |
   +-------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | **allow-access-from**               | Checks the attribute value and determines the source domain of the flash file that can access content of the domain.                                                                                             |
   |                                     |                                                                                                                                                                                                                  |
   |                                     | The attribute value can be:                                                                                                                                                                                      |
   |                                     |                                                                                                                                                                                                                  |
   |                                     | **domain**: This attribute specifies an IP address, a domain, and a wildcard domain (any domain). Only domains specified in **domain** have the permission to access content of the domain using the flash file. |
   |                                     |                                                                                                                                                                                                                  |
   |                                     | **to-ports**: Socket connection ports that can access content of the domain.                                                                                                                                     |
   |                                     |                                                                                                                                                                                                                  |
   |                                     | **secure**: Specifies whether information is transmitted through encryption.                                                                                                                                     |
   +-------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | **allow-access-from-identity**      | Allows cross-domain sources with certain certificates to access resources in this domain.                                                                                                                        |
   +-------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | **allow-http-request-headers-from** | Grants permission to a third-party domain to sent data to the domain in **http** header format.                                                                                                                  |
   |                                     |                                                                                                                                                                                                                  |
   |                                     | The attribute value can be:                                                                                                                                                                                      |
   |                                     |                                                                                                                                                                                                                  |
   |                                     | **domain**: This attribute specifies an IP address, a domain, and a wildcard domain (any domain). Only domains specified in **domain** have the permission to access content of the domain using the flash file. |
   |                                     |                                                                                                                                                                                                                  |
   |                                     | **headers**: Specifies a list of http headers separated by commas. Wildcard (``*``) can be used to indicate the http header.                                                                                     |
   |                                     |                                                                                                                                                                                                                  |
   |                                     | **secure**: Specifies whether information is transmitted through encryption.                                                                                                                                     |
   +-------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
