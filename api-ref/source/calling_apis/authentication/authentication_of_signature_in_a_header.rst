:original_name: obs_04_0010.html

.. _obs_04_0010:

Authentication of Signature in a Header
=======================================

For all API operations, the most common identity authentication is to carry signatures in headers.

In the header, the signature is carried in the authorization header field of the HTTP message. The format of the message header is as follows:

.. code-block::

   Authorization: OBS AccessKeyID:signature

The process of calculating a signature is as follows:

#. .. _obs_04_0010__li162697142015:

   Construct the StringToSign.

#. .. _obs_04_0010__li5269617200:

   Encode the result of :ref:`1 <obs_04_0010__li162697142015>` in UTF-8.

#. .. _obs_04_0010__li1226919112203:

   Use the SK to calculate the HMAC-SHA1 signature on the result of :ref:`2 <obs_04_0010__li5269617200>`.

#. Encode the result of :ref:`3 <obs_04_0010__li1226919112203>` in Base64 to obtain the signature.

The StringToSign is constructed according to the following rules. :ref:`Table 1 <obs_04_0010__table34479832212511>` describes the parameters.

.. code-block::

   StringToSign =
       HTTP-Verb + "\n" +
       Content-MD5 + "\n" +
       Content-Type + "\n" +
       Date + "\n" +
       CanonicalizedHeaders + CanonicalizedResource

.. _obs_04_0010__table34479832212511:

.. table:: **Table 1** Parameters required for constructing a StringToSign

   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                         | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
   +===================================+============================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================+
   | HTTP-Verb                         | Indicates an HTTP request method supported by the OBS REST API. The value can be an HTTP verb such as **PUT**, **GET**, or **DELETE**.                                                                                                                                                                                                                                                                                                                                                                                                                     |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Content-MD5                       | Base64-encoded 128-bit MD5 digest of the message according to RFC 1864. This parameter can be empty. For details, see :ref:`Table 6 <obs_04_0010__table12510133817416>` and the algorithm examples below the table.                                                                                                                                                                                                                                                                                                                                        |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Content-Type                      | Specifies the message type, for example, **text/plain**.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
   |                                   | If a request does not contain this header field, this parameter is deemed as an empty string. For details, see :ref:`Table 2 <obs_04_0010__table14775325212511>`.                                                                                                                                                                                                                                                                                                                                                                                          |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Date                              | Time when a request is initiated. This parameter uses the RFC 1123 time format. If the deviation between the time specified by this parameter and the server time is over 15 minutes, the server returns error 403.                                                                                                                                                                                                                                                                                                                                        |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
   |                                   | This parameter is an empty string when the **x-obs-date** is specified. For details, see :ref:`Table 6 <obs_04_0010__table12510133817416>`.                                                                                                                                                                                                                                                                                                                                                                                                                |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
   |                                   | If an operation (for example, obtaining an object content) is temporarily authorized, this parameter is not required.                                                                                                                                                                                                                                                                                                                                                                                                                                      |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | CanonicalizedHeaders              | OBS request header field in an HTTP request header, referring to header fields starting with **x-obs-**, such as, **x-obs-date**, **x-obs-acl**, and **x-obs-meta-\***. When calling an API, choose a header that is supported by the API as required.                                                                                                                                                                                                                                                                                                     |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
   |                                   | #. All characters of keywords in a request header field must be converted to lowercase letters (content values must be case sensitive). If a request contains multiple header fields, these fields should be organized by keyword in the alphabetical order from a to z.                                                                                                                                                                                                                                                                                   |
   |                                   | #. If multiple header fields in a request have the same prefix, combine the header fields into one. For example, **x-obs-meta-name:name1** and **x-obs-meta-name:name2** should be reorganized into **x-obs-meta-name:name1,name2**. Use comma to separate the values.                                                                                                                                                                                                                                                                                     |
   |                                   | #. Keywords in the request header field cannot contain non-ASCII or unrecognizable characters, which are also not advisable for values in the request header field. If the two types of characters are necessary, they should be encoded and decoded on the client side. Either URL encoding or Base64 encoding is acceptable, but the server does not perform decoding.                                                                                                                                                                                   |
   |                                   | #. Delete meaningless spaces and tabs in a header field. For example, **x-obs-meta-name: name** (with a meaningless space before **name**) must be changed to **x-obs-meta-name:name**.                                                                                                                                                                                                                                                                                                                                                                    |
   |                                   | #. Each header field occupies a separate line. See :ref:`Table 4 <obs_04_0010__table46456687212511>`.                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | CanonicalizedResource             | Indicates the OBS resource specified by an HTTP request. This parameter is constructed as follows:                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
   |                                   | <Bucket name + Object name> + [Subresource 1] + [Subresource 2] + ...                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
   |                                   | #. Bucket name and object name, for example, **/bucket/object**. If no object name is specified, for example, **/bucket/**, the entire bucket is listed. If no bucket name is specified either, the value of this field is **/**.                                                                                                                                                                                                                                                                                                                          |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
   |                                   | #. If a subresource (such as **?acl** and **?logging**) exists, the subresource must be added.                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
   |                                   |    OBS supports a variety of sub-resources, including acl, attname, cors, delete, deletebucket, inventory, length, lifecycle, location, logging, metadata, modify, name, notification, partNumber, policy, position, quota, replication, response-cache-control, response-content-disposition, response-content-encoding, response-content-language, response-content-type, response-expires, storagePolicy, storageinfo, tagging, torrent, uploadId, uploads, versionId, versioning, versions, website, object-lock, retention, and x-obs-security-token. |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
   |                                   | #. If there are multiple subresources, sort them in the alphabetical order from a to z, and use **&** to combine the subresources.                                                                                                                                                                                                                                                                                                                                                                                                                         |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
   |                                   | .. note::                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
   |                                   |    -  A subresource is unique. Do not add subresources with the same keyword (for example, **key=value1&key=value2**) in the same request URL. In this case, signature is computed only based on the first subresource, and only the value of the first subresource takes effect on the actual service.                                                                                                                                                                                                                                                    |
   |                                   |    -  Using the **GetObject** API as an example, assume there is a bucket named **bucket-test** and an object named **object-test** in the bucket, and the object version is **xxx**. When obtaining the object, you need to rewrite Content-Type to **text/plain**. Then, the **CanonicalizedResource** calculated by the signature is **/bucket-test/object-test?response-content-type=text/plain&versionId=xxx**.                                                                                                                                       |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

