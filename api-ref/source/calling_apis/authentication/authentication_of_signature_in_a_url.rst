:original_name: obs_04_0011.html

.. _obs_04_0011:

Authentication of Signature in a URL
====================================

You can create a presigned URL for a specific operation. This kind of URL includes the user AK, signature, validity period, resources and other information. It allows any user who gets it to perform the specified operation (such as download) as if they are its creator. Presigned URLs enable authentication without secret access keys. Such URLs, however, must be used before expiration.

A request with a presigned URL is formed as follows:

.. code-block:: text

   GET /ObjectKey?AccessKeyId=AccessKeyID&Expires=ExpiresValue&Signature=signature HTTP/1.1
   Host: bucketname.obs.region.example.com

A download request with a URL that uses a temporary AK/SK pair and security token is formed as follows:

.. code-block:: text

   GET /ObjectKey?AccessKeyId=AccessKeyID&Expires=ExpiresValue&Signature=signature&x-obs-security-token=securitytoken HTTP/1.1
   Host: bucketname.obs.region.example.com

:ref:`Table 1 <obs_04_0011__table5447121714296>` describes the parameters.

.. _obs_04_0011__table5447121714296:

.. table:: **Table 1** Request parameters

   +-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Parameter             | Description                                                                                                                                                         | Mandatory             |
   +=======================+=====================================================================================================================================================================+=======================+
   | AccessKeyId           | The access key of the URL creator. OBS uses it to verify the identity.                                                                                              | Yes                   |
   |                       |                                                                                                                                                                     |                       |
   |                       | Type: string                                                                                                                                                        |                       |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Expires               | When the URL expires, measured as a Unix timestamp (how many seconds elapsed since 00:00:00 on January 1, 1970). After the specified time elapses, the URL expires. | Yes                   |
   |                       |                                                                                                                                                                     |                       |
   |                       | Type: string                                                                                                                                                        |                       |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Signature             | The signature based on the user SK and **Expires**                                                                                                                  | Yes                   |
   |                       |                                                                                                                                                                     |                       |
   |                       | Type: string                                                                                                                                                        |                       |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | x-obs-security-token  | A temporary AK/SK pair must be used with a security token, indicated by the **x-obs-security-token** header.                                                        | No                    |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

A signature is calculated as follows:

#. .. _obs_04_0011__li587641544619:

   Construct the StringToSign.

#. .. _obs_04_0011__li4876101544611:

   Encode the result of :ref:`1 <obs_04_0011__li587641544619>` in UTF-8.

#. .. _obs_04_0011__li187621516463:

   Use the SK to calculate HMAC-SHA1 based on the result of :ref:`2 <obs_04_0011__li4876101544611>`.

#. .. _obs_04_0011__li208761159468:

   Encode the result of :ref:`3 <obs_04_0011__li187621516463>` in Base64.

#. Encode the result of :ref:`4 <obs_04_0011__li208761159468>` in URL to obtain the signature.

The format of StringToSign is shown below. :ref:`Table 2 <obs_04_0011__table34479832212511>` describes the parameters.

.. code-block::

   StringToSign =
        HTTP-Verb + "\n" +
        Content-MD5 + "\n" +
        Content-Type + "\n" +
        Expires + "\n" +
        CanonicalizedHeaders + CanonicalizedResource

.. _obs_04_0011__table34479832212511:

