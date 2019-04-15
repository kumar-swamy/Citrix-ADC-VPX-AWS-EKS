## About these CloudFormation templates
This CloudFormation template is provided to bring up a VPX instance with one ENI.  Users can re-use / modify or enhance the templates to suit their particular production and testing needs.
This CFT also provisions NSIP, VIP and SNIP. The Primary IP address will be marked as VIP such that multiple instances of VPX can be deployed and load-balanced using AWS classic loadbalancer.  This also creates a security group attached to the ENI of VPX  to  allow all TCP traffic on Port 22,80 and 443. Users can modify this to suit their requirements. 
>**Note:**
    >
    > This Cloud formation template has AMI IDs of Customer licensed BYOL ( Bring your own License ) Variant and 12.1 version. Read more about this [here](https://aws.amazon.com/marketplace/pp/B00AA01BOE?ref_=aws-mp-console-subscription-detail)
    > o use a different version / edition of the Citrix NetScaler VPX with a CloudFormation template requires the user to edit the template and replace the AMI Ids. You can read more about how to get AMI Ids [here]()
    
## Pre-requisites
The CloudFormation template requires sufficient permissions to create IAM roles, beyond normal EC2 full privileges. The user of this template also needs to [accept the terms and subscribe to the AWS Marketplace product](https://aws.amazon.com/marketplace/pp/FIXME/) before using this CloudFormation template.
<p>The following should be present</p>

- VPC connected to Internet Gateway
- 1 Public Subnet


## Input
`VpcId`: VPC where the VPX to be deployed.
`SubnetId`: Subnet Id where the VPX instance to be deployed.
`VPXInstanceType`: Instance type to be used for VPX EC2 instance
`VPXTenancyType`: Tenancy Type, Dedicated or Shared
`KeyName`: SSH Key name for accessing the VPX through SSH. 


## CloudFormation Template description
 The CloudFormation template  provisions a lambda function that initializes the VPX instance with NSIP, VIP and SNIP. Initial configuration performed by the lambda function includes network interface configuration, VIP configuration and feature configuration. Further configuration can be performed by logging in to the GUI or via SSH (username: nsroot and password is same as `InstanceIdNS`). The output of the CloudFormation template includes:

- `InstanceIdNS`. Instance Id of newly created VPX instance. This is the default password for the GUI / ssh access
- `ManagementURL`. Use this HTTPS URL to the Management GUI (uses self-signed cert) to login to the VPX and configure it further 
- `ManagementURL2`: Use this HTTP URL to the Management GUI (if your browser has problems with the self-signed cert) to login to the VPX 
- `PublicNSIp`: Use this public IP to ssh into the appliance 
- `PublicIpVIP`: The Public IP where load balanced applications can be accessed
- `PrivateNSIP`: The Private IP address which is used for Management of Citrix ADC. This is mapped to Public Elastic IP Address `PublicNSIp`
- `PrivateVIP`: The Private IP address which is used as Virtual IP for hosting the application. This is mapped to Public Elastic IP Address `PublicIpVIP`
- `SNIP`: The Private IP Address which is used for Backend communication for EKS pods. 
- `SecurityGroup`: Security group associated with the VPX ENI. 

## Quick Launch Links

- US-East-1 region
    [![Create NetScaler VPX Express](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=Citrix-ADC-12.1-VPX&templateURL=https://s3.amazonaws.com/citrix-adc-vpx-cft/citrix.adc.1nic.template)
- US-East-2 region
    [![Create NetScaler VPX Express](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=us-east-2#/stacks/new?stackName=Citrix-ADC-12.1-VPX&templateURL=https://s3.amazonaws.com/citrix-adc-vpx-cft/citrix.adc.1nic.template)
- US-West-1 region
    [![Create NetScaler VPX Express](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=us-west-1#/stacks/new?stackName=Citrix-ADC-12.1-VPX&templateURL=https://s3.amazonaws.com/citrix-adc-vpx-cft/citrix.adc.1nic.template)
- US-West-2 region
    [![Create NetScaler VPX Express](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks/new?stackName=Citrix-ADC-12.1-VPX&templateURL=https://s3.amazonaws.com/citrix-adc-vpx-cft/citrix.adc.1nic.template)
- CA-Central-1 region
    [![Create NetScaler VPX Express](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=ca-central-1#/stacks/new?stackName=Citrix-ADC-12.1-VPX&templateURL=https://s3.amazonaws.com/citrix-adc-vpx-cft/citrix.adc.1nic.template)
- CA-Central-1 region
    [![Create NetScaler VPX Express](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=ca-central-1#/stacks/new?stackName=Citrix-ADC-12.1-VPX&templateURL=https://s3.amazonaws.com/citrix-adc-vpx-cft/citrix.adc.1nic.template)
- EU-West-1 region
    [![Create NetScaler VPX Express](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=eu-west-1#/stacks/new?stackName=Citrix-ADC-12.1-VPX&templateURL=https://s3.amazonaws.com/citrix-adc-vpx-cft/citrix.adc.1nic.template)
- EU-West-2 region
    [![Create NetScaler VPX Express](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=eu-west-2#/stacks/new?stackName=Citrix-ADC-12.1-VPX&templateURL=https://s3.amazonaws.com/citrix-adc-vpx-cft/citrix.adc.1nic.template)
- EU-central-1 region
    [![Create NetScaler VPX Express](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=eu-central-1#/stacks/new?stackName=Citrix-ADC-12.1-VPX&templateURL=https://s3.amazonaws.com/citrix-adc-vpx-cft/citrix.adc.1nic.template)
- AP-South-1 region
    [![Create NetScaler VPX Express](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=ap-south-1#/stacks/new?stackName=Citrix-ADC-12.1-VPX&templateURL=https://s3.amazonaws.com/citrix-adc-vpx-cft/citrix.adc.1nic.template)
- AP-Northeast-1 region
    [![Create NetScaler VPX Express](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=ap-northeast-1#/stacks/new?stackName=Citrix-ADC-12.1-VPX&templateURL=https://s3.amazonaws.com/citrix-adc-vpx-cft/citrix.adc.1nic.template)
- AP-Northeast-2 region
    [![Create NetScaler VPX Express](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=ap-northeast-2#/stacks/new?stackName=Citrix-ADC-12.1-VPX&templateURL=https://s3.amazonaws.com/citrix-adc-vpx-cft/citrix.adc.1nic.template)
- AP-Southeast-1 region
    [![Create NetScaler VPX Express](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-1#/stacks/new?stackName=Citrix-ADC-12.1-VPX&templateURL=https://s3.amazonaws.com/citrix-adc-vpx-cft/citrix.adc.1nic.template)
- AP-Southeast-2 region
    [![Create NetScaler VPX Express](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-2#/stacks/new?stackName=Citrix-ADC-12.1-VPX&templateURL=https://s3.amazonaws.com/citrix-adc-vpx-cft/citrix.adc.1nic.template)
- SA-East-1 region
    [![Create NetScaler VPX Express](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=sa-east-1#/stacks/new?stackName=Citrix-ADC-12.1-VPX&templateURL=https://s3.amazonaws.com/citrix-adc-vpx-cft/citrix.adc.1nic.template)


## Additional Links:

- VPX installation in AWS :https://docs.citrix.com/en-us/citrix-adc/12-1/deploying-vpx/deploy-aws.html
- Citrix ADC 12.1 Documentation : https://docs.citrix.com/en-us/citrix-adc/12-1.html
- Citrix ADC Overview : https://www.citrix.com/products/netscaler-adc/resources/netscaler-vpx.html
