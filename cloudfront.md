
# Use Cases
When you add field-level encryption, you can protect specific data throughout system processing in addition to HTTPS security, so that only certain applications at your origin can see the data.

Running serverless code at the edge 

Using Lambda@Edge can help you configure your CloudFront distribution to serve private content from your own custom origin, in addition to using signed URLs or signed cookies.

The CloudFront managed prefix list contains the IP address ranges of all of CloudFront's globally distributed origin-facing servers. If your origin is hosted on AWS and protected by an Amazon VPC security group, you can use the CloudFront managed prefix list to allow inbound traffic to your origin only from CloudFront's origin-facing servers, preventing any non-CloudFront traffic from reaching your origin.

# Cache Behavior
A cache behavior lets you configure a variety of CloudFront functionality for a given URL path pattern for files on your website.  The functionality that you can configure for each cache behavior includes:
* The path pattern.
* If you have configured multiple origins for your CloudFront distribution, which origin you want CloudFront to forward your requests to.
* Whether to forward query strings to your origin.
* Whether accessing the specified files requires signed URLs.
* Whether to require users to use HTTPS to access those files.
* The minimum amount of time that those files stay in the CloudFront cache regardless of the value of any Cache-Control headers that your origin adds to the files.

When you create a new distribution, you specify settings for the default cache behavior, which automatically forwards all requests to the origin that you specify when you create the distribution. After you create a distribution, you can create additional cache behaviors that define how CloudFront responds when it receives a request for objects that match a path pattern. 

When you create a cache behavior, you specify the one origin from which you want CloudFront to get objects. As a result, if you want CloudFront to distribute objects from all of your origins, you must have at least as many cache behaviors (including the default cache behavior) as you have origins.

# CloudFront Distribution Configuration
* Origin settings
* Cache behavior settings - A cache behavior lets you configure a variety of CloudFront functionality for a given URL path pattern for files on your website.
* Distribution settings - apply to the entire distribution.
* Custom error pages and error caching
* Restrictions - If you need to prevent users in selected countries from accessing your content (blacklist or whitelist)

# Customize CloudFront with Policies
* With a CloudFront cache policy, you can specify the HTTP headers, cookies, and query strings that CloudFront includes in the cache key. You can also use the cache policy to specify time to live (TTL) and cache compressed settings.
* With an origin request policy you can include additional values in origin requests without including them in the cache key, in addition to all of the values in the cache policy
* With a CloudFront response headers policy, you can specify the HTTP headers that CloudFront adds to HTTP responses to viewers.

# Configuring secure access and restricting access to content
* Configure HTTPS connections
* Prevent users in specific geographic locations from accessing content
* Require users to access content using CloudFront signed URLs or signed cookies
* Set up field-level encryption for specific content fields
* Use AWS WAF to control access to your content

# Using signed URLs and signed cookies
When you create signed URLs or signed cookies, you use the private key from the signer’s key pair to sign a portion of the URL or the cookie. When someone requests a restricted file, CloudFront compares the signature in the URL or cookie with the unsigned URL or cookie, to verify that it hasn’t been tampered with. CloudFront also verifies that the URL or cookie is valid, meaning, for example, that the expiration date and time hasn’t passed.

When you specify a signer, you also indirectly specify the files that require signed URLs or signed cookies by adding the signer to a cache behavior. A signer is either a trusted key group that you create in CloudFront (recommended because it does not require the use of root user), or an AWS account that contains a CloudFront key pair. 

# Optimizing Caching and Availability
Ways to improve cache hit ratio:
* Specifying how long CloudFront caches your objects (Expiry/max-age/TTL settings)
* Using Origin Shield
* Caching based on query string parameters
* Caching based on cookie values
  * Amazon S3 and some HTTP servers don’t process cookies.
* Caching based on request headers
* Remove Accept-Encoding header when compression is not needed
* Serving media content by using HTTP

You can set up CloudFront with origin failover and origin groups for scenarios that require high availability. 
