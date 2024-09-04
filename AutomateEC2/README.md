# EC2 Instance Management Automation with AWS CLI

This project demonstrates how to automate the management of Amazon EC2 instances using the AWS CLI. The goal is to help you understand essential cloud concepts such as EC2 instance management, key pair and security group configuration, and basic scripting with the AWS CLI.

## Objective

Write scripts to automate the launching, stopping, and terminating of EC2 instances using the AWS CLI.

## Skills Learned
- EC2 instance management.
- Key pair and security group configuration.
- Scripting with the AWS CLI for instance management.
- Creating and managing AMIs (Amazon Machine Images).

---

## Prerequisites

- **AWS Account**: With appropriate permissions for EC2 and IAM management.

---

## Project Steps

### 1. Set Up Your Environment

1. **Install AWS CLI**  
   If you haven't already installed the AWS CLI, you can follow the instructions [here](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html).

2. **Configure AWS CLI**  
   Run the following command to set up your AWS credentials:
   ```bash
   aws configure
   ```

## 2. Create a Key Pair

A key pair is required to securely access your EC2 instances.

1. **Create the Key Pair**  
   Run the following command to create the key pair and save it to a `.pem` file:
   ```bash
   aws ec2 create-key-pair --key-name MyKeyPair --query 'KeyMaterial' --output text > MyKeyPair.pem
   ```

2. **Secure the Key Pair**  
   Modify the permissions for the key pair to ensure it's not publicly viewable:
   ```bash
   chmod 400 MyKeyPair.pem
   ```

---

## 3. Create a Security Group

Security groups act as a virtual firewall to control inbound and outbound traffic for your instances.

1. **Create a Security Group**  
   Create a security group using the AWS CLI:
   ```bash
   aws ec2 create-security-group --group-name MySecurityGroup --description "My security group"
   ```

2. **Authorize Inbound SSH Access**  
   Allow SSH access to the EC2 instance from anywhere. You may want to limit the IP address range for better security:
   ```bash
   aws ec2 authorize-security-group-ingress --group-name MySecurityGroup --protocol tcp --port 22 --cidr 0.0.0.0/0
   ```

---

## 4. Launch an EC2 Instance

1. **Launch an EC2 Instance**  
   Run the following command to launch an EC2 instance. Replace the `ami-xxxxxxx` with a valid AMI ID for your region:
   ```bash
   aws ec2 run-instances --image-id ami-0abcdef1234567890 --instance-type t2.micro --key-name MyKeyPair --security-groups MySecurityGroup
   ```

2. **Get Instance Information**  
   To retrieve information about your running instances:
   ```bash
   aws ec2 describe-instances --query "Reservations[*].Instances[*].[InstanceId,InstanceType,State.Name,PublicIpAddress]" --output table
   ```

---

## 5. Automate EC2 Instance Management

You can automate the EC2 instance lifecycle by writing simple bash scripts.

1. **Create a Bash Script to Manage Instances**  
   Here's an example script (`ec2-manager.sh`) that will start, stop, or terminate an instance based on user input:
   ```bash
   #!/bin/bash

   ACTION=$1
   INSTANCE_ID="i-0123456789abcdef0"

   case $ACTION in
       start)
           aws ec2 start-instances --instance-ids $INSTANCE_ID
           ;;
       stop)
           aws ec2 stop-instances --instance-ids $INSTANCE_ID
           ;;
       terminate)
           aws ec2 terminate-instances --instance-ids $INSTANCE_ID
           ;;
       *)
           echo "Usage: $0 {start|stop|terminate}"
           exit 1
   esac
   ```

2. **Run the Script**  
   Make the script executable:
   ```bash
   chmod +x ec2-manager.sh
   ```

   Run the script to manage your instance:
   - Start the instance:
     ```bash
     ./ec2-manager.sh start
     ```

   - Stop the instance:
     ```bash
     ./ec2-manager.sh stop
     ```

   - Terminate the instance:
     ```bash
     ./ec2-manager.sh terminate
     ```

---

## 6. Create and Manage AMIs

Amazon Machine Images (AMIs) are snapshots of your EC2 instances that you can use to launch identical instances in the future.

1. **Create an AMI**  
   Create an AMI from an existing instance:
   ```bash
   aws ec2 create-image --instance-id i-0123456789abcdef0 --name "MyServerImage" --no-reboot
   ```

2. **List Your AMIs**  
   View a list of your AMIs:
   ```bash
   aws ec2 describe-images --owners self --query "Images[*].[ImageId,Name,State]" --output table
   ```

3. **Deregister an AMI**  
   Remove an AMI when you no longer need it:
   ```bash
   aws ec2 deregister-image --image-id ami-0123456789abcdef0
   ```

---

## 7. Clean Up

After completing your EC2 instance management, it’s important to clean up resources to avoid unwanted charges.

1. **Terminate EC2 Instances**  
   Terminate your EC2 instance:
   ```bash
   aws ec2 terminate-instances --instance-ids i-0123456789abcdef0
   ```

2. **Delete Key Pair and Security Group**  
   Remove the key pair and security group created for this project:
   ```bash
   aws ec2 delete-key-pair --key-name MyKeyPair
   aws ec2 delete-security-group --group-name MySecurityGroup
   ```


