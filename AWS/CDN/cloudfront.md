## CloudFront Basics
### What is AWS CloudFront?
* Managed Content Delivery Network (CDN) by AWS
* CloudFront allows customers to distribute content with low latency and high data transfer rates by serving requests using a network of edge locations around the world.
* Cloudfront is a **global** (not regional) service
  * It uses ingress (injection proxy) to upload objects and egress to distribute content.
* Web Application Firewall (WAF) can also be integrated with CloudFront.
* **Compliance**
  * PCI DSS Compliant: AWS recommends against caching Credit Card information in edge locations
  * HIPAA Eligible: HIPAA recognizes AWS CloudFront as HIPAA eligible service

### Edge Locations
* The content is delivered through a worldwide network of data centers called edge location (not same as region/AZ in AWS).
* Edge Locations are **not tied** to **AZs or REGIONS**.
* By default, each object stays in an edge location for 24 hours before it expires.
* The minimum expiration time is 0 seconds (no caching); there isn't a maximum expiration time limit.

### What are the different distribution options in CloudFront?
**1. WEB Distribution** - Create a web distribution if you want to:
* Speed up distribution of static and dynamic content, for example, .html, .css, .php, and graphics files.
* Distribute media files using HTTP or HTTPS.
* Add, update, or delete objects, and submit data from web forms.
* Use live streaming to stream an event in real time.

You store your files in an origin - either an Amazon S3 bucket or a web server. After you create the distribution, you can add more origins to the distribution.

**2. RTMP Distribution** - Create an RTMP distribution to speed up distribution of your **streaming media files** using **Adobe Flash Media Server's RTMP protocol**. An RTMP distribution allows an end user to begin playing a media file before the file has finished downloading from a CloudFront edge location. Note the following:

* To create an RTMP distribution, you **must store the media files in an Amazon S3 bucket**.
* To use CloudFront live streaming, create a web distribution.
* RTMP stands for Real Time Media Processing

* **Limit** - CloudFront lets you create a total of up to 200 web distributions and 100 RTMP distributions for an AWS account.
* Please be mindful of the fact that any changes to the CloudFront distribution might take up to 45 minutes to get deployed to the edge locations.

### Visualizing Viewer / Origin Protocol
```
        Viewer Request                     Origin Request
       --------------->                   --------------->
CLIENT  VIEWER PROTOCOL   EDGE LOCATIONS   ORIGIN PROTOCOL  CLOUDFRONT ORIGIN(S)
       <---------------                   <---------------
        Viewer Response                    Origin Response
```
* **Viewer Protocol**
  * The techincal configuration of the communication between Client and the Edge Location.
  * HTTP or HTTPS / Redirect HTTP to HTTPS / HTTPS only
  * HTTP Methods: GET,HEAD,OPTIONS,PUT,POST,PATCH,DELETE etc.
  * Configured via Cache Behaviour Settings

* **Origin Protocol**
  * The techincal configuration between the "Origin" and the Edge location.
  * If the "Origin" is an Amazon Service such as S3/ELB/MediaStore, you don't need to define the Origin Protocol setting. If using custom origin, this needs to be set.

## CloudFront: Server Name Indication (SNI) and HTTP Redirection

### CloudFront with custom SSL certificates
* CloudFront supports custom SSL certificates, giving you the ability to upload your own certificate to your AWS account, and to select it for use with your CloudFront distribution.
* This model works with any browser because AWS **dedicates IP addresses to your SSL certificate at each CloudFront edge location**.
* The dedicated IP addresses are necessary so that CloudFront can associate the incoming requests with the proper SSL certificate.

### Server Name Indication (SNI) for Custom SSL Certificates
* SNI support for CloudFront gives customers a second way to use their own SSL certificates with CloudFront.
* With the SNI extension of TLS, dedicated IP addresses are no longer necessary.
* This is because modern web browsers and HTTP client libraries transmit the destination host name at the beginning of the SSL handshaking process.
* Old browsers, which don't support SNI extension, will not be able to load the HTTPS content. If you want to take advantage of SNI and need to support legacy browsers, you can detect them in your client code and route the HTTPS requests directly to the origin server.
  * IE on Windows XP
  * Default browsers on Android 2.2
  * Java web browsers earlier than version 1.7

### HTTP Redirection at the Edge
* If you are moving an existing HTTP-based site to a full or partial HTTPS-based model, you can use a CloudFront behavior to configure CloudFront to redirect HTTP requests to HTTPS.
  * View Protocol Policy: "Redirect HTTP to HTTPS"
* When yours users make an HTTP request for an object that’s in a distribution configured for redirection, the CloudFront edge location will return an HTTP 301 (moved permanently) status code, along with the HTTPS URL for the object.
  * Your Viewer will then make a second request for the object, this time via HTTPS.

For more information on this topic, please read through the following [AWS Blog](https://aws.amazon.com/blogs/aws/server-name-indication-sni-and-http-redirection-for-amazon-cloudfront/).
