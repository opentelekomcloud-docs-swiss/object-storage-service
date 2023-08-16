:original_name: obs_04_0118.html

.. _obs_04_0118:

Consistency of Concurrent Operations
====================================

After a success message is returned in response to a client's write or deletion request, the client can obtain the latest data. If a client that initiates a write request times out in waiting for a response, or the server returns HTTP response status code **500** or **503**, the subsequent read operations may fail. If such an error occurs, query whether the data has been successfully uploaded to the server. If not, upload the data again.

If a client simultaneously uploads, queries, or deletes the same object or bucket, these operations may reach the system at different times and have different latency periods, so different results may return. For example, if multiple clients simultaneously upload the same object, the latest upload request received by the system will replace the previous one. If you want to prevent an object from being simultaneously accessed, you must add a lock mechanism for the object in upper-layer applications.

Example of Concurrent Operations
--------------------------------

1. When client1 is uploading an object V1, client2 is uploading an object V2 with the same name. After the successful uploads, both client1 and client2 can access the latest object data V2, as shown in :ref:`Figure 1 <obs_04_0118__fig143262124514>`.

.. _obs_04_0118__fig143262124514:

.. figure:: /_static/images/en-us_image_0100846816.png
   :alt: **Figure 1** Concurrent upload of the same object

   **Figure 1** Concurrent upload of the same object

2. When client2 is uploading an object V1 and object metadata is not written yet, client1 deletes an object with the same name. In this scenario, the upload operation of client2 is still successful, and both client1 and client2 can access data object V1, as shown in :ref:`Figure 2 <obs_04_0118__fig143141034184518>`.

.. _obs_04_0118__fig143141034184518:

.. figure:: /_static/images/en-us_image_0100846818.png
   :alt: **Figure 2** Concurrent upload and deletion of the same object (1)

   **Figure 2** Concurrent upload and deletion of the same object (1)

3. When client2 has successfully uploaded an object V1 and object metadata is still being written, client1 deletes an object with the same name. In this scenario, the upload operation of client2 is still successful. However, when client1 and client2 attempt to download the object, they may be able to access data object V1, or an error may be returned indicating that the object does not exist, as shown in :ref:`Figure 3 <obs_04_0118__fig017318519469>`.

.. _obs_04_0118__fig017318519469:

.. figure:: /_static/images/en-us_image_0100846820.png
   :alt: **Figure 3** Concurrent upload and deletion of the same object (2)

   **Figure 3** Concurrent upload and deletion of the same object (2)

4. When client1 is downloading an object, client2 deletes an object with the same name. In this scenario, client1 may have downloaded a full copy or only part of the object data. After a deletion success message is returned to client2, an attempt to download the object will fail, and an error will be returned indicating that the object does not exist, as shown in :ref:`Figure 4 <obs_04_0118__fig17810203484616>`.

.. _obs_04_0118__fig17810203484616:

.. figure:: /_static/images/en-us_image_0100846822.png
   :alt: **Figure 4** Concurrent download and deletion of the same object

   **Figure 4** Concurrent download and deletion of the same object

5. When client1 is downloading an object, client2 is updating an object with the same name. In this scenario, client1 may have downloaded a full copy or only part of the object data. After an update success message is returned to client 2, an attempt to download the object will succeed, and the latest data will be returned, as shown in :ref:`Figure 5 <obs_04_0118__fig16197219472>`.

.. _obs_04_0118__fig16197219472:

.. figure:: /_static/images/en-us_image_0100846824.png
   :alt: **Figure 5** Concurrent download and update of the same object

   **Figure 5** Concurrent download and update of the same object

6. When client2 is uploading part V1 of an object, client1 is uploading part V2 of the same object. After part V2 is uploaded successfully, both client1 and client2 can list the information about the multipart whose entity tag (ETag) is part V2, as shown in :ref:`Figure 6 <obs_04_0118__fig097482816477>`.

.. _obs_04_0118__fig097482816477:

.. figure:: /_static/images/en-us_image_0100846826.png
   :alt: **Figure 6** Concurrently uploading the same part of the same object

   **Figure 6** Concurrently uploading the same part of the same object
