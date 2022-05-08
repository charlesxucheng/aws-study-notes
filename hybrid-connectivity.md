# Client VPN



# Site-to-site VPN
A Site-to-Site VPN connection offers two VPN tunnels between a **virtual private gateway** or a **transit gateway** on the AWS side, and a customer gateway (which represents a VPN device) on the remote (on-premises) side. Both vgw and tg can have multiple Site-to-Site VPN connections to multiple on-premises locations. vpg can connect to on-premise network via **Direct Connect**. See [Architecture Diagrams](https://docs.aws.amazon.com/vpn/latest/s2svpn/Examples.html).

Virtual private gateway does not support IPv6.
Transit gateway can support either IPv4 (default) or IPv6 inside the VPN tunnels.

Your Site-to-Site VPN connection consists of two VPN tunnels for redundancy. AWS selects one of the two redundant tunnels as the primary egress path. For a virtual private gateway, one tunnel across all Site-to-Site VPN connections on the gateway will be selected. To use more than one tunnel, use Equal Cost Multipath (ECMP) on a transit gateway. AWS applies tunnel endpoint updates to one tunnel of your VPN connection at a time.

You can use pre-shared keys, or certificates to authenticate your Site-to-Site VPN tunnel endpoints.

You can create additional VPN connections from your on-premises location to other VPCs using the same customer gateway device or another device.

VPN CloudHub enables your remote sites to communicate with each other, and not just with the VPC. The VPN CloudHub operates on a simple hub-and-spoke model that you can use with or without a VPC. The sites must not have overlapping IP ranges.

## Accelration
 An accelerated Site-to-Site VPN connection uses AWS Global Accelerator to route traffic from your on-premises network to an AWS edge location that is closest to your customer gateway device. 
 
 Acceleration is only supported for Site-to-Site VPN connections that are attached to a transit gateway. Virtual private gateways do not support accelerated VPN connections. An Accelerated Site-to-Site VPN connection cannot be used with an AWS Direct Connect public virtual interface.

## Routing
 If your customer gateway device supports Border Gateway Protocol (BGP), specify dynamic routing. If your customer gateway device does not support BGP, specify static routing.

* If propagated routes from a Site-to-Site VPN connection or AWS Direct Connect connection **overlap** with the local route for your VPC, the local route is most preferred even if the propagated routes are more specific.

* If propagated routes from a Site-to-Site VPN connection or AWS Direct Connect connection have the **same destination CIDR block** as other existing static routes (longest prefix match cannot be applied), we prioritize the static routes whose targets are an internet gateway, a virtual private gateway, a network interface, an instance ID, a VPC peering connection, a NAT gateway, a transit gateway, or a gateway VPC endpoint.

