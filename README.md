CloudFormation Template for VPC with Public and Private Subnets

Overview
This CloudFormation template provisions a Virtual Private Cloud (VPC) with the following architecture:

2 Public Subnets: Located in different availability zones.
2 Private Subnets: Located in different availability zones.
Route Tables:
Public Route Table with an Internet Gateway for internet access.
Private Route Table with a NAT Gateway for outbound internet access for private subnets.
Internet Gateway (IGW): Enables public subnets to communicate with the internet.
NAT Gateway: Allows private subnets to connect to the internet without exposing their instances publicly.

Resources Provisioned
Networking Resources
VPC:

CIDR Block: 10.0.0.0/16
Subnets:

Public Subnets:
CftPub1: 10.0.0.0/24 in Availability Zone us-east-1a
CftPub2: 10.0.2.0/24 in Availability Zone us-east-1b
Private Subnets:
CftPrv1: 10.0.1.0/24 in Availability Zone us-east-1a
CftPrv2: 10.0.3.0/24 in Availability Zone us-east-1b
Internet Gateway:

Connects public subnets to the internet.
NAT Gateway:

Placed in the first public subnet (CftPub1) to allow private subnets to access the internet securely.
Route Tables:

Public Route Table with a route to the Internet Gateway.
Private Route Table with a route to the NAT Gateway.


Architecture Diagram

VPC (10.0.0.0/16)
├── Public Subnet 1 (10.0.0.0/24) - IGW
├── Public Subnet 2 (10.0.2.0/24) - IGW
├── Private Subnet 1 (10.0.1.0/24) - NAT Gateway
└── Private Subnet 2 (10.0.3.0/24) - NAT Gateway

Prerequisites
AWS CLI: Install and configure the AWS CLI on your system.
CloudFormation Service: Ensure you have permissions to use AWS CloudFormation and create the required resources (VPC, subnets, NAT Gateway, etc.).
IAM Permissions: Your IAM user/role should have permissions to manage VPCs, subnets, route tables, internet gateways, NAT gateways, and EIPs.

Usage

Clone this repository to your local system:
git clone <repository-url>
cd <repository-folder>

Deploy the CloudFormation template using the AWS CLI:

aws cloudformation create-stack --stack-name my-vpc-stack --template-body file://template.yaml --capabilities CAPABILITY_NAMED_IAM

Monitor the stack creation

aws cloudformation describe-stacks --stack-name my-vpc-stack

Once the stack is successfully created, you can view the provisioned resources in the AWS Management Console under the VPC service.

Cleanup
To delete the stack and all its resources, run:

aws cloudformation delete-stack --stack-name my-vpc-stack





