# Client VPN
With Client VPN, VPN client connects to a VPN Endpoint in AWS. The VPN Endpoint is associated with client VPN network interfaces in each subnet, allowing access to the resources in the subnets. The VPN Endpoint performs NAT (SNAT).

Client VPN offers the following types of **client authentication**:
* Active Directory authentication (user-based)
  * Can use on-premises Active Directory with AD Connector
* Mutual authentication (certificate-based)
  * Uses AWS Certificate Manager
* Single sign-on (SAML-based federated authentication) (user-based)
  * Supports Okta and Microsoft AD

Client VPN supports two types of **client authorization**: security groups and network-based authorization (using authorization rules).

**Connection Authorization:** You can configure a client connect handler for your Client VPN endpoint. The handler enables you to run a lambda function that authorizes a new connection, based on device, user, and connection attributes.

**Split-tunnel** ensures that only traffic with a destination to the network matching a route from the Client VPN endpoint route table is routed over the Client VPN tunnel. Split tunnel can optimize routing and reduce data egress cost by routing traffic to AWS network only when required.

You can associate multiple subnets in different AZs with a Client VPN endpoint for high availability.

# Site-to-site VPN
A Site-to-Site VPN connection offers two VPN tunnels between a **virtual private gateway** or a **transit gateway** on the AWS side, and a customer gateway (which represents a VPN device) on the remote (on-premises) side. Both vgw and tg can have multiple Site-to-Site VPN connections to multiple on-premises locations. vpg can connect to on-premise network via **Direct Connect**. See [Architecture Diagrams](https://docs.aws.amazon.com/vpn/latest/s2svpn/Examples.html).

Virtual private gateway does not support IPv6.
Transit gateway can support either IPv4 (default) or IPv6 inside the VPN tunnels.

Your Site-to-Site VPN connection consists of two VPN tunnels for redundancy. AWS selects one of the two redundant tunnels as the primary egress path. For a virtual private gateway, one tunnel across all Site-to-Site VPN connections on the gateway will be selected. To use more than one tunnel, use Equal Cost Multipath (ECMP) on a transit gateway. AWS applies tunnel endpoint updates to one tunnel of your VPN connection at a time.

You can use pre-shared keys or certificates to authenticate your Site-to-Site VPN tunnel endpoints.

You can create additional VPN connections from your on-premises location to other VPCs using the same customer gateway device or another device.

There can only be one VGW attached to a VPC at a given time.

VPN CloudHub enables your remote sites to communicate with each other, and not just with the VPC. The VPN CloudHub operates on a simple hub-and-spoke model that you can use with or without a VPC. The sites must not have overlapping IP ranges.

## Acceleration
 An accelerated Site-to-Site VPN connection uses AWS Global Accelerator to route traffic from your on-premises network to an AWS edge location that is closest to your customer gateway device. 
 
 Acceleration is only supported for Site-to-Site VPN connections that are attached to a transit gateway. Virtual private gateways do not support accelerated VPN connections. An Accelerated Site-to-Site VPN connection cannot be used with an AWS Direct Connect public virtual interface.

## Routing
 If your customer gateway device supports Border Gateway Protocol (BGP), specify dynamic routing. If your customer gateway device does not support BGP, specify static routing.

* If propagated routes from a Site-to-Site VPN connection or AWS Direct Connect connection **overlap** with the local route for your VPC, the local route is most preferred even if the propagated routes are more specific.

* If propagated routes from a Site-to-Site VPN connection or AWS Direct Connect connection have the **same destination CIDR block** as other existing static routes (longest prefix match cannot be applied), we prioritize the static routes whose targets are an internet gateway, a virtual private gateway, a network interface, an instance ID, a VPC peering connection, a NAT gateway, a transit gateway, or a gateway VPC endpoint.

# Direct Connect
* A private VIF can be used to connect to a single VPC in the same AWS region using a private IP through a VGW.
* A public VIF can be used to connect to AWS public services **in any region** using a public IP.
* A transit VIF can be used to access one or more Amazon VPC Transit Gateways associated with Direct Connect gateways.

You can use a single connection in a public Region to access public AWS services in all other public Regions to build multi-Region services. 

Types of connections:
* Dedicated connections. Connection speed: 1 Gbps, 10 Gbps, and 100 Gbps.
* Hosted connection. Connection speed: From 50 Mbps to 10 Gbps

DX connections are not encrypted. IPSec Site-to-Site VPN or MACSec can be used over DX connections.

Hosted VIF shares bandwidth with other customers. It allows sharing of VIF to other accounts.

Need to understand better: https://docs.aws.amazon.com/directconnect/latest/UserGuide/routing-and-bgp.html

## Direct Connect Gateway
Use Direct Connect Gateway to connect to multiple VPCs. A Direct Connect Gateway can connect to transit gateways or VGWs. A Direct Connect gateway is a globally available resource. You can create the Direct Connect gateway in any Region and access it from all other Regions. Direct Connect Gateway can be associated to multiple accounts. 

You can attach multiple private virtual interfaces to your Direct Connect gateway. You cannot create a public virtual interface to a Direct Connect gateway. The VPCs to which you connect through a Direct Connect gateway cannot have overlapping CIDR blocks. 

You cannot attach a Direct Connect gateway to a transit gateway when the Direct Connect gateway is already associated with a virtual private gateway or is attached to a private virtual interface. A transit gateway can only be used with a 1 Gbps or faster Direct Connect connection.

## Link Aggregation Group
A link aggregation group (LAG) is a logical interface that uses the Link Aggregation Control Protocol (LACP) to aggregate multiple connections at a single AWS Direct Connect endpoint, allowing you to treat them as a single, managed connection. 
* All connections must be dedicated connections and have a port speed of 1 Gbps, 10 Gbps, or 100 Gbps.
* All connections in the LAG must use the same bandwidth.
* You can have a maximum of two 100G connections, or four connections with a port speed less than 100G in a LAG. 
* All connections in the LAG must terminate at the same AWS Direct Connect endpoint.