The following tables provide some examples of generating StringToSign.

.. _obs_04_0010__table14775325212511:

.. table:: **Table 2** Obtaining an object

   +-----------------------------------------+-----------------------------------+
   | Request Header                          | StringToSign                      |
   +=========================================+===================================+
   | GET /object.txt HTTP/1.1                | GET \\n                           |
   |                                         |                                   |
   | Host: bucket.obs.\ *region*.example.com | ``\n``                            |
   |                                         |                                   |
   | Date: Sat, 12 Oct 2015 08:12:38 GMT     | ``\n``                            |
   |                                         |                                   |
   |                                         | Sat, 12 Oct 2015 08:12:38 GMT\\n  |
   |                                         |                                   |
   |                                         | /bucket/object.txt                |
   +-----------------------------------------+-----------------------------------+

.. table:: **Table 3** Using temporary AK/SK and security token to upload objects

   +------------------------------------------+---------------------------------------------+
   | Request Header                           | StringToSign                                |
   +==========================================+=============================================+
   | PUT /object.txt HTTP/1.1                 | PUT\\n                                      |
   |                                          |                                             |
   | User-Agent: curl/7.15.5                  | ``\n``                                      |
   |                                          |                                             |
   | Host: bucket.obs.\ *region*.example.com  | text/plain\\n                               |
   |                                          |                                             |
   | x-obs-date:Tue, 15 Oct 2015 07:20:09 GMT | ``\n``                                      |
   |                                          |                                             |
   | x-obs-security-token: YwkaRTbdY8g7q....  | x-obs-date:Tue, 15 Oct 2015 07:20:09 GMT\\n |
   |                                          |                                             |
   | content-type: text/plain                 | x-obs-security-token:YwkaRTbdY8g7q....\\n   |
   |                                          |                                             |
   | Content-Length: 5913339                  | /bucket/object.txt                          |
   +------------------------------------------+---------------------------------------------+

