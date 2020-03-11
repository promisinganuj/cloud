### What are endpoints?
* Endpoints are virtual devices.
* They are horizontally scaled, redundant, and highly available VPC components.
* They allow communication between instances in your VPC and services without imposing availability risks or bandwidth constraints on your network traffic.

### What is VPC endpoint?
* A VPC endpoint enables you to privately connect your VPC to supported AWS services and VPC endpoint services powered by AWS PrivateLink without requiring an internet gateway, NAT device, VPN connection, or AWS Direct Connect connection. 
* Instances in your VPC do not require public IP addresses to communicate with resources in the service.
* Traffic between your VPC and the other service does not leave the Amazon network.

### What are the different types of Endpoints?
#### Gateway Endpoint
* A gateway endpoint is a gateway that you specify as a target for a route in your route table for traffic destined to a supported AWS service.
* References specific service in specific region
* Only supports S3 and DynamoDB

#### Interface Endpoint
* An interface endpoint is an elastic network interface (ENI) with a private IP address from the IP address range of your subnet that serves as an entry point for traffic destined to a supported service.
* An interface VPC endpoint (interface endpoint) enables you to connect to services powered by AWS PrivateLink. This includes:
1. Some AWS services
2. Services hosted by other AWS customers and Partners in their own VPCs (referred to as VPC endpoint services)
3. Supported AWS Marketplace Partner services
