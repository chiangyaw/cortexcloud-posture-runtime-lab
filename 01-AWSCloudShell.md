# Cortex Cloud Hands-On Lab for Posture & Runtime Security
## Accessing Your AWS Account
As part of this workshop, you will need to have an AWS account, which can be either your own personal AWS account or utilize your corporate AWS account. You will need full admin access where you are able to provision the following:
- EKS Cluster
- Ubuntu EC2 Instance
- S3 Bucket with sensitive data
- Keypair to access the Ubuntu EC2 instance
- Required network infrastructure, including VPC, subnet, route table, security group, etc
- Required IAM roles for access and provisioning
Note: If you're using your personal AWS account, do take note that the resources are chargable, and Palo Alto Networks will not be responsible for any costs on your AWS account.

## Setting Up Your AWS Cloudshell
What is AWS Cloudshell? AWS CloudShell is a browser-based, pre-authenticated shell that you can launch directly from the AWS Management Console. You can navigate to CloudShell from the AWS Management Console a few different ways. For more information, you can always look into AWS tech doc [here](https://docs.aws.amazon.com/cloudshell/latest/userguide/welcome.html#:~:text=AWS%20CloudShell%20enables%20managing%20Lightsail,work%20with%20AWS%20Control%20Tower). You can run AWS CLI commands using your preferred shell, such as Bash and Powershell. 

You will be deploying the AWS resources on AWS Cloudshell with ```terraform``` and accessing the EKS cluster with ```kubectl```.

### What is terraform?
`terraform` is an open-source infrastructure-as-code (IaC) tool created by HashiCorp that allows users to define, create, change, and manage infrastructure components using declarative configuration files. It enables automation of infrastructure provisioning and management across various cloud providers and on-premises environments. 

### What is kubectl?
`kubectl` is the command-line interface (CLI) tool provided by Kubernetes for interacting with a Kubernetes cluster. It allows you to deploy applications, manage cluster resources, view logs, and more. Essentially, kubectl acts as a bridge between your local machine and the Kubernetes API server, enabling you to control and manage your cluster. 

1. Login to your AWS account, launch AWS Cloudshell by clicking the AWS Cloudshell icon on your AWS Management Console.
![](/resources/aws-cloudshell-01.png?raw=true)

2. As AWS Cloudshell is not pre-installed with ```terraform``` by default, you will need to install it manually. Install ```terraform``` with the following:
```
git clone https://github.com/tfutils/tfenv.git ~/.tfenv
mkdir ~/bin
ln -s ~/.tfenv/bin/* ~/bin/
tfenv install
tfenv use 1.11.4
```
To verify if the installation is successful, you should be able to see the version via ```terraform -version```.

3. ```kubectl``` should be pre-installed in AWS Cloudshell. To verify ```kubectl``` is installed, run the following:
```
kubectl --help
```
if you see a list of commands that you can execute with ```kubectl```, you're good to go. 

Move on to the next section [here]().