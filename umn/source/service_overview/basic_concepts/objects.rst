:original_name: obs_03_0206.html

.. _obs_03_0206:

Objects
=======

Objects are basic units stored in OBS. An object contains both data and the metadata that describes data attributes. Data uploaded to OBS is stored in buckets as objects.

An object consists of the following:

-  A key that specifies the name of an object. An object key is a UTF-8 string up to 1,024 characters long. Each object within a bucket is uniquely identified by a key.
-  Metadata that describes an object. The metadata is a set of key-value pairs that are assigned to objects stored in OBS. There are two types of metadata: system-defined metadata and custom metadata.

   -  System-defined metadata is automatically assigned by OBS. Such metadata includes Date, Content-Length, Last-Modified, ETag, and more.
   -  You can specify custom metadata to describe the object when you upload an object to OBS.

-  Data that refers to the content of an object.

Objects are generally managed as files, but OBS, as an object-based service, has no concept of files and folders. For easy data management, OBS provides a method to simulate folders. By adding a slash (/) to an object name, for example, **test/123.jpg**, you can specify **test** as a folder and **123.jpg** as the name of a file in the **test** folder. The key of the object is **test/123.jpg**.

When uploading an object, you can specify a storage class for it. If you do not specify a storage class, the object inherits the storage class of the bucket. You can also change the storage class of an existing object in a bucket.

On OBS Console and OBS Browser+, you can use folders the same way you use them in a file system.

.. _obs_03_0206__section320173016163:

Object Key Naming Guidelines
----------------------------

Although any UTF-8 characters can be used in an object key name, naming object keys according to the following guidelines can help maximize the object keys' compatibility with other applications. Ways to analyze special characters vary depending on applications. The following guidelines help object key names substantially meet the requirements of DNS, web security characters, XML analyzers and other APIs.

The following character sets can be safely used in key names.

+---------------------------------------------------------------+-----------------------------------+
| Alphanumeric characters (also known as unreserved characters) | 0-9, a-z, and A-Z                 |
+---------------------------------------------------------------+-----------------------------------+
| Special characters (also known as reserved characters)        | Exclamation mark (!)              |
|                                                               |                                   |
|                                                               | Hyphen (-)                        |
|                                                               |                                   |
|                                                               | Underscore (_)                    |
|                                                               |                                   |
|                                                               | Period (.)                        |
|                                                               |                                   |
|                                                               | Asterisk (``*``)                  |
|                                                               |                                   |
|                                                               | Single quote (')                  |
|                                                               |                                   |
|                                                               | Left parenthesis (()              |
|                                                               |                                   |
|                                                               | Right parenthesis ())             |
+---------------------------------------------------------------+-----------------------------------+

The following are examples of valid object key names:

.. code-block::

   4my-organization
   my.great_photos-2014/jan/myvacation.jpg
   videos/2014/birthday/video1.wmv
