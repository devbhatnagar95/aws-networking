
# AWS Multi-VPC Architecture Deployment

This repository contains an AWS CloudFormation template to deploy a multi-VPC architecture as described in the provided architectural diagram. The architecture includes separate VPCs for Web, Shared, and Transit purposes, along with various subnets, NAT gateways, and simulated on-premises networks.

## Table of Contents

- [Architecture Overview](#architecture-overview)
- [Prerequisites](#prerequisites)
- [Template Structure](#template-structure)
- [Deployment Instructions](#deployment-instructions)
- [Customizing the Template](#customizing-the-template)
- [Troubleshooting](#troubleshooting)
- [License](#license)

## Architecture Overview

The deployed architecture includes:
- **Web VPC:** Hosts a web server in a public subnet with internet access.
- **Shared VPC:** Contains a NAT gateway and a database server in private subnets.
- **Transit VPC:** Serves as a central routing hub with a simulated Cloud Service Router.
- **On-Premises Networks:** Simulated using EC2 instances representing routers and servers in Charleston and Atlanta.

## Prerequisites

Before deploying the CloudFormation stack, ensure you have the following:
- **AWS CLI** installed and configured with sufficient permissions to create resources (EC2, VPC, Subnets, NAT Gateway, etc.).
- **AWS account** with access to create CloudFormation stacks.
- **IAM permissions** to create and manage VPCs, subnets, and associated resources.

## Template Structure

- **`architecture.yaml`:** The main CloudFormation template that defines the AWS resources and architecture.

## Deployment Instructions

### Deploying via AWS Console

1. Clone this repository to your local machine:
   ```bash
   git clone https://gitlab.com/yourusername/aws-multi-vpc-architecture.git
   cd aws-multi-vpc-architecture
   ```

2. Navigate to the AWS CloudFormation console.

3. Click **Create Stack** and select **Upload a template file**.

4. Upload the `architecture.yaml` file.

5. Follow the on-screen instructions to deploy the stack.

### Deploying via AWS CLI

1. Clone this repository to your local machine:
   ```bash
   git clone https://gitlab.com/yourusername/aws-multi-vpc-architecture.git
   cd aws-multi-vpc-architecture
   ```

2. Deploy the CloudFormation stack using the AWS CLI:
   ```bash
   aws cloudformation deploy --template-file architecture.yaml --stack-name my-aws-architecture --capabilities CAPABILITY_NAMED_IAM
   ```

3. Monitor the stack creation process in the AWS CloudFormation console.

## Customizing the Template

To customize the architecture:
- **Modify CIDR Blocks:** Update the `CidrBlock` values in the template to match your networking requirements.
- **Add/Remove Resources:** Modify the `Resources` section of the `architecture.yaml` file to add or remove AWS resources as needed.
- **Change Instance Types:** Adjust the `InstanceType` property of the EC2 instances to suit your performance needs.

### Example: Adding a New Subnet

To add a new subnet in the Web VPC:

1. Locate the **Web VPC** section in the `architecture.yaml` file.
2. Add a new subnet resource, for example:
   ```yaml
   WebAppSubnet:
     Type: "AWS::EC2::Subnet"
     Properties:
       VpcId: !Ref WebVPC
       CidrBlock: "10.1.1.0/24"
       MapPublicIpOnLaunch: true
       Tags:
         - Key: Name
           Value: "web-app-subnet"
   ```

## Troubleshooting

- **Stack Creation Failures:** Check the AWS CloudFormation console for error messages and troubleshoot accordingly.
- **Resource Limits:** Ensure your AWS account has sufficient resource limits (VPCs, subnets, EC2 instances) to create the architecture.

## License

This project is licensed under the MIT License.
