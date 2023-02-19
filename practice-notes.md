Identity Federation with SAML 2.0 enables federated single sign-on (SSO), so users can log in to the AWS Management Console or call the AWS API operations without you having to create an IAM user for everyone in your organization.

AWS SSO supports single sign-on to business applications through web browsers only. AWS SSO supports only SAML 2.0–based applications. A SAML 2.0-based federation doesn't use social media logins.

You can use trusted access to enable an AWS service that you specify, called the trusted service, to perform tasks in your organization and its accounts on your behalf. This involves granting permissions to the trusted service but does not otherwise affect the permissions for IAM users or roles. When you enable access, the trusted service can create an IAM role called a service-linked role in every account in your organization. That role has a permissions policy that allows the trusted service to do the tasks that are described in that service's documentation. This enables you to specify settings and configuration details that you would like the trusted service to maintain in your organization's accounts on your behalf. Only the linked AWS service can assume a service-linked role, which is why you cannot modify the trust policy of a service-linked role.

AWS VM Import/Export does not support synching incremental changes from the on-premises environment to AWS. AWS SMS supports up to 16TB volumes. 

You create a AWS Systems Manager patch group by using Amazon EC2 tag key Patch Group. You should be tagging instances based on the environment and its OS type for patch groups. The AWS Systems Manager Maintenance Windows feature lets you define a schedule for when to perform potentially disruptive actions on your instances such as patching an operating system, updating drivers, or installing software or patches. It is not the least effort way for applying patches.

AWS Batch enables developers, scientists, and engineers to easily and efficiently run hundreds of thousands of batch computing jobs on AWS. AWS Batch dynamically provisions the optimal quantity and type of compute resources (e.g., CPU or memory optimized instances) based on the volume and specific resource requirements of the batch jobs submitted. => Suitable for HPC, digital media and entertainment related workload.

To connect to services such as EC2 using just Direct Connect you need to create a private virtual interface. However, if you want to encrypt the traffic flowing through Direct Connect, you will need to use the public virtual interface of DX to create a VPN connection that will allow access to AWS services such as S3, EC2, and other services. If you want to establish a virtual private network (VPN) connection from your company network to an Amazon Virtual Private Cloud (Amazon VPC) over an AWS Direct Connect (DX) connection, you must use a public virtual interface for your DX connection.

Large batch processing workflow => AWS Simple Workflow Service, define workflows and steps. Use Mechanical Turk if human action is required. To visualize the workflow state, process the logs using Lambda and OpenSearch and Kibana.

NACL is useful for responding to DDoS attacks because it lets you create your own rules to mitigate the attack when you know the source IPs or other signature.

Lex - Advanced deep learning functionalities of automatic speech recognition (ASR) for converting speech to text, and natural language understanding (NLU) to recognize the intent of the text. Chatbots.

Route 53 attributes enableDnsHostnames and enableDnsSupport are set to “TRUE” by default and are needed for VPC resources to query Route 53 zone entries.

For EC2, use a Type A Record without an Alias. For ELB, Cloudfront and S3, always use a Type A Record with an Alias. For RDS, always use the CNAME Record with no Alias.

To use a certificate with Elastic Load Balancing for the same site (the same fully qualified domain name, or FQDN, or set of FQDNs) in a different Region, you must request a new certificate for each Region in which you plan to use it. To use an ACM certificate with Amazon CloudFront, you must request the certificate in the US East (N. Virginia) region.

AWS Elemental MediaConnect is a high-quality transport service for live video. 

Polly - Text to Speech; Textract - OCR

Amazon CloudSearch is a managed service in the AWS Cloud that makes it simple and cost-effective to set up, manage, and scale a search solution for your website or application.

SSE-S3 provides strong multi-factor encryption in which each object is encrypted with a unique key. It also encrypts the key itself with a master key that it rotates regularly.

# Hybrid environment server management
* Use a Secure String data type in AWS Systems Manager Parameter Store for secrets. 
* Set up a new IAM role that enables access and decryption of the database credentials from SSM Parameter Store. 
* Install the AWS SSM agent on all servers. This allows SSM to manage both the EC2 and on-premise servers.
  * Associate this role to the EC2 instances. 
  * For the on-premises servers, create an IAM Service Role and associate it with the servers. 
* Deploy the application packages to the EC2 instances and on-premises servers using AWS CodeDeploy.



Amazon Rekognition makes it easy to add image and video analysis to your applications. - Pattern recognition


