## CloudFront Basics
### What is AWS CloudFront?
* Managed Content Delivery Network (CDN) by AWS
* CloudFront allows customers to distribute content with low latency and high data transfer rates by serving requests using a network of edge locations around the world.
* Cloudfront is a **global** (not regional) service
  * It uses ingress (injection proxy) to upload objects and egress to distribute content.
* Web Application Firewall (WAF) can also be integrated with CloudFront.
* DDoS Protection, integration with AWS Shield
* **Compliance**
  * PCI DSS Compliant: AWS recommends against caching Credit Card information in edge locations
  * HIPAA Eligible: HIPAA recognizes AWS CloudFront as HIPAA eligible service

### Edge Locations
* The content is delivered through a worldwide network of data centers called edge location (not same as region/AZ in AWS).
* Edge Locations are **not tied** to **AZs or REGIONS**.
* By default, each object stays in an edge location for 24 hours before it expires.
* The minimum expiration time is 0 seconds (no caching); there isn't a maximum expiration time limit.

### CloudFront vs S3 Cross Region Replication
* CloudFront
  * Global Edge Network
  * Files are cached for a TTL
  * Great for static content distribution across the globe
  
* S3 Cross Region Replication
  * Must be setup for each individual region
  * Files are updated in near real-time
  * Read only - No active-active configuration supported
  * Great for dynamic content that needs to be available at low-latency in certain regions.
  
### CloudFront Signed URL vs S3 Pre-Signed URL
* CloudFront Signed URL
  * It provides access to a path, no matter what the origin is (can be a S3 bucket or a customer origin)
  * Account wide key-pair, only the root can manage it
  * Can filter by IP, path, date, expiration
  * Can leverage caching features
  
* S3 Pre-Signed URL
  * Issue a request as the person which pre-signed the URL
  * The credentials that you can use to create a presigned URL include:
    * **IAM instance profile**: Valid up to 6 hours
    * **AWS Security Token Service**: Valid up to 36 hours when signed with permanent credentials, such as the credentials of the AWS account root user or an IAM user
    * **IAM user**: Valid up to 7 days when using AWS Signature Version 4
  * The presigned URLs are valid only for the specified duration.
  * If you created a presigned URL using a temporary token, then the URL expires when the token expires, even if the URL was created with a later expiration time.

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

### CloudFront - Origins
* **S3 bucket**
  * For distributing files and caching them at the edge
  * Enhanced security with CloudFront Origin Accces Identity (OAI)
  * CloudFront can be used as an ingress (to upload files to S3)
  
* **S3 Website**
  * For this, you must first enable the bucket as a static S3 website.
  
* **Custom Origin (HTTP)**
  * Application Load Balancer
  * EC2 instance
  * API Gateway (API Gateway Edge)
  * Any HTTP backend

It's possible to have primary/secondary origins for High Availability (HA) and/or Failover

### S3 bucket as Origing - Origin Access Identity (OAI)
* If you use CloudFront signed URLs or signed cookies to restrict access to files in your Amazon S3 bucket, you probably also want to prevent users from accessing your Amazon S3 files by using Amazon S3 URLs. This is achieved by using OAI.

* To ensure that your users access your files using only CloudFront URLs, regardless of whether the URLs are signed, do the following:
  1. Create an origin access identity, which is a special CloudFront user, and associate the origin access identity with CloudFront distribution.
  2. Change the permissions either on your Amazon S3 bucket or on the files in your bucket so that only the origin access identity has read permission (or read and download permission).
  
* When your users access your Amazon S3 files through CloudFront, the CloudFront origin access identity gets the files on behalf of your users. If your users request files directly by using Amazon S3 URLs, they're denied access.

### Custom Origin - ALB/EC2 as Origing
* Please note that **EC2 or ALB must be Public**.
* The communication between the CloudFront edge locations and EC2/ALB happens over internet.

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
