:original_name: en-us_topic_0125560506.html

.. _en-us_topic_0125560506:

DELETE Bucket lifecycle
=======================

You can use this operation to delete the lifecycle configuration of a bucket.

After the lifecycle configuration of a bucket is deleted, OBS will not automatically delete objects in that bucket.

Only users granted the **s3:PutLifecycleConfiguration** permission can delete the bucket lifecycle configuration. By default, only the bucket owner can delete the bucket lifecycle configuration. The bucket owner can allow other users to delete the bucket lifecycle configuration by granting them the permission.

Request Syntax
--------------

.. code-block:: text

   DELETE /?lifecycle HTTP/1.1
   User-agent: agent
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Thu, 05 Sep 2013 10:58:33 +0000
    Authorization: AWS B9A70C60A39C4D551A16:1iTeJ0lyd3dLM911NvNhWXSzLSQ=

Request Parameters
------------------

This request involves no parameters.

Request Headers
---------------

This request uses common headers. For details about common request headers, see section :ref:`Common Request Headers <en-us_topic_0125560462>`.

Request Elements
----------------

This request involves no elements.

Response Syntax
---------------

.. code-block::

   HTTP/1.1 204 No Content
    Server: OBS
    x-amz-request-id: 90E2BA0A420C00000140EDC608490C46
    x-amz-id-2: KjN5GBIHSX5z8vJPmmrQSIfzvlhsjnofUEap+GZ4pzuawO3+ArTKAZWtXoTFKA/0
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Date: Thu, 05 Sep 2013 10:58:33 GMT

Response Headers
----------------

This response uses common headers. For details about common response headers, see section :ref:`Common Response Headers <en-us_topic_0125560484>`.

Response elements
-----------------

This response involves no elements.

Error Responses
---------------

No special error responses are returned. For details about error responses, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`.

Sample Request
--------------

.. code-block:: text

   DELETE /?lifecycle HTTP/1.1
   User-Agent: curl/7.29.0
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Thu, 05 Sep 2013 10:09:36 +0000
    Authorization: AWS B9A70C60A39C4D551A16:oNFuFZV8JLUqxsaFPI1Gs/HPRKg=

Sample Response
---------------

.. code-block::

   HTTP/1.1 204 No Content
    Server: OBS
    x-amz-request-id: 90E2BA0A420C00000140EDC608490C46
    x-amz-id-2: KjN5GBIHSX5z8vJPmmrQSIfzvlhsjnofUEap+GZ4pzuawO3+ArTKAZWtXoTFKA/0
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Date: Thu, 05 Sep 2013 10:58:33 GMT
