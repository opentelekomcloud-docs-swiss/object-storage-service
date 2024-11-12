:original_name: obs_faq_0051.html

.. _obs_faq_0051:

Which Events Can Trigger Event Notifications?
=============================================

OBS supports notification for the following event types:

-  **ObjectCreated**: all kinds of object creation operations, including PUT, POST, COPY, and part assembling

   -  **Put**: Creates or overwrites an object using the PUT method.
   -  **Post**: Creates or overwrites an object using the POST (browser-based upload) method.
   -  **Copy**: Creates or overwrites an object using the COPY method.
   -  **CompleteMultipartUpload**: Assembles parts of a multipart upload.

-  **ObjectRemoved**: Deletes an object.

   -  **Delete**: Deletes an object with a specified version ID.
   -  **DeleteMarkerCreated**: Deletes an object without specifying a version ID.
