:original_name: obs_04_0017.html

.. _obs_04_0017:

Uploading an Object
===================

Scenarios
---------

You can upload files of any type to OBS buckets for storage.

The following describes how to call the API for :ref:`uploading objects using the PUT method <obs_04_0080>` to a specified bucket. For details about how to call an API, see :ref:`Calling APIs <obs_04_0006>`.

Prerequisites
-------------

-  You have obtained the AK and SK. For details, see :ref:`Obtaining Access Keys (AK/SK) <obs_04_0116>`.
-  At least one bucket is available.
-  The file to be uploaded has been prepared and you know the complete local path of the file.
-  You have obtained the region of the bucket which you want to upload files to and determined the endpoint required for API calls. For details, see `Regions and Endpoints <https://docs.sc.otc.t-systems.com/en-us/endpoint/index.html>`__.

Uploading the Object **objecttest1** to Bucket **bucket001** in the a1 Region
-----------------------------------------------------------------------------

In this example, an Apache HttpClient is used.

::

   package com.obsclient;

   import java.io.*;
   import java.util.ArrayList;
   import java.util.List;

   import org.apache.http.Header;
   import org.apache.http.HttpEntity;
   import org.apache.http.NameValuePair;
   import org.apache.http.client.entity.UrlEncodedFormEntity;
   import org.apache.http.client.methods.CloseableHttpResponse;
   import org.apache.http.client.methods.HttpGet;
   import org.apache.http.client.methods.HttpPost;
   import org.apache.http.client.methods.HttpPut;
   import org.apache.http.entity.InputStreamEntity;
   import org.apache.http.entity.StringEntity;
   import org.apache.http.impl.client.CloseableHttpClient;
   import org.apache.http.impl.client.HttpClients;
   import org.apache.http.message.BasicNameValuePair;


   public class TestMain {

       /* Hard-coded or plaintext AK and SK are risky. For security purposes, encrypt your AK and SK and store them in the configuration file or environment variables.
       In this example, the AK and SK are stored in environment variables for identity authentication. Before running the code in this example, configure environment variables YOUR_AK and YOUR_SK. */
       public static String accessKey = System.getenv("YOUR_AK"); //The value is the AK obtained.
       public static String securityKey = System.getenv("YOUR_SK");  //The value is the SK obtained.

       public static void main(String[] str) {

           putObjectToBucket();

       }


       private static void putObjectToBucket() {

           InputStream inputStream = null;
           CloseableHttpClient httpClient = HttpClients.createDefault();
           CloseableHttpResponse httpResponse = null;
           String requestTime = DateUtils.formatDate(System.currentTimeMillis());
           HttpPut httpPut = new HttpPut("http://bucket001.obs.a1.example.com/objecttest1");
           httpPut.addHeader("Date", requestTime);

            /**Calculate the signature based on the request.**/
           String contentMD5 = "";
           String contentType = "";
           String canonicalizedHeaders = "";
           String canonicalizedResource = "/bucket001/objecttest1";
           // Content-MD5 and Content-Type fields do not contain line breaks. The data format is RFC 1123, which is the same as the time in the request.
           String canonicalString = "PUT" + "\n" + contentMD5 + "\n" + contentType + "\n" + requestTime + "\n" + canonicalizedHeaders + canonicalizedResource;
           System.out.println("StringToSign:[" + canonicalString + "]");
           String signature = null;
           try {
               signature = Signature.signWithHmacSha1(securityKey, canonicalString);
               // Directory for storing uploaded files
               inputStream = new FileInputStream("D:\\OBSobject\\text01.txt");
               InputStreamEntity entity = new InputStreamEntity(inputStream);
               httpPut.setEntity(entity);

              // Added the Authorization: OBS AccessKeyID:signature field to the header.
               httpPut.addHeader("Authorization", "OBS " + accessKey + ":" + signature);
               httpResponse = httpClient.execute(httpPut);

              // Prints the sending request information and the received response message.
               System.out.println("Request Message:");
               System.out.println(httpPut.getRequestLine());
               for (Header header : httpPut.getAllHeaders()) {
                   System.out.println(header.getName() + ":" + header.getValue());
               }

               System.out.println("Response Message:");
               System.out.println(httpResponse.getStatusLine());
               for (Header header : httpResponse.getAllHeaders()) {
                   System.out.println(header.getName() + ":" + header.getValue());
               }
               BufferedReader reader = new BufferedReader(new InputStreamReader(
                       httpResponse.getEntity().getContent()));

               String inputLine;
               StringBuffer response = new StringBuffer();

               while ((inputLine = reader.readLine()) != null) {
                   response.append(inputLine);
               }
               reader.close();

               // print result
               System.out.println(response.toString());


           } catch (UnsupportedEncodingException e) {
               e.printStackTrace();

           } catch (IOException e) {
               e.printStackTrace();
           } finally {
               try {
                   httpClient.close();
               } catch (IOException e) {
                   e.printStackTrace();
               }
           }
       }

   }

**The format of the** **Date** **header field** **DateUtils** **is as follows:**

::

   package com.obsclient;

   import java.text.DateFormat;
   import java.text.SimpleDateFormat;
   import java.util.Locale;
   import java.util.TimeZone;

   public class DateUtils {

       public static String formatDate(long time)
       {
           DateFormat serverDateFormat = new SimpleDateFormat("EEE, dd MMM yyyy HH:mm:ss z", Locale.ENGLISH);
           serverDateFormat.setTimeZone(TimeZone.getTimeZone("GMT"));
           return serverDateFormat.format(time);
       }
   }

**The method of calculating the signature character string is as follows:**

::

   package com.obsclient;

   import javax.crypto.Mac;
   import javax.crypto.spec.SecretKeySpec;
   import java.io.UnsupportedEncodingException;
   import java.security.NoSuchAlgorithmException;
   import java.security.InvalidKeyException;
   import java.util.Base64;

   public class Signature {
       public static String signWithHmacSha1(String sk, String canonicalString) throws UnsupportedEncodingException {

           try {
               SecretKeySpec signingKey = new SecretKeySpec(sk.getBytes("UTF-8"), "HmacSHA1");
               Mac mac = Mac.getInstance("HmacSHA1");
               mac.init(signingKey);
               return Base64.getEncoder().encodeToString(mac.doFinal(canonicalString.getBytes("UTF-8")));
           } catch (NoSuchAlgorithmException | InvalidKeyException | UnsupportedEncodingException e) {
               e.printStackTrace();
           }
           return null;
       }
   }
