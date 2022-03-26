VPC = Virtual Private Cloud

Concepts: https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html

**Difference between an egress-only internet gateway and an NAT gateway:** An egress-only internet gateway is for use with IPv6 traffic only. To enable outbound-only internet communication over IPv4, use a NAT gateway instead. 
[(Source)](https://docs.aws.amazon.com/vpc/latest/userguide/egress-only-internet-gateway.)

**Difference between a NAT gateway and a NAT instance:** A NAT gateway is a managed AWS service that allows EC2 instances in private subnets to connect to the internet, other VPCs, or on-premises networks. A NAT instance is an EC2 instance in a public subnet that allows instances in private subnets to connect to the internet, other VPCs, or on-premises networks.

**Carrier gateways:** For subnets in **Wavelength Zones**, this type of gateway allows inbound traffic from a telecommunication carrier network in a specific location and outbound traffic to a telecommunication carrier network and the internet.

**Prefix lists:** A collection of CIDR blocks that can be used to configure VPC security groups, VPC route tables, and AWS Transit Gateway route tables and can be shared with other AWS accounts using Resource Access Manager (RAM).

**Implicit Association with the Main Route Table:** You can explicitly associate a subnet with a particular route table. Otherwise, the subnet is implicitly associated with the main route table. 

The route table has:
 - Destination: The range of IP addresses where you want traffic to go (destination CIDR). 
- Target: The gateway, network interface, or connection through which to send the destination traffic; for example, an internet gateway.

If your route table has multiple routes, we use the most specific route that matches the traffic (longest prefix match) to determine how to route the traffic.

**Propagation:** allows a virtual private gateway to automatically propagate routes to the route tables without the need to manually enter VPN routes.

**Gateway route table:** associated with an internet gateway or virtual private gateway.

## Gateway Route Table
A route table can be associated with internet gateways or virtual private gateways. 

A gateway route table associated with an internet gateway supports routes with the following targets:
* The default local route
* A Gateway Load Balancer endpoint
* A network interface (eni) for a middlebox appliance

**A gateway load balancer endpoint** is a VPC endpoint in the service consumer VPC of a gateway load balancer located in the service provider VPC. Gateway Load Balancers enable you to deploy, scale, and manage virtual appliances, such as firewalls, intrusion detection and prevention systems, and deep packet inspection systems. (Choke point)

**The transit gateway** acts as a **Regional** virtual router for traffic flowing between its attachments, which can include **VPCs, VPN connections, AWS Direct Connect gateways, and transit gateway peering connections**.

The allowed CIDR block size of a VPC is between a /16 netmask (65,536 IP addresses) and /28 netmask (16 IP addresses). After you've created your VPC, you can associate secondary CIDR blocks with the VPC. 

**VPC sharing** allows multiple AWS accounts to create their application resources, such as EC2 instances and RDS databases into shared, centrally-managed virtual private clouds (VPCs).

VPC resources locations:
* **Availability Zones** are multiple, isolated locations within each Region.
* **Local Zones** allow you to place resources, such as compute and storage, in multiple locations closer to your end users. When you create a subnet in a Local Zone, you extend the VPC to that Local Zone.
  * A **network border group** is a unique set of Availability Zones or Local Zones from which AWS advertises public IP addresses. IP addresses cannot move between network border groups.
  * Local Zones can have IGW. 
  * Local zones can use a virtual private gateway to connect to a Direct Connect gateway and reach on-prem network.
  * You can't create a transit gateway attachment for a subnet in a Local Zone. It has to go through other subnets in the parent AZ.
* **AWS Outposts** brings native AWS services, infrastructure, and operating models to virtually any data center, co-location space, or on-premises facility.
  * The subnets in AWS Outpost must reside in one Outpost location.
  * A **Local Gateway** handles the network connectivity between your VPC and on-premises networks. 
* **Wavelength Zones** allow developers to build applications that deliver ultra-low latencies to 5G devices and end users. Wavelength deploys standard AWS compute and storage services to the edge of telecommunication carriers' 5G networks. When you create a subnet in a Wavelength Zone, you extend the VPC to that Wavelength Zone.
  * You can create EC2 instances, EBS volumes, and carrier gateways in Wavelength Zones. You can also use services that orchestrate or work with EC2, EBS, and VPC such as EC2 Auto Scaling, EKS, ECS, EC2 Systems Manager, CloudWatch, CloudTrail, and CloudFormation.
  * You can't create a transit gateway attachment for a subnet in a Wavelength Zone. It has to go through other subnets in the parent AZ.
  * EC2 instances in different Wavelength Zones in the same VPC are not allowed to communicate with each other. If you need Wavelength Zone to Wavelength Zone communication, AWS recommends that you use multiple VPCs, one for each Wavelength Zone. You can use a transit gateway to connect the VPCs. 

# DNS Related
Each VPC has a default DHCP options set that contains the following network configurations:
* DNS server: The DNS name servers that your network interfaces will use for domain name resolution.
* Domain name: The domain name that EC2 instances in the VPC will use in their private hostnames.

AmazonProvidedDNS is an Amazon Route 53 Resolver server.

When you launch an instance, it always receives a private IPv4 address and a private DNS hostname that corresponds to its private IPv4 address.
* Private IP DNS name (IPv4 only): The IPBN-based (legacy scheme) IPv4 DNS hostname that includes the private IPv4 address. You can use the Private IP DNS name (IPv4 only) hostname for communication between instances in the same network, but we can't resolve the DNS hostname outside the network that the instance is in. Example: ip-10-24-34-0.ec2.internal, ip-10-24-34-0.us-west-2.compute.internal
* Private resource DNS name: The RBN-based DNS name that includes the EC2 instance id. When used as the Private DNS hostname, it can return both the Private IPv4 address (A record) and/or the IPv6 Global Unicast Address (AAAA record). Example: i-0123456789abcdef.ec2.internal

To access the resources in your VPC using custom DNS domain names, such as example.com, instead of using private IPv4 addresses or AWS-provided private DNS hostnames, you can create a **private hosted zone in Route 53**. A private hosted zone is a container that holds information about how you want to route traffic for a domain and its subdomains within one or more VPCs without exposing your resources to the internet. 

