---
layout: post
title: How to Generate AWS Signature Version 4
modified:
categories: 
excerpt: generate aws signature version 4, groovy
tags: []
image:
  feature:
date: 2018-12-28T15:11:51+07:00
---
>> Signature Version 4 is the process to add authentication information to AWS requests sent by HTTP. For security, most requests to AWS must be signed with an access key, which consists of an access key ID and secret access key. These two keys are commonly referred to as your security credentials. [aws](https://docs.aws.amazon.com/general/latest/gr/signature-version-4.html)

For more detail,  
1. [Create a Canonical Request for Signature Version 4](https://docs.aws.amazon.com/general/latest/gr/sigv4-create-canonical-request.html)  
2. [Create a String to Sign for Signature Version 4](https://docs.aws.amazon.com/general/latest/gr/sigv4-create-string-to-sign.html)  
3. [Calculate the Signature for AWS Signature Version 4](https://docs.aws.amazon.com/general/latest/gr/sigv4-calculate-signature.html)  
4. [Add the Signature to the HTTP Request](https://docs.aws.amazon.com/general/latest/gr/sigv4-add-signature-to-request.html)  

{% highlight java %}
import javax.crypto.Mac
import javax.crypto.spec.SecretKeySpec
import java.security.MessageDigest

class app2 {
    static def HmacSHA256(String data, byte[] key) {
        def algorithm = "HmacSHA256"
        Mac mac = Mac.getInstance(algorithm)
        mac.init(new SecretKeySpec(key, algorithm))
        return mac.doFinal(data.getBytes("UTF8"))
    }


    static void main(String[] args) {
        /* variabel */
        def sha1 = MessageDigest.getInstance("SHA-256")
        def httpVerb = "GET"
        def path="/"
        def queryString="Action=ListUsers&Version=2010-05-08"
        def contentType = "content-type:application/x-www-form-urlencoded; charset=utf-8"
        def host = "host:iam.amazonaws.com"
        def xAmzDate = "x-amz-date:20150830T123600Z"
        def xAmzTarget = "x-amz-target:RekognitionService.CompareFaces"
        def signHeaders = "content-type;host;x-amz-date"
        def body = ""
        def algorithm = "AWS4-HMAC-SHA256"
        def serviceName = "iam"
        def regionName = "us-east-1"
        def aws4Request = "aws4_request"
        def secretKey = "wJalrXUtnFEMI/K7MDENG+bPxRfiCYEXAMPLEKEY"
        def accessKey = "AKIAISGUFQ4A43I2GLPA"
        def timestamp = "20150830T123600Z"
        def date = "20150830"
        def credentialScope = date + "/" + regionName + "/" + serviceName + "/" + aws4Request
        def aws4Key = "AWS4" + secretKey
        def digestBody = sha1.digest(body.getBytes())
        def hashedBody = (new BigInteger(1, digestBody).toString(16))
        /* end variabel */

        /* canonical header */
        def canonicalHeaders = new StringBuilder()
        canonicalHeaders.append(path).append("\n")
        canonicalHeaders.append(queryString).append("\n")
        canonicalHeaders.append(contentType).append("\n")
        canonicalHeaders.append(host).append("\n")
        canonicalHeaders.append(xAmzDate).append("\n")
        canonicalHeaders = canonicalHeaders.toString()
        /* end canonical header */

        /* signed header */
        def signedHeaders = new StringBuilder()
        signedHeaders.append(signHeaders)
        signedHeaders = signedHeaders.toString()
        /* end signed header */

        /* canonical request */
        def canonicalRequest = new StringBuilder()
        canonicalRequest.append(httpVerb).append("\n")
        canonicalRequest.append(canonicalHeaders).append("\n")
        canonicalRequest.append(signedHeaders).append("\n")
        canonicalRequest.append(hashedBody)
        canonicalRequest = canonicalRequest.toString()
  
        println("canonicalRequest")
        println(canonicalRequest)
        println("==========")
        /* end canonical request */

        /* hashed canonical */
        def digest = sha1.digest(canonicalRequest.getBytes())
        def hashedCanonical = (new BigInteger(1, digest).toString(16))
        
        println("hashedCanonical")
        println(hashedCanonical)
        println("==========")
        /* end hashed canonical */
        

        /* string to sign */
        def stringToSign = new StringBuilder()
        stringToSign.append(algorithm).append("\n")
        stringToSign.append(timestamp).append("\n")
        stringToSign.append(credentialScope).append("\n")
        stringToSign.append(hashedCanonical)
        stringToSign = stringToSign.toString()
        
        println("stringToSign")
        println(stringToSign)
        println("==========")
        /* end string to sign */

        /* derived Signing Key */
        def kDate = HmacSHA256(date, aws4Key.getBytes())
        def kRegion = HmacSHA256(regionName, kDate)
        def kService = HmacSHA256(serviceName, kRegion)
        def kSigning = HmacSHA256(aws4Request, kService)
        def derivedSigningKey = (new BigInteger(1, kSigning).toString(16))
        
        println("derivedSigningKey")
        println(derivedSigningKey)
        println("==========")
        /* end derived Signing Key */


        /* signature */
        def signatureHexa = HmacSHA256(stringToSign, kSigning)
        def signature = (new BigInteger(1, signatureHexa).toString(16))
        
        println("signature")
        println(signature)
        println("==========")
        /* end signature */

        /* header signature */
        def headerSignature = algorithm + " Credential=" + accessKey + "/" + credentialScope + ", SignedHeaders=" + signedHeaders + ", Signature=" + signature
        /* end header signature */

        println(headerSignature)
    }

}
{% endhighlight %}

### output
 {% highlight java %}
canonicalRequest
GET
/
Action=ListUsers&Version=2010-05-08
content-type:application/x-www-form-urlencoded; charset=utf-8
host:iam.amazonaws.com
x-amz-date:20150830T123600Z

content-type;host;x-amz-date
e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
==========
hashedCanonical
f536975d06c0309214f805bb90ccff089219ecd68b2577efef23edd43b7e1a59
==========
stringToSign
AWS4-HMAC-SHA256
20150830T123600Z
20150830/us-east-1/iam/aws4_request
f536975d06c0309214f805bb90ccff089219ecd68b2577efef23edd43b7e1a59
==========
derivedSigningKey
c4afb1cc5771d871763a393e44b703571b55cc28424d1a5e86da6ed3c154a4b9
==========
signature
5d672d79c15b13162d9279b0855cfba6789a8edb4c82c400e06b5924a6f2b5d7
==========
finished Authorization header
Authorization:AWS4-HMAC-SHA256 Credential=AKIAISGUFQ4A43I2GLPA/20150830/us-east-1/iam/aws4_request, SignedHeaders=content-type;host;x-amz-date, Signature=5d672d79c15b13162d9279b0855cfba6789a8edb4c82c400e06b5924a6f2b5d7
 {% endhighlight %}