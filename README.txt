# Deploy a high-availability web app using CloudFormation

## Architecture Overview
The following diagram shows the infrastructure setup of this project.

Infra_Diagram_Udagram.PNG


## Deployment

### Create Stack
Network and service stacks need to be created in subsequent order.

#### Create Network Stack
aws cloudformation create-stack --stack-name udagramNetwork1Abhinav --region us-east-1 --template-body file://udagram_network.yml --parameters file://udagram_network_parameters.json --capabilities "CAPABILITY_IAM" "CAPABILITY_NAMED_IAM"

#### Create Service Stack
aws cloudformation create-stack --stack-name udagramServer1Abhinav --region us-east-1 --template-body file://servers.yml --parameters file://server_parameters.json --capabilities "CAPABILITY_IAM" "CAPABILITY_NAMED_IAM"


### Update Stack

#### Update Network Stack
aws cloudformation update-stack --stack-name udagramNetwork1Abhinav --region us-east-1 --template-body file://udagram_network.yml --parameters file://udagram_network_parameters.json --capabilities "CAPABILITY_IAM" "CAPABILITY_NAMED_IAM"


#### Update Service Stack
aws cloudformation update-stack --stack-name udagramServer1Abhinav --region us-east-1 --template-body file://servers.yml --parameters file://server_parameters.json --capabilities "CAPABILITY_IAM" "CAPABILITY_NAMED_IAM"


### Delete Stacks
aws cloudformation delete-stack --stack-name udagramNetwork1Abhinav
aws cloudformation delete-stack --stack-name udagramServer1Abhinav

## Test the deployment
Once the CFN scripts succeeded there will be an output named `WebAppLoadBalancerDnsName` generated in the service Cloud Formation stack. This output points to the Load Balancer's DNS name which can be pasted into a browser.

URL to verify installation: `http://uda-p-webap-1bl80mxoqtza-1156059490.eu-central-1.elb.amazonaws.com/`
