# Cloudfront
- CloudFront is a Content Delivery network (CDN) within AWS.
- Origin - The source location of your content
- S3 origin or custom origin (anything other than S3 origin)
- Distribution - The unit of configuration within cloudfront
- everything in cloudfront is inside a distribution directly or indirectly
- Edge Location - local cache of your data.
- Regional Edge location - larger version of an edge location. Provides another layer of caching.
  - exception, S3 origin can't use regional edge location. This is used by all other origins (custom origins) 
- cloudfront integrates with ACM (AWS certificate manager) for https. Hence, that can be resolved faster.
- cloudfront edge location only used for downloading (caching) part. All upload tasks goes directly to requested origin.
- cloudfront performs no write operation for caching.
- **exam imp**
  - The distribution contains the configuration deployed to the edge locations.
  - Every distribution can be configured for behaviours
  - Origins are used by behaviours as content sources
  - A distribution can have one or many behaviours which are configured with a path pattern. but the **precedence** level decides which one gets priority.
  - If requests match that pattern - that behaviour is used .. otherwise the default.
  - Other behaviours that can be configured are, Origins, Origin groups, TTL, protocol policies, restricted access (privacy settings) are configured via behaviours.
 
 ### Cloudfront behaviours
 - Price class depends on your edge location selections. (example, all or USA, canada, etc)
 - Cloudfront allows to select various security policies, example TLSv1, TLSv1.2 etc, There are various protocols and ciphers associated to each policy.
 - **exam imp** -- cloudfront allows you to restrict viewer access using signed URLs or Signed cookies. This selection also requires you to select **Trusted Signers**, and only those trusted entities would be allowed.

### TTL and cache Invalidations
- how CloudFront handles object expiry and invalidation
- **exam imp**
- More frequent cache HITS = lower origin load
- Default TTL (behaviour) = 24 hours (validity period)
- You can set Minimum TTL and Maximum TTL values
- Origin Header: Cache-control max-age (seconds)
- origin header: Cache-Control s-maxage (seconds)
- Origin Header: Expires (Date and Time)
- Custom Origin or S3 (via object metadata)

### Cache invalidation
- **exam imp** its performed on a distribution level
- **exam imp** it applies to all edge locations ... and it takes some time to show affect
- patterns can be used to perform invalidations, example /images/\*, /images/whiskers1.jpg, etc
- Invalidation incur cost and its done per request and new object caching will also incur cost, hence should be planned accordingly
- If your file updates regularly or frequently, then a better way is to use **exam imp ---- versioned file name **
  - example, whiskers1_v1.jpg, whiskers1_v2.jpg, whiskers1_v3.jpg
  - and modify application code to point to the respective objects
  - This will avoid unwanted caching and invalidation cost
- Remember, this versioning of object is different from S3 versioning,
  - in S3 object versioning, object name is same, but under the hood S3 creates versions for the same object
  - in cloudfront, you use different object names, to avoid invalidation.

### CloudFront and SSL/TLS & SNI
- SSL certificate is a way to authenticate that you own a specific domain that you claim you want to use in cloudfront
- This also proof on internet that your domain is secure for any users to access your application
- **exam imp** for cloudfront if you want to add any SSL/TLS certificate, it should always needs to be added in us-east-1 region, why becoz cloudfront is global service. Its not regional service.
- on the other hand, normally, if you distribute your application in multiple regions, then you need to generate or import your SSL/TLS cert to individual region and use it through ACM or some other 3rd part cert manager.
- Remember, if you use cloudfront with ACM, certificate must be in us-east-1 region
- cloudfront always provides default domain name that can be configured as CNAME in the R53, if needed.
- https://6976jhlkjjk.cloudfront.net
- **exam imp** SSL supported by default by cloudfront..... \*cloudfront.net cert
- http or https, http ==> https, https only
- every cloudfront has Two part SSL connections: viewer ==> cloudfront and cloudfront => origin, meaning traffic always flows through cloudfront.
- **exam imp** -- important to remember that both above parts need **valid public certificates and intermediate certificate**
- remember here, self-signed certificate will not work with cloudfront in this case, they need to be **publicly trusted certificate**
- how Pricing work for SSL over cloudfront (SNI helps in this)

- SNI
  - Server Name Indication (SNI) allows the server to safely host multiple TLS Certificates for multiple sites, all under a single IP address. It adds the hostname of the server (website) in the TLS handshake as an extension in the CLIENT HELLO message.
  - Server Name Indication is an extension to the Transport Layer Security computer networking protocol by which a client indicates which hostname it is attempting to connect to at the start of the handshaking process.
- old browsers don't support SNI.. Cloudfront charges extra for dedicated IP
- but if you use SNI, its free as part of the product
- SNI gets support in almost all modern browsers, and SSL/TLS helps in identifying application security in public internet
- Certificate issued by trusted certificate authority (CA) must match the DNS name used by application
- Origins need to have certificates issued by a trusted authority (CA).
  - in case of S3 origins handle certificates natively. Hence, no need to implement it seperately
  - In case of ALB its needs and can be done using ACM
  - In case of EC2 or other custom origins, external generated cert needs to be used, and no self-signed certs used.






