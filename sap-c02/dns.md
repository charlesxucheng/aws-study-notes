Route 53 main functions: domain registration, DNS routing, and health checking.

The name of every record in a hosted zone must end with the name of the hosted zone. 

Amazon Route 53 health checks monitor the health of your resources.

Routing Policies:
* Simple routing policy – Use to route internet traffic to a single resource that performs a given function for your domain, for example, a web server that serves content for the example.com website.
* Failover routing policy – Use when you want to configure active-passive failover.
* Geolocation routing policy – Use when you want to route internet traffic to your resources based on the location of your users.
* Geoproximity routing policy – Use when you want to route traffic based on the location of your resources and, optionally, shift traffic from resources in one location to resources in another.
* Latency routing policy – Use when you have resources in multiple locations and you want to route traffic to the resource that provides the best latency.
* Multivalue answer routing policy – Use when you want Route 53 to respond to DNS queries with up to eight healthy records selected at random.
* Weighted routing policy – Use to route traffic to multiple resources in proportions that you specify.

Amazon Route 53 divides its functionality into a control and a data plane. 
The control planes are optimized for data consistency, whereas the data planes are optimized for availability. 
For Route 53 public and private DNS and health checks, the control plane is located in the us-east-1 AWS Region and the data planes are globally distributed.

The total length of a domain name cannot exceed 255 bytes, including the dots.

You can migrate from another DNS provider and can import records
You can migrate a hosted zone to another AWS account
You can migrate from Route 53 to another registrar
You can also associate a Route 53 Hosted Zone with a VPC in another account

When you register a domain with Route 53, we automatically create a hosted zone for the domain, assign four name servers to the hosted zone, and then update the domain registration to use those name servers. 

If you delete the hosted zone for a domain, you need to create another hosted zone when you're ready to make the domain available on the internet.

You can protect your domain from DNS spoofing or a man-in-the-middle attack by configuring Domain Name System Security Extensions (DNSSEC), a protocol for securing DNS traffic.

To replace a hosted zone for a domain registered with Route 53, update the domain configuration to use the name servers for the new hosted zone. When you create a hosted zone, Route 53 assigns a set of four name servers to the hosted zone. If you delete a hosted zone and then create a new one, Route 53 assigns another set of four name servers. Typically, none of the name servers for the new hosted zone match any of the name servers for the previous hosted zone. If you don't update the domain configuration to use the name servers for the new hosted zone, the domain will remain unavailable on the internet.

You can transfer domain registration from another registrar to Amazon Route 53, from one AWS account to another, or from Route 53 to another registrar.

When you use a separate hosted zone to route traffic for a subdomain, you can use IAM permissions to restrict access to the hosted zone for the subdomain. (You can't use IAM to control access to individual records.)

You can delete a hosted zone only if there are no records other than the default SOA and NS records. 

You can use Amazon Route 53 to route traffic to a variety of AWS resources: Cloudfront distribution, EC2 instance, S3 bucket, Beanstalk, ELB load balancer, API Gateway API, Amazon Virtual Private Cloud interface endpoint, Amazon WorkMail.

## Routing traffic to Subdomain
 The NS record for a hosted zone identifies the name servers that respond to DNS queries for the domain or subdomain. To start using the records in the hosted zone for the subdomain to route internet traffic, you create a new NS record in the hosted zone for the domain (example.com), and give it the name of the subdomain (acme.example.com). For the value of the NS record, you specify the names of the name servers from the hosted zone for the subdomain.

 ## Health Checks
 * Health checks that monitor an endpoint
   * Route 53 has health checkers in locations around the world. 
   * Route 53 aggregates the data from the health checkers and determines whether the endpoint is healthy: If more than 18% of health checkers report that an endpoint is healthy, Route 53 considers it healthy.
   * Each health checker evaluates the health of the endpoint based on the response time and whether the endpoint responds to a number of consecutive health checks that you specify (the failure threshold)
 * Health checks that monitor other health checks (calculated health checks)
 * Health checks that monitor CloudWatch alarms
   * Route 53 monitors the data stream for the corresponding alarm instead of monitoring the alarm state. 

Amazon Route 53 **alias** records provide a Route 53–specific extension to DNS functionality. Alias records let you route traffic to selected AWS resources, such as CloudFront distributions and Amazon S3 buckets. They also let you route traffic from one record in a hosted zone to another record.

If you're routing traffic to resources that you can't create alias records for, such as EC2 instances, you create a record and a health check for each resource. Then you associate each health check with the applicable record. 

 When you configure an alias record to evaluate the health of a resource, you don't need to create a health check for the resource.

 In general, you should set Evaluate Target Health to Yes for all the alias records in a tree. If you set Evaluate Target Health to No, Route 53 continues to route traffic to the records that an alias record refers to even if health checks for those records are failing.

 Route 53 periodically checks the health of the endpoint that is specified in a health check; it doesn't perform the health check when the DNS query arrives.

 Records without a health check are always healthy.
 If no record is healthy, all records are healthy.
 Weighted records that have a weight of 0 - Route 53 considers the zero-weighted records if all the records that have a weight greater than 0 are unhealthy.

 Route 53 health checkers are outside the VPC. To check the health of an endpoint within a VPC by IP address, you must assign a public IP address to the instance in the VPC. You can also create an alarm for a Cloudwatch metric, and then create a health check based on the data stream for the alarm.

## Route 53 Resolver DNS Firewall
DNS Firewall provides protection for outbound DNS requests from your VPCs. A primary use of DNS Firewall protections is to help prevent DNS exfiltration of your data. 

You can use Firewall Manager to centrally configure and manage your DNS Firewall rule group associations for your VPCs across your accounts in AWS Organizations.

DNS Firewall processes rule groups for a VPC from the lowest numeric priority setting on up.

Each rule specifies one domain list and an action to take on DNS queries whose domains match the domain specifications in the list. 

Route 53 Resolver DNS Firewall is a Regional service. You can share rule groups between accounts, and use rule groups across your organization in AWS Organizations by managing them in AWS Firewall Manager policies.


