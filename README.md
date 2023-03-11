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


### How to Create Stack
To deploy any of the templates, use the command below upon successfully logging in to the aws cli

aws cloudformation create-stack \
	--stack-name "stackName" \
	--template-body file://network-infrastructure.yml \
	--parameters file://network-parameters.json \
	--region=us-east-1 \
	--capabilities "CAPABILITY_IAM" "CAPABILITY_NAMED_IAM"