.. table:: **Table 2** Parameters for StringToSign

   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                         | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
   +===================================+==============================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================+
   | HTTP-Verb                         | Type of operation. For REST APIs, HTTP request operations include **PUT**, **GET**, and **DELETE**.                                                                                                                                                                                                                                                                                                                                                                                                                                          |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Content-MD5                       | (Optional) Base64-encoded 128-bit MD5 value of the request body based on RFC 1864                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Content-Type                      | The type of the message, for example, **text/plain**.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
   |                                   | If this header is not included, an empty string is used.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Expires                           | When the URL expires (**ExpiresValue**)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | CanonicalizedHeaders              | HTTP request headers that start with **x-obs-**, such as **x-obs-date**, **x-obs-acl**, and **x-obs-meta-\***.                                                                                                                                                                                                                                                                                                                                                                                                                               |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
   |                                   | #. All characters in a header name must be lower-case. Multiple header names are sorted in alphabetical order.                                                                                                                                                                                                                                                                                                                                                                                                                               |
   |                                   | #. If a header has more than one value, combine them using commas (,). For example, **x-obs-meta-name:name1** and **x-obs-meta-name:name2** need to be written as **x-obs-meta-name:name1,name2**.                                                                                                                                                                                                                                                                                                                                           |
   |                                   | #. Non-ASCII or unrecognizable characters are not allowed for header names and also not recommended for header values. If such characters are required, encode or decode them on the client using URL or Base64. The server does not perform decoding.                                                                                                                                                                                                                                                                                       |
   |                                   | #. Delete meaningless spaces or tabs in a header. For example, **x-obs-meta-name: name** (there is a meaningless space before the second **name**) must be changed to **x-obs-meta-name:name**.                                                                                                                                                                                                                                                                                                                                              |
   |                                   | #. Each header occupies a separate line.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | CanonicalizedResource             | OBS resources specified in an HTTP request.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
   |                                   | Resources are arranged in this order: bucket name, object name, sub-resource 1, sub-resource 2...                                                                                                                                                                                                                                                                                                                                                                                                                                            |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
   |                                   | #. Bucket name and object name, for example, **/bucket/object**. If no object name is specified, for example, **/bucket/**, the entire bucket is listed. If no bucket name is specified either, the value of this field is **/**.                                                                                                                                                                                                                                                                                                            |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
   |                                   | #. If a subresource (such as **?acl** and **?logging**) exists, the subresource must be added.                                                                                                                                                                                                                                                                                                                                                                                                                                               |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
   |                                   |    OBS sub-resources: acl, attname, cors, delete, deletebucket, inventory, length, lifecycle, location, logging, metadata, modify, name, notification, partNumber, policy, position, quota, replication, response-cache-control, response-content-disposition, response-content-encoding, response-content-language, response-content-type, response-expires, restore, storageClass, storagePolicy, storageinfo, tagging, torrent, uploadId, uploads, versionId, versioning, versions, website, x-obs-security-token, object-lock, retention |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
   |                                   | #. Sort multiple sub-resources in alphabetical order by name and use ampersands (&) to separate them.                                                                                                                                                                                                                                                                                                                                                                                                                                        |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
   |                                   | .. note::                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
   |                                   |    -  A sub-resource is usually unique. Do not specify multiple values for the same sub-resource (such as key=value1&key=value2). Otherwise, only the first value is used.                                                                                                                                                                                                                                                                                                                                                                   |
   |                                   |    -  Suppose you use the **GetObject** API to download version **xxx** of object **object-test** from bucket **bucket-test** and require **Content-Type** be changed to **text/plain**. **CanonicalizedResource** is **/bucket-test/object-test?response-content-type=text/plain&versionId=xxx**.                                                                                                                                                                                                                                           |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Use hash-based message authentication code (HMAC) to calculate the signature based on the StringToSign and SK:

.. code-block::

   Signature = URL-Encode( Base64( HMAC-SHA1( Your_SK, UTF-8-Encoding-Of( StringToSign ) ) ) )

Compared with the Authorization header method:

-  URLs must use URL encoding — after using Base64 — for signatures.
-  **Expires** in **StringToSign** of a URL is similar to **Date** in the **Authorization** header.

Generate a predefined URL instance for the browser by carrying the signature in the URL.

.. table:: **Table 3** Request that has the signature carried in the URL and the StringToSign

   +------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------+
   | Request Header                                                                                                                           | StringToSign                      |
   +==========================================================================================================================================+===================================+
   | GET /objectkey?AccessKeyId=MFyfvK41ba2giqM7Uio6PznpdUKGpownRZlmVmHc&Expires=1532779451&Signature=0Akylf43Bm3mD1bh2rM3dmVp1Bo%3D HTTP/1.1 | GET \\n                           |
   |                                                                                                                                          |                                   |
   | Host: examplebucket.obs.\ *region*.example.com                                                                                           | ``\n``                            |
   |                                                                                                                                          |                                   |
   |                                                                                                                                          | ``\n``                            |
   |                                                                                                                                          |                                   |
   |                                                                                                                                          | 1532779451\\n                     |
   |                                                                                                                                          |                                   |
   |                                                                                                                                          | /examplebucket/objectkey          |
   +------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------+

.. table:: **Table 4** Object download request that has the temporary AK/SK and security token carried in the URL and the StringToSign

   +---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------+
   | Request Header                                                                                                                                                                  | StringToSign                                                    |
   +=================================================================================================================================================================================+=================================================================+
   | GET /objectkey?AccessKeyId=MFyfvK41ba2giqM7Uio6PznpdUKGpownRZlmVmHc&Expires=1532779451&Signature=0Akylf43Bm3mD1bh2rM3dmVp1Bo%3D&x-obs-security-token=YwkaRTbdY8g7q.... HTTP/1.1 | GET \\n                                                         |
   |                                                                                                                                                                                 |                                                                 |
   | Host: examplebucket.obs.\ *region*.example.com                                                                                                                                  | ``\n``                                                          |
   |                                                                                                                                                                                 |                                                                 |
   |                                                                                                                                                                                 | ``\n``                                                          |
   |                                                                                                                                                                                 |                                                                 |
   |                                                                                                                                                                                 | 1532779451\\n                                                   |
   |                                                                                                                                                                                 |                                                                 |
   |                                                                                                                                                                                 | /examplebucket/objectkey?x-obs-security-token=YwkaRTbdY8g7q.... |
   +---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------+

Calculation rule of the signature

.. code-block::

   Signature = URL-Encode( Base64( HMAC-SHA1( Your_SK, UTF-8-Encoding-Of( StringToSign ) ) ) )

Calculate the signature and use the host as the prefix of the URL to generate a predefined URL:

http(s)://examplebucket.obs.\ *region*.example.com/objectkey?AccessKeyId=AccessKeyID&Expires=1532779451&Signature=0Akylf43Bm3mD1bh2rM3dmVp1Bo%3D

If you enter the address in the browser, then the object **objectkey** in the **examplebucket** bucket can be downloaded. The validity period of this link is **1532779451** (indicating Sat Jul 28 20:04:11 CST 2018).

In the Linux operating system, when running the **curl** command, you need to add a forward slash (\\) to escape the character (&). The following command can download the **objectkey** object to the **output** file:

curl http(s)://examplebucket.obs.\ *region*.example.com/objectkey?AccessKeyId=AccessKeyID\\&Expires=1532779451\\&Signature=0Akylf43Bm3mD1bh2rM3dmVp1Bo%3D -X GET -o output

.. note::

   If you want to open a pre-defined URL using your browser, you must not use **Content-MD5**, **Content-Type**, or **CanonicalizedHeaders** headers to calculate a signature. This is because the browser cannot carry them. If you do so, the server will return a signature error.

Signature Calculation in Java
-----------------------------

::

   import java.io.UnsupportedEncodingException;
   import java.net.URLEncoder;
   import java.security.InvalidKeyException;
   import java.security.NoSuchAlgorithmException;
   import java.util.ArrayList;
   import java.util.Arrays;
   import java.util.Base64;
   import java.util.Collections;
   import java.util.HashMap;
   import java.util.List;
   import java.util.Locale;
   import java.util.Map;
   import java.util.TreeMap;
   import java.util.regex.Pattern;

   import javax.crypto.Mac;
   import javax.crypto.spec.SecretKeySpec;

   public class SignDemo {

       private static final String SIGN_SEP = "\n";

       private static final String OBS_PREFIX = "x-obs-";

       private static final String DEFAULT_ENCODING = "UTF-8";

       private static final List<String> SUB_RESOURCES = Collections.unmodifiableList(Arrays.asList(
               "CDNNotifyConfiguration", "acl", "attname",  "cors", "delete",
               "deletebucket", "inventory", "length", "lifecycle", "location", "logging",
               "metadata", "mirrorBackToSource", "modify", "name", "notification", "obscompresspolicy",
               "partNumber", "policy", "position", "quota","replication", "response-cache-control",
               "response-content-disposition","response-content-encoding", "response-content-language", "response-content-type",
               "response-expires","restore", "storageClass", "storagePolicy", "storageinfo", "tagging", "torrent", "truncate",
               "uploadId", "uploads", "versionId", "versioning", "versions", "website",
               "x-obs-security-token", "object-lock", "retention"));

       private String ak;

       private String sk;

       private boolean isBucketNameValid(String bucketName) {
           if (bucketName == null || bucketName.length() > 63 || bucketName.length() < 3) {
               return false;
           }

           if (!Pattern.matches("^[a-z0-9][a-z0-9.-]+$", bucketName)) {
               return false;
           }

           if (Pattern.matches("(\\d{1,3}\\.){3}\\d{1,3}", bucketName)) {
               return false;
           }

           String[] fragments = bucketName.split("\\.");
           for (int i = 0; i < fragments.length; i++) {
               if (Pattern.matches("^-.*", fragments[i]) || Pattern.matches(".*-$", fragments[i])
                       || Pattern.matches("^$", fragments[i])) {
                   return false;
               }
           }

           return true;
       }

       public String encodeUrlString(String path) throws UnsupportedEncodingException {
           return URLEncoder.encode(path, DEFAULT_ENCODING)
                   .replaceAll("\\+", "%20")
                   .replaceAll("\\*", "%2A")
                   .replaceAll("%7E", "~");
       }

       public String encodeObjectName(String objectName) throws UnsupportedEncodingException {
           StringBuilder result = new StringBuilder();
           String[] tokens = objectName.split("/");
           for (int i = 0; i < tokens.length; i++) {
               result.append(this.encodeUrlString(tokens[i]));
               if (i < tokens.length - 1) {
                   result.append("/");
               }
           }
           return result.toString();
       }

       private String join(List<?> items, String delimiter) {
           StringBuilder sb = new StringBuilder();
           for (int i = 0; i < items.size(); i++) {
               String item = items.get(i).toString();
               sb.append(item);
               if (i < items.size() - 1) {
                   sb.append(delimiter);
               }
           }
           return sb.toString();
       }

       private boolean isValid(String input) {
           return input != null && !input.equals("");
       }

       public String hmacSha1(String input) throws NoSuchAlgorithmException, InvalidKeyException, UnsupportedEncodingException {
           SecretKeySpec signingKey = new SecretKeySpec(this.sk.getBytes(DEFAULT_ENCODING), "HmacSHA1");
           Mac mac = Mac.getInstance("HmacSHA1");
           mac.init(signingKey);
           return Base64.getEncoder().encodeToString(mac.doFinal(input.getBytes(DEFAULT_ENCODING)));
       }

       private String stringToSign(String httpMethod, Map<String, String[]> headers, Map<String, String> queries,
                                   String bucketName, String objectName, long expires) throws Exception {
           String contentMd5 = "";
           String contentType = "";
           TreeMap<String, String> canonicalizedHeaders = new TreeMap<String, String>();
           String key;
           List<String> temp = new ArrayList<String>();
           for (Map.Entry<String, String[]> entry : headers.entrySet()) {
               key = entry.getKey();
               if (key == null || entry.getValue() == null || entry.getValue().length == 0) {
                   continue;
               }
               key = key.trim().toLowerCase(Locale.ENGLISH);
               if (key.equals("content-md5")) {
                   contentMd5 = entry.getValue()[0];
                   continue;
               }
               if (key.equals("content-type")) {
                   contentType = entry.getValue()[0];
                   continue;
               }
               if (key.startsWith(OBS_PREFIX)) {
                   for (String value : entry.getValue()) {
                       if (value != null) {
                           temp.add(value.trim());
                       }
                   }
                   canonicalizedHeaders.put(key, this.join(temp, ","));
                   temp.clear();
               }
           }
           // handle method/content-md5/content-type
           StringBuilder stringToSign = new StringBuilder();
           stringToSign.append(httpMethod).append(SIGN_SEP)
                   .append(contentMd5).append(SIGN_SEP)
                   .append(contentType).append(SIGN_SEP)
                   .append(expires).append(SIGN_SEP);


           // handle canonicalizedHeaders
           for (Map.Entry<String, String> entry : canonicalizedHeaders.entrySet()) {
               stringToSign.append(entry.getKey()).append(":").append(entry.getValue()).append(SIGN_SEP);
           }


           // handle CanonicalizedResource
           stringToSign.append("/");
           if (this.isValid(bucketName)) {
               stringToSign.append(bucketName).append("/");
               if (this.isValid(objectName)) {
                   stringToSign.append(this.encodeObjectName(objectName));
               }
           }

           TreeMap<String, String> canonicalizedResource = new TreeMap<String, String>();
           for (Map.Entry<String, String> entry : queries.entrySet()) {
               key = entry.getKey();
               if (key == null) {
                   continue;
               }

               if (SUB_RESOURCES.contains(key)) {
                   canonicalizedResource.put(key, entry.getValue());
               }
           }

           if (canonicalizedResource.size() > 0) {
               stringToSign.append("?");
               for (Map.Entry<String, String> entry : canonicalizedResource.entrySet()) {
                   stringToSign.append(entry.getKey());
                   if (this.isValid(entry.getValue())) {
                       stringToSign.append("=").append(entry.getValue());
                   }
                   stringToSign.append("&");
               }
               stringToSign.deleteCharAt(stringToSign.length() - 1);
           }
           //      System.out.println(String.format("StringToSign:%s%s", SIGN_SEP, stringToSign.toString()));

           return stringToSign.toString();
       }

       public String querySignature(String httpMethod, Map<String, String[]> headers, Map<String, String> queries,
                                     String bucketName, String objectName, long expires) throws Exception {
            if (!isBucketNameValid(bucketName)) {
                throw new IllegalArgumentException("the bucketName is illegal");
            }
            //1. stringToSign
            String stringToSign = this.stringToSign(httpMethod, headers, queries, bucketName, objectName, expires);

            //2. signature
            return this.encodeUrlString(this.hmacSha1(stringToSign));
        }

       public String getURL(String endpoint, Map<String, String> queries,
                            String bucketName, String objectName, String signature, long expires) throws UnsupportedEncodingException {
           StringBuilder URL = new StringBuilder();
           URL.append("https://").append(bucketName).append(".").append(endpoint).append("/").
                   append(this.encodeObjectName(objectName)).append("?");
           String key;
           for (Map.Entry<String, String> entry : queries.entrySet()) {
               key = entry.getKey();
               if (key == null) {
                   continue;
               }
               if (SUB_RESOURCES.contains(key)) {
                   String value = entry.getValue();
                   URL.append(key);
                   if (value != null) {
                       URL.append("=").append(value).append("&");
                   } else {
                       URL.append("&");
                   }
               }
           }
           URL.append("AccessKeyId=").append(this.ak).append("&Expires=").append(expires).
                   append("&Signature=").append(signature);
           return URL.toString();
       }

       public static void main(String[] args) throws Exception {
           SignDemo demo = new SignDemo();

           /* Hard-coded or plaintext AK and SK are risky. For security purposes, encrypt your AK and SK and store them in the configuration file or environment variables.
           In this example, the AK and SK are stored in environment variables for identity authentication. Before running the code in this example, configure environment variables YOUR_AK and YOUR_SK. */
       demo.ak = System.getenv("YOUR_AK");
       demo.sk = System.getenv("YOUR_SK");
           String endpoint = "<your-endpoint>";

           String bucketName = "bucket-test";
           String objectName = "hello.jpg";

           // A header cannot be included if you want to use a URL to access OBS with a browser. If a header is added to headers, the signature does not match. To use headers, it must be processed by the client.
           Map<String, String[]> headers = new HashMap<String, String[]>();
           Map<String, String> queries = new HashMap<String, String>();

           // Expiration time. Set it to expire in 24 hours.
           long expires = (System.currentTimeMillis() + 86400000L) / 1000;
           String signature = demo.querySignature("GET", headers, queries, bucketName, objectName, expires);
           System.out.println(signature);
           String URL = demo.getURL(endpoint, queries, bucketName, objectName, signature, expires);
           System.out.println(URL);
       }
   }
