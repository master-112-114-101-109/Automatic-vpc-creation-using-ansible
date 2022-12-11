# Automatic-vpc-creation-using-ansible
_*Create an entire VPC  in aws with pairs of public and private subnets based on the available AZ of the AWS region*_

Here I am sharing an ansible playbook that will create a custom VPC(Virtual Private Cloud) in AWS which will contain equal number of public and private subnets based on the total number of Availability Zones in the provided AWS region.

#### Pre-requisites 

- Free tier AWS account
- An EC2 instance as Ansible master 
- IAM role attached to the Ansible master with required privileges to execute the intended tasks

## IMPORTANT
## This setup will cost you money if left running for long as the VPC includes elastic IP and NAT gateway.
__ __ __

#### Before running this playbook, make sure to change the variable values in vpc.vars as per your requirements.
```sh
aws_region: "Name of the region where you wish to deploy this VPC"
vpc_name: "VPC name"
vpc_cidr_block: IP address in CIDR format
```


Running the playbook will check the region you have specified and create N number of public-private subnet pair where N is the total number of AZ available in that particular region.
__ __ __

> For reference, 
> if the region is ap-south-1 , then there will be 
- 1 VPC
- 3 public subnets
- 3 private subnets
- 1 Internet gateway
- 1 Public route table with public subnet associations and global traffic routed through the Internet gateway
- 1 Elastic IP
- 1 NAT gateway 
- 1 Private route table with private subnet associations and global traffic routed through the NAT gateway.
