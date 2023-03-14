## Project Title - Deploy a high-availability web app using CloudFormation

This repo contains Cloud Formation Templates to deploy infrastructure shown below: a highly available web site on AWS

![image](https://user-images.githubusercontent.com/99427790/224475443-b62e377a-b33e-4f3b-8738-79654af6e2db.png)


### Dependencies
##### 1. AWS account
You would require to have an AWS account to be able to build cloud infrastructure.

##### 2. VS code editor
An editor would be helpful to visualize the image as well as code. Download the VS Code editor [here](https://code.visualstudio.com/download).

##### 3. An account on www.lucidchart.com
A free user-account on [www.lucidchart.com](www.lucidchart.com) is required to be able to draw the web app architecture diagrams for AWS.

## Project Requirements
### Server specs
	- You'll need to create a Launch Configuration for your application servers in order to deploy four servers, two located in each of your private subnets. The launch configuration will be used by an auto-scaling group.
	- You'll need two vCPUs and at least 4GB of RAM. The Operating System to be used is Ubuntu 18. So, choose an Instance size and Machine Image (AMI) that best fits this spec.
	- Be sure to allocate at least 10GB of disk space so that you don't run into issues. 
	
### Security Groups and Roles
	- Since you will be downloading the application archive from an S3 Bucket, you'll need to create an IAM Role that allows your instances to use the S3 Service.(Optional)
	- The App communicates on the default HTTP Port: 80, so your servers will need this inbound port open since you will use it with the Load Balancer and the Load Balancer Health Check. As for outbound, the servers will need unrestricted internet access to be able to download and update their software.
	- The load balancer should allow all public traffic (0.0.0.0/0) on port 80 inbound, which is the default HTTP port. Outbound, it will only be using port 80 to reach the internal servers.
	- The application needs to be deployed into private subnets with a Load Balancer located in a public subnet.
	- One of the output exports of the CloudFormation script should be the public URL of the LoadBalancer.

### Other Considerations
	- You can deploy your servers with an SSH Key into Public subnets while you are creating the script. This helps with troubleshooting. Once done, move them to your private subnets and remove the SSH Key from your Launch Configuration.
	- It also helps to test directly, without the load balancer. Once you are confident that your server is behaving correctly, increase the instance count and add the load balancer to your script.
	- While your instances are in public subnets, you'll also need the SSH port open (port 22) for your access, in case you need to troubleshoot your instances.
	- Log information for UserData scripts is located in this file: cloud-init-output.log under the folder: /var/log.
	- You should be able to destroy the entire infrastructure and build it back up without any manual steps required, other than running the CloudFormation scr
	- 
	- into your private subnet servers. This bastion host would be on a Public Subnet with port 22 open only to your home IP address, and it would need to have the private key that you use to access the other servers.
	
	
	
	
### How to Create Stack
To deploy any of the templates, use the command below upon successfully logging in to the aws cli

```
aws cloudformation create-stack \
	--stack-name "stackName" \
	--template-body file://network-infrastructure.yml \
	--parameters file://network-parameters.json \
	--region=us-east-1 \
	--capabilities "CAPABILITY_IAM" "CAPABILITY_NAMED_IAM"
```