.. note::

   For details about how to obtain a temporary AK/SK pair and security token, see `Obtaining a Temporary AK/SK Pair <https://docs.sc.otc.t-systems.com/api/iam/en-us_topic_0097949518.html>`__.

.. _obs_04_0010__table46456687212511:

.. table:: **Table 4** An object upload request containing header fields

   +-----------------------------------------+-----------------------------------+
   | Request Header                          | StringToSign                      |
   +=========================================+===================================+
   | PUT /object.txt HTTP/1.1                | PUT\\n                            |
   |                                         |                                   |
   | User-Agent: curl/7.15.5                 | ``\n``                            |
   |                                         |                                   |
   | Host: bucket.obs.\ *region*.example.com | text/plain\\n                     |
   |                                         |                                   |
   | Date: Mon, 14 Oct 2015 12:08:34 GMT     | Mon, 14 Oct 2015 12:08:34 GMT\\n  |
   |                                         |                                   |
   | x-obs-acl: public-read                  | x-obs-acl:public-read\\n          |
   |                                         |                                   |
   | content-type: text/plain                | /bucket/object.txt                |
   |                                         |                                   |
   | Content-Length: 5913339                 |                                   |
   +-----------------------------------------+-----------------------------------+

.. table:: **Table 5** Obtaining an object ACL

   +-----------------------------------------+-----------------------------------+
   | Request Header                          | StringToSign                      |
   +=========================================+===================================+
   | GET /object.txt?acl HTTP/1.1            | GET \\n                           |
   |                                         |                                   |
   | Host: bucket.obs.\ *region*.example.com | ``\n``                            |
   |                                         |                                   |
   | Date: Sat, 12 Oct 2015 08:12:38 GMT     | ``\n``                            |
   |                                         |                                   |
   |                                         | Sat, 12 Oct 2015 08:12:38 GMT\\n  |
   |                                         |                                   |
   |                                         | /bucket/object.txt?acl            |
   +-----------------------------------------+-----------------------------------+

.. _obs_04_0010__table12510133817416:

.. table:: **Table 6** An object upload request carrying the Content-MD5 header

   +------------------------------------------+---------------------------------------------+
   | Request Header                           | StringToSign                                |
   +==========================================+=============================================+
   | PUT /object.txt HTTP/1.1                 | PUT\\n                                      |
   |                                          |                                             |
   | Host: bucket.obs.\ *region*.example.com  | I5pU0r4+sgO9Emgl1KMQUg==\\n                 |
   |                                          |                                             |
   | x-obs-date:Tue, 15 Oct 2015 07:20:09 GMT | ``\n``                                      |
   |                                          |                                             |
   | Content-MD5: I5pU0r4+sgO9Emgl1KMQUg==    | ``\n``                                      |
   |                                          |                                             |
   | Content-Length: 5913339                  | x-obs-date:Tue, 15 Oct 2015 07:20:09 GMT\\n |
   |                                          |                                             |
   |                                          | /bucket/object.txt                          |
   +------------------------------------------+---------------------------------------------+

Content-MD5 Algorithm in Java
-----------------------------

::

   import java.security.MessageDigest;
   import sun.misc.BASE64Encoder;
   import java.io.UnsupportedEncodingException;
   import java.security.NoSuchAlgorithmException;

   public class Md5{
        public static void main(String[] args) {
             try {
                    String exampleString = "blog";
                    MessageDigest messageDigest = MessageDigest.getInstance("MD5");
                    BASE64Encoder encoder = new BASE64Encoder();
                    String contentMd5 = encoder.encode(messageDigest.digest(exampleString.getBytes("utf-8")));
                    System.out.println("Content-MD5:" + contentMd5);
             } catch (NoSuchAlgorithmException | UnsupportedEncodingException e)
             {
                    e.printStackTrace();
             }
        }
   }

The signature is generated as follows based on the StringToSign and SK. The hash-based message authentication code algorithm (HMAC algorithm) is used to generate the signature.

.. code-block::

   Signature = Base64( HMAC-SHA1( YourSecretAccessKeyID, UTF-8-Encoding-Of( StringToSign ) ) )

For example, to create a private bucket named **newbucketname2** in a region, the format of a client request is as follows:

.. code-block:: text

   PUT / HTTP/1.1
   Host: newbucketname2.obs.region.example.com
   Content-Length: length
   Date: Fri, 06 Jul 2018 03:45:51 GMT
   x-obs-acl:private
   Authorization: OBS UDSIAMSTUBTEST000254:ydH8ffpcbS6YpeOMcEZfn0wE90c=
   <CreateBucketConfiguration xmlns="http://obs.region.example.com/doc/2015-06-30/">
       <Location>region</Location>
   </CreateBucketConfiguration>

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
       "response-expires","storagePolicy", "storageinfo", "tagging", "torrent", "truncate",
       "uploadId", "uploads", "versionId", "versioning", "versions", "website",
        "x-obs-security-token", "object-lock", "retention"));

       private String ak;

       private String sk;

        public String urlEncode(String input) throws UnsupportedEncodingException {
           return URLEncoder.encode(input, DEFAULT_ENCODING)
               .replaceAll("%7E", "~") //for browser
               .replaceAll("%2F", "/")
               .replaceAll("%20", "+");
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
           String bucketName, String objectName) throws Exception{
           String contentMd5 = "";
           String contentType = "";
           String date = "";

           TreeMap<String, String> canonicalizedHeaders = new TreeMap<String, String>();

           String key;
           List<String> temp = new ArrayList<String>();
           for(Map.Entry<String, String[]> entry : headers.entrySet()) {
               key = entry.getKey();
               if(key == null || entry.getValue() == null || entry.getValue().length == 0) {
                   continue;
               }

               key = key.trim().toLowerCase(Locale.ENGLISH);
               if(key.equals("content-md5")) {
                   contentMd5 = entry.getValue()[0];
                   continue;
               }

               if(key.equals("content-type")) {
                   contentType = entry.getValue()[0];
                   continue;
               }

               if(key.equals("date")) {
                   date = entry.getValue()[0];
                   continue;
               }

               if(key.startsWith(OBS_PREFIX)) {
                   for(String value : entry.getValue()) {
                       if(value != null) {
                           temp.add(value.trim());
                       }
                   }
                   canonicalizedHeaders.put(key, this.join(temp, ","));
                   temp.clear();
               }
           }

           if(canonicalizedHeaders.containsKey("x-obs-date")) {
               date = "";
           }

           // handle method/content-md5/content-type/date
           StringBuilder stringToSign = new StringBuilder();
           stringToSign.append(httpMethod).append(SIGN_SEP)
               .append(contentMd5).append(SIGN_SEP)
               .append(contentType).append(SIGN_SEP)
               .append(date).append(SIGN_SEP);

           // handle canonicalizedHeaders
           for(Map.Entry<String, String> entry : canonicalizedHeaders.entrySet()) {
               stringToSign.append(entry.getKey()).append(":").append(entry.getValue()).append(SIGN_SEP);
           }

           // handle CanonicalizedResource
           stringToSign.append("/");
           if(this.isValid(bucketName)) {
               stringToSign.append(bucketName).append("/");
               if(this.isValid(objectName)) {
                   stringToSign.append(this.urlEncode(objectName));
               }
           }

           TreeMap<String, String> canonicalizedResource = new TreeMap<String, String>();
           for(Map.Entry<String, String> entry : queries.entrySet()) {
               key = entry.getKey();
               if(key == null) {
                   continue;
               }

               if(SUB_RESOURCES.contains(key)) {
                   canonicalizedResource.put(key, entry.getValue());
               }
           }

           if(canonicalizedResource.size() > 0) {
               stringToSign.append("?");
               for(Map.Entry<String, String> entry : canonicalizedResource.entrySet()) {
                   stringToSign.append(entry.getKey());
                   if(this.isValid(entry.getValue())) {
                       stringToSign.append("=").append(entry.getValue());
                   }
                   stringToSign.append("&");
               }
               stringToSign.deleteCharAt(stringToSign.length()-1);
           }

           //    System.out.println(String.format("StringToSign:%s%s", SIGN_SEP, stringToSign.toString()));

           return stringToSign.toString();
       }

       public String headerSignature(String httpMethod, Map<String, String[]> headers, Map<String, String> queries,
           String bucketName, String objectName) throws Exception {

           //1. stringToSign
           String stringToSign = this.stringToSign(httpMethod, headers, queries, bucketName, objectName);

           //2. signature
           return String.format("OBS %s:%s", this.ak, this.hmacSha1(stringToSign));
       }

       public String querySignature(String httpMethod, Map<String, String[]> headers, Map<String, String> queries,
           String bucketName, String objectName, long expires) throws Exception {
           if(headers.containsKey("x-obs-date")) {
               headers.put("x-obs-date", new String[] {String.valueOf(expires)});
           } else {
               headers.put("date", new String[] {String.valueOf(expires)});
           }
           //1. stringToSign
           String stringToSign = this.stringToSign(httpMethod, headers, queries, bucketName, objectName);

           //2. signature
           return this.urlEncode(this.hmacSha1(stringToSign));
       }

       public static void main(String[] args) throws Exception {
           SignDemo demo = new SignDemo();

                   /* Hard-coded or plaintext AK and SK are risky. For security purposes, encrypt your AK and SK and store them in the configuration file or environment variables.
           In this example, the AK and SK are stored in environment variables for identity authentication. Before running the code in this example, configure environment variables YOUR_AK and YOUR_SK. */
           demo.ak = System.getenv("YOUR_AK");
           demo.sk = System.getenv("YOUR_SK");

           String bucketName = "bucket-test";
           String objectName = "hello.jpg";
           Map<String, String[]> headers = new HashMap<String, String[]>();
           headers.put("date", new String[] {"Sat, 12 Oct 2015 08:12:38 GMT"});
           headers.put("x-obs-acl", new String[] {"public-read"});
           headers.put("x-obs-meta-key1", new String[] {"value1"});
           headers.put("x-obs-meta-key2", new String[] {"value2", "value3"});
           Map<String, String> queries = new HashMap<String, String>();
           queries.put("acl", null);

           System.out.println(demo.headerSignature("PUT", headers, queries, bucketName, objectName));
       }

   }

