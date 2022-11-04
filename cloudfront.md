
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
