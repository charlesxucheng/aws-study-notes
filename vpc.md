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