The calculation result of the signature is **ydH8ffpcbS6YpeOMcEZfn0wE90c=**, which varies depending on the execution time.

Signature Algorithm in Python
-----------------------------

::

   import os
   import sys
   import hashlib
   import hmac
   import binascii
   from datetime import datetime
   IS_PYTHON2 = sys.version_info.major == 2 or sys.version < '3'

   # Hard-coded or plaintext AK and SK are risky. For security purposes, encrypt your AK and SK and store them in the configuration file or environment variables.
   # In this example, the AK and SK are stored in environment variables for identity authentication. Before running the code in this example, configure environment variables YOUR_AK and YOUR_SK.
   yourSecretAccessKeyID = os.getenv('YOUR_SK')
   httpMethod = "PUT"
   contentType = "application/xml"
   # "date" is the time when the request was actually generated
   date = datetime.utcnow().strftime('%a, %d %b %Y %H:%M:%S GMT')
   canonicalizedHeaders = "x-obs-acl:private\n"
   CanonicalizedResource = "/newbucketname2"
   canonical_string = httpMethod + "\n" + "\n" + contentType + "\n" + date + "\n" + canonicalizedHeaders + CanonicalizedResource
   if IS_PYTHON2:
       hashed = hmac.new(yourSecretAccessKeyID, canonical_string, hashlib.sha1)
       encode_canonical = binascii.b2a_base64(hashed.digest())[:-1]
   else:
       hashed = hmac.new(yourSecretAccessKeyID.encode('UTF-8'), canonical_string.encode('UTF-8'), hashlib.sha1)
       encode_canonical = binascii.b2a_base64(hashed.digest())[:-1].decode('UTF-8')

   print(encode_canonical)

The calculation result of the signature is **ydH8ffpcbS6YpeOMcEZfn0wE90c=**, which varies depending on the execution time.
