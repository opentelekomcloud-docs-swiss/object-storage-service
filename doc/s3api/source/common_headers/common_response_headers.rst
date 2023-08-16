:original_name: en-us_topic_0125560484.html

.. _en-us_topic_0125560484:

Common Response Headers
=======================

:ref:`Table 1 <en-us_topic_0125560484__table33358910>` describes headers common to OBS REST responses.

.. _en-us_topic_0125560484__table33358910:

.. table:: **Table 1** Common response headers

   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | Header                            | Description                                                                                                                        |
   +===================================+====================================================================================================================================+
   | Content-Length                    | Indicates the length (in bytes) of a response body.                                                                                |
   |                                   |                                                                                                                                    |
   |                                   | Type: String                                                                                                                       |
   |                                   |                                                                                                                                    |
   |                                   | Default: None                                                                                                                      |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | Connection                        | Indicates whether the connection to the server is opened or closed.                                                                |
   |                                   |                                                                                                                                    |
   |                                   | Type: String.                                                                                                                      |
   |                                   |                                                                                                                                    |
   |                                   | Valid values: **keep-alive \| close**                                                                                              |
   |                                   |                                                                                                                                    |
   |                                   | Default: None                                                                                                                      |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | Date                              | Indicates the date and time at which OBS responds to a request.                                                                    |
   |                                   |                                                                                                                                    |
   |                                   | Type: String                                                                                                                       |
   |                                   |                                                                                                                                    |
   |                                   | Default: None                                                                                                                      |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | ETag                              | Indicates the hash value of an object. The entity tag (ETag) only reflects changes to the contents of an object, not its metadata. |
   |                                   |                                                                                                                                    |
   |                                   | Type: String                                                                                                                       |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | x-amz-id-2                        | Indicates a special token that helps OBS troubleshoot faults.                                                                      |
   |                                   |                                                                                                                                    |
   |                                   | Type: String                                                                                                                       |
   |                                   |                                                                                                                                    |
   |                                   | Default: None                                                                                                                      |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | x-amz-request-id                  | Indicates the value created by OBS to uniquely identify a request. OBS uses this value to troubleshoot faults.                     |
   |                                   |                                                                                                                                    |
   |                                   | Type: String                                                                                                                       |
   |                                   |                                                                                                                                    |
   |                                   | Default: None                                                                                                                      |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | x-reserved                        | Indicates the copyright.                                                                                                           |
   |                                   |                                                                                                                                    |
   |                                   | Type: String                                                                                                                       |
   |                                   |                                                                                                                                    |
   |                                   | Default: None                                                                                                                      |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------+
