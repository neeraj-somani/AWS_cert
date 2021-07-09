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
  - A distribution can have one or many behaviours which are configured with a path pattern.
  - If requests match that pattern - that behaviour is used .. otherwise the default.
  - Other behaviours that can be configured are, Origins, Origin groups, TTL, protocol policies, restricted access (privacy settings) are configured via behaviours.
 
 ### Cloudfront behaviours
 - Price class depends on your edge location selections.
 - 
