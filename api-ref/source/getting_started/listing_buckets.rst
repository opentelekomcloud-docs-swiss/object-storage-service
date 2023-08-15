:original_name: obs_04_0016.html

.. _obs_04_0016:

Listing Buckets
===============

Scenarios
---------

If you want to view information about all buckets created by yourself, you can call the API for listing buckets.

The following describes how to call the API for :ref:`listing buckets <obs_04_0020>`. For details about how to call an API, see :ref:`Calling APIs <obs_04_0006>`.

Prerequisites
-------------

-  You have obtained the AK and SK. For details about how to obtain the AK and SK, see :ref:`Obtaining Access Keys (AK/SK) <obs_04_0116>`.
-  You need to specify the region where the buckets to be listed reside and determine the endpoint for calling an API based on the region. For details, see `Regions and Endpoints <https://docs.sc.otc.t-systems.com/en-us/endpoint/index.html>`__.

Obtaining the Bucket List in the a1 Region
------------------------------------------

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

       public static String accessKey = "UDSIAMSTUBTEST000012"; //The value of this parameter is the AK obtained.
        public static String securityKey = "Udsiamstubtest000000UDSIAMSTUBTEST000012";  //The value of this parameter is the SK obtained.

       public static void main(String[] str) {

           listAllMyBuckets();

       }


       private static void listAllMyBuckets() {
           CloseableHttpClient httpClient = HttpClients.createDefault();
           String requesttime = DateUtils.formatDate(System.currentTimeMillis());


           HttpGet httpGet = new HttpGet("http://obs.a1.example.com");
           httpGet.addHeader("Date", requesttime);

           /**Calculate the signature based on the request.**/
           String contentMD5 = "";
           String contentType = "";
           String canonicalizedHeaders = "";
           String canonicalizedResource = "/";
           // Content-MD5 and Content-Type fields do not contain line breaks. The data format is RFC 1123, which is the same as the time in the request.
           String canonicalString = "GET" + "\n" + contentMD5 + "\n" + contentType + "\n" + requesttime + "\n" + canonicalizedHeaders + canonicalizedResource;
           System.out.println("StringToSign:[" + canonicalString + "]");
           String signature = null;
           try {
               signature = Signature.signWithHmacSha1(securityKey, canonicalString);

                // Added the Authorization: OBS AccessKeyID:signature field to the header.
               httpGet.addHeader("Authorization", "OBS " + accessKey + ":" + signature);
               CloseableHttpResponse httpResponse = httpClient.execute(httpGet);

               // Prints the sending request information and the received response message.
               System.out.println("Request Message:");
               System.out.println(httpGet.getRequestLine());
               for (Header header : httpGet.getAllHeaders()) {
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

The format of the **Date** header field **DateUtils** is as follows:

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

The method of calculating the signature character string is as follows:

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
