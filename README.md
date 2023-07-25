# Infrastructure as code (IaC) - Cloudformation

## Description

This repo contains AWS cloudformation YAML code for deploying a high-availability web application in AWS.

The architecture contains an internet gateway attached and a load balancer attached to a VPC, the web application
is deployed across two availability zones for high availability.
Each availability zone has public and private subnets, the application servers are in the private subnet and the 
jumpbox/bastion server and the NAT gateway are part of the public subnet. The application servers are auto-scaled.

## Technologies used

- AWS
- AWS cloudformation

## Architecture diagram
![arch-1](https://github.com/nikhil-31/django-docker-kubernetes-deploy-scripts/assets/19944703/82604d50-a92e-4695-a488-2c41726627b7)

## Getting started

1. Setup command line access to your AWS account with AWS CLI [link](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html).
2. In the `project.json` file set the values for `AMIforServer`, `AMIforJumpBox`, `KeyPairNameForServer`, `KeyPairNameForJumpBox`.
The values AMI can be from the free tier,and the KeyPair can be created from the EC2 console
3. The `index.html` file is zipped and uploaded to a s3 bucket as `index.zip`, the URL to the s3 bucket is part of the 
launch configuration on line 260 and has to be changed with the URL of your s3 bucket.
4. There are two helper scripts in the `/scripts` directory, check the usage section below.
5. After the cloudformation stack is successfully created go to the load balancer DNS name to view the web page 
rendered by `index.html`.

## Usage

1. Create the cloudformation stack using script `create.sh`
```
./scripts/create.sh {stack_name} {template} {parameters} 
```
Eg-
```
./scripts/create.sh stack1 project.yaml project.json 
```

2. Update the cloudformation stack using script `update.sh`

```
./scripts/update.sh stack1 project.yaml project.json 
```
The cloudformation stack must already exist

## License
Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at
http://www.apache.org/licenses/LICENSE-2.0 Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.

Copyright 2023 Nikhil Bhaskar

