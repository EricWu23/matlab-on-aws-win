# MATLAB on Amazon Web Services

This repository shows how to deploy MATLAB&reg; on an Amazon EC2&reg; instance using your Amazon&reg; Web Services (AWS&reg;) account and connect to it using the Remote Desktop Protocol (RDP), SSH, or NICE DCV. The automation uses an AWS CloudFormation template. 

For information about the architecture of this solution, see [Learn about Architecture](#learn-about-architecture). For information about templates, see [AWS CloudFormation Templates](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-guide.html).

This reference architecture has been reviewed and qualified by AWS.

![AWS Qualified Software badge](img/aws-qualified-software.png)


## Requirements
You need:
* A MATLAB license. For more information, see [License Requirements for MATLAB on Cloud Platforms](https://www.mathworks.com/help/install/license/licensing-for-mathworks-products-running-on-the-cloud.html).
* An [Amazon Web Services (AWS)](https://aws.amazon.com) account.
* A key pair for your AWS account, in the appropriate region. For more information, see [Amazon EC2 Key Pairs](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html).


## Costs
You are responsible for the cost of the AWS services used when you create cloud resources using this guide. Resource settings, such as instance type, affect the cost of deployment. For cost estimates, see the pricing pages for each AWS service you will be using. Prices are subject to change.

# Deployment Steps

To view instructions for deploying the MATLAB reference architecture, select a MATLAB release:

| Linux | Windows |
| ----- | ------- |
| [R2024a](https://github.com/mathworks-ref-arch/matlab-on-aws/tree/master/releases/R2024a/README.md) | [R2024a](releases/R2024a/README.md) |
| [R2023b](https://github.com/mathworks-ref-arch/matlab-on-aws/tree/master/releases/R2023b/README.md) | [R2023b](releases/R2023b/README.md) |
| [R2023a](https://github.com/mathworks-ref-arch/matlab-on-aws/tree/master/releases/R2023a/README.md) | [R2023a](releases/R2023a/README.md) |
| [R2022b](https://github.com/mathworks-ref-arch/matlab-on-aws/tree/master/releases/R2022b/README.md) | [R2022b](releases/R2022b/README.md) |
| [R2022a](https://github.com/mathworks-ref-arch/matlab-on-aws/tree/master/releases/R2022a/README.md) | [R2022a](releases/R2022a/README.md) |
| [R2021b](https://github.com/mathworks-ref-arch/matlab-on-aws/tree/master/releases/R2021b/README.md) | [R2021b](releases/R2021b/README.md) |
| [R2021a](https://github.com/mathworks-ref-arch/matlab-on-aws/tree/master/releases/R2021a/README.md) | [R2021a](releases/R2021a/README.md) |
| [R2020b](https://github.com/mathworks-ref-arch/matlab-on-aws/tree/master/releases/R2020b/README.md) | [R2020b](releases/R2020b/README.md) |
| [R2020a](https://github.com/mathworks-ref-arch/matlab-on-aws/tree/master/releases/R2020a/README.md) |  |
| [R2019b](https://github.com/mathworks-ref-arch/matlab-on-aws/tree/master/releases/R2019b/README.md) |  |
| [R2019a\_and\_older](https://github.com/mathworks-ref-arch/matlab-on-aws/tree/master/releases/R2019a_and_older/README.md) |  |


The above instructions allow you to launch instances based on the latest MathWorks&reg; Amazon Machine Images (AMIs).
MathWorks periodically replaces older AMIs with new images.
For more details, see
[When are the MathWorks Amazon Machine Images updated?](#when-are-the-mathWorks-amazon-machine-images-updated)

## Learn about Architecture

![MATLAB on AWS Reference Architecture](img/aws-matlab-diagram.png)

Deploying this reference architecture sets up a single AWS EC2 instance containing MATLAB, a private VPC with an internet gateway, a private subnet, and a security group that opens the appropriate ports for SSH and RDP access.

The Amazon Machine Image (AMI) contains pre-installed drivers, and the following software:
* MATLAB, Simulink, toolboxes, and support for GPUs.
* Add-ons: several pretrained deep neural networks for classification, feature extraction, and transfer learning with Deep Learning Toolbox&trade;, including GoogLeNet, ResNet-50, and NASNet-Large.


### Resources

The following resources will be created as part of the CloudFormation Stack:

1. Security Group for SSH and RDP access
2. EC2 Instance

The following resources might be created, depending on your deployment configuration:

1. IAM role
2. A CloudWatch log group
3. An elastic IP address
4. A SSM document

## FAQ

### When are the MathWorks Amazon Machine Images updated?
The links in [Deployment Steps](#deployment-steps) launch instances based on the latest MathWorks
AMIs for at least the four most recent MATLAB releases. MATLAB releases occur twice each year.

For each MATLAB release, MathWorks periodically replaces the corresponding AMI with a newer AMI
that includes the latest MATLAB updates and important security updates of the base OS image.

When MathWorks replaces an AMI, the older AMI is deleted.
However, any running instances previously launched from the older AMI are not affected.
To continue using an older AMI, copy the AMI into your AWS account.
For more details on how to copy an AMI, see
[How do I copy the AMI?](#how-do-I-copy-the-ami)
For more details on how to customize the reference architectures to
deploy the copied AMI see [How do I customize the AMI?](#how-do-I-customize-the-ami)

### How do I save my changes in the AMI?
All your files and changes are stored locally on the virtual machine. They persist until you either terminate the virtual machine instance or delete the stack. Stopping the instance does not destroy the data on the instance. If you want your changes to persist outside the stack or before you terminate an instance, you need to:
* Copy your files to another location, or
* Create an image of the virtual machine.

### What happens to my data if I shut down the instance?
To minimize costs, you might want to shut down the instance when you are not using it. When the virtual machine is stopped, you are only charged for storage. To shut down an EC2 instance, locate it in the AWS web console, select the instance and choose “Instance State/Stop” from the “Actions” menu. You can restart it from the same menu. Any files or changes you make to the virtual machine will persist when you shut it down and will be present when you restart it. Shutting down the virtual machine and restarting it might change the public IP address and DNS name.  Inspecting the EC2 instance in the AWS console will reveal the new IP address and DNS name.

### How do I keep the same public IP address?
To avoid having to change the IP address between restarts, enable the **Keep public IP address the same** option during deployment. For more information, see (Elastic IP addresses)[https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html].

### How do I manage my EC2 quotas?
See [Amazon EC2 Service Quotas](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-resource-limits.html).

### How do I save or copy an AMI?
To save an AMI, locate the EC2 Instance in the AWS web console and select **Actions** > **Image** > **Create Image.**

To copy the AMI for a certain MATLAB version to a target region of your choice, follow these steps:
* Choose the MATLAB release that you want to copy from the Releases folder of this repository. Download and open the CloudFormation template .json file for that release.
* Locate the Mappings section in the CloudFormation template. Copy the AMI ID for one of the existing regions, for example, us-east-1.
* To copy the AMI to your target region, see [Copy an AMI](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/CopyingAMIs.html) in the AWS documentation.
* In the Mappings section of the CloudFormation template, add a new RegionMap pair corresponding to your target region. Insert the new AMI ID of the AMI in the target region.
* In your AWS Console, change your region to your target region. In the CloudFormation menu, select the **Create Stack > With new resources** option. Provide the modified CloudFormation template.

You can now deploy the AMI in your target region using the AMI that you copied.

### How do I customize the AMI?
You can customize a prebuilt AMI by launching the reference architecture, applying changes you want to the EC2 Instance (such as installing additional software, drivers, and files), then saving an image of that instance using the AWS Console. For more information, see [How do I save or copy an AMI?](#how-do-i-save-or-copy-an-ami). When you create a stack, replace the AMI ID in the CloudFormation template with the AMI ID of your customized image.

### How do I use a different license manager?
The AMI uses MathWorks Hosted License Manager by default. For information on how to use other license managers, see [MATLAB Licensing in the Cloud](https://www.mathworks.com/help/licensingoncloud/matlab-on-the-cloud.html).

# Technical Support
To request assistance or additional features, contact [MathWorks Technical Support](https://www.mathworks.com/support/contact_us.html).

----

Copyright 2018-2024 The MathWorks, Inc.

----