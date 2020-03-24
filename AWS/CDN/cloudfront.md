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
