VPC = Virtual Private Cloud

Concepts: https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html

Difference between an egress-only internet gateway and an NAT gateway: An egress-only internet gateway is for use with IPv6 traffic only. To enable outbound-only internet communication over IPv4, use a NAT gateway instead. 
[(Source)](https://docs.aws.amazon.com/vpc/latest/userguide/egress-only-internet-gateway.)

Difference between a NAT gateway and a NAT instance: A NAT gateway is a managed AWS service that allows EC2 instances in private subnets to connect to the internet, other VPCs, or on-premises networks. A NAT instance is an EC2 instance in a public subnet that allows instances in private subnets to connect to the internet, other VPCs, or on-premises networks.
