:original_name: en-us_topic_0045853553.html

.. _en-us_topic_0045853553:

Logging Overview
================

You can enable logging to facilitate analysis or audit as required. Access logs enable a bucket owner to analyze the property, type, or trend of requests to the bucket in depth. When the logging function of a bucket is enabled, OBS will log access requests for the bucket automatically, and write the generated log files to the specified bucket (target bucket).

The logging function itself is offered for free, only the space occupied by log files is charged.

After logging is enabled, the log delivery user group will be automatically granted the permission to read the bucket ACL and write the bucket where logs are saved. If you manually disable such permissions, bucket logging fails.

OBS can record bucket access requests in logs for request analysis and log audit.

Logs occupy the OBS storage that incurs costs, so OBS does not collect bucket access logs by default.

OBS creates log files and uploads them to a specified bucket. To perform these operations, OBS must be granted required permissions. Therefore, before configuring logging for a bucket, you need to create an IAM agency for OBS and add this agency when configuring logging for the bucket. By default, when configuring permissions for an agency, you only need to grant the agency the permission to upload log files (PutObject) to the bucket for storing log files. In the following example, **mybucketlogs** is the bucket. If the default encryption function is enabled for the log storing bucket, the IAM agency also requires the KMS Administrator permissions in the region where the log storing bucket resides.

.. code-block::

   {
       "Version": "1.1",
       "Statement": [
           {
               "Action": [
                   "obs:object:PutObject"
               ],
               "Resource": [
                   "OBS:*:*:object:mybucketlogs/*"
               ],
               "Effect": "Allow"
           }
       ]
   }

After logging is configured, you can view operation logs in the bucket that stores the logs in approximately fifteen minutes.

The following shows an example access log of the target bucket:

.. code-block::

   787f2f92b20943998a4fe2ab75eb09b8 bucket [13/Aug/2015:01:43:42 +0000] xx.xx.xx.xx
   787f2f92b20943998a4fe2ab75eb09b8 281599BACAD9376ECE141B842B94535B  REST.GET.BUCKET.LOCATION
   - "GET /bucket?location HTTP/1.1" 200 - 211 - 6 6 "-"  "HttpClient" - -

The access log of each bucket contains the following information.

.. table:: **Table 1** Bucket log format

   +-----------------+----------------------------------+-------------------------------------------------+
   | Parameter       | Value Example                    | Description                                     |
   +=================+==================================+=================================================+
   | BucketOwner     | 787f2f92b20943998a4fe2ab75eb09b8 | Account ID of the bucket owner                  |
   +-----------------+----------------------------------+-------------------------------------------------+
   | Bucket          | bucket                           | Name of the bucket                              |
   +-----------------+----------------------------------+-------------------------------------------------+
   | Time            | [13/Aug/2015:01:43:42 +0000]     | Timestamp of the request (UTC)                  |
   +-----------------+----------------------------------+-------------------------------------------------+
   | Remote IP       | xx.xx.xx.xx                      | IP address from where the request is initiated  |
   +-----------------+----------------------------------+-------------------------------------------------+
   | Requester       | 787f2f92b20943998a4fe2ab75eb09b8 | Requester ID                                    |
   +-----------------+----------------------------------+-------------------------------------------------+
   | RequestID       | 281599BACAD9376ECE141B842B94535B | Request ID                                      |
   +-----------------+----------------------------------+-------------------------------------------------+
   | Operation       | REST.GET.BUCKET.LOCATION         | Name of the operation                           |
   +-----------------+----------------------------------+-------------------------------------------------+
   | Key             | ``-``                            | Object name                                     |
   +-----------------+----------------------------------+-------------------------------------------------+
   | Request-URI     | GET /bucket?location HTTP/1.1    | URI of the request                              |
   +-----------------+----------------------------------+-------------------------------------------------+
   | HTTPStatus      | 200                              | Return code                                     |
   +-----------------+----------------------------------+-------------------------------------------------+
   | ErrorCode       | ``-``                            | Error code                                      |
   +-----------------+----------------------------------+-------------------------------------------------+
   | BytesSent       | 211                              | Size of the HTTP response, expressed in bytes   |
   +-----------------+----------------------------------+-------------------------------------------------+
   | ObjectSize      | ``-``                            | Object size (bytes)                             |
   +-----------------+----------------------------------+-------------------------------------------------+
   | TotalTime       | 6                                | Processing time on the server (ms)              |
   +-----------------+----------------------------------+-------------------------------------------------+
   | Turn-AroundTime | 6                                | Total time for processing the request (ms)      |
   +-----------------+----------------------------------+-------------------------------------------------+
   | Referer         | ``-``                            | Header field **Referer** of the request         |
   +-----------------+----------------------------------+-------------------------------------------------+
   | User-Agent      | HttpClient                       | User-Agent header of the request                |
   +-----------------+----------------------------------+-------------------------------------------------+
   | VersionID       | ``-``                            | Version ID carried in the request               |
   +-----------------+----------------------------------+-------------------------------------------------+
   | STSLogUrn       | ``-``                            | Federated authentication and agency information |
   +-----------------+----------------------------------+-------------------------------------------------+
