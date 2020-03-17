## AWS Direct Connect (DX)

### DX - Features
* **Dedicated, private** fibre to AWS
* **Consistent** network performance compared to internet
* **Lower cost** data-out rates compared to internet data-out
* **Sharewable** service
* 1 Gbps and 10 Gbps service from AWS
* Service below 1 Gpbs can be purchased through an APN partner
* Supports Ethernet VPAN trunking
  * Your device must support 802.1Q VLANs
  * Supports a MTU (Maximum Transmission Unit) of up to 9001 bytes at the physical layer
* **Virtual interface(VIF)** built per VLAN on a connection
  * Sub-1 Gbps can have only 1 VIF
  * 1-10 Gbps can have up to 50 VIFs and may be more cost-effective
* External Border Gateway Protocol (eBGP) peering for route exchange
* Maximum of 4 links for LAG

## What is AWS Direct Connect ((DX)?
* AWS Direct Connect (DX) links your internal network to a DX location over a standard 1-gigabit or 10-gigabit Ethernet fiber-optic cable.
* One end of the cable is connected to your router, and the other is connected to a DX router.
* With this connection in place, you can create virtual interfaces directly to the AWS Cloud (for example, to Amazon EC2 and Amazon S3) and to Amazon VPC, bypassing internet service providers (ISPs) in your network path.
