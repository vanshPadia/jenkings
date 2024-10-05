Here's a simple step-by-step guide for the `README.md` file to accompany your CloudFormation template:

---

# EC2 Instance CloudFormation Template

This CloudFormation template deploys an EC2 instance with Jenkins installed using user data. It provides flexibility to define the instance type, key pair, subnet, and AMI.

## Prerequisites

Before you use this template, ensure that you have the following:

- An existing AWS account.
- A valid EC2 Key Pair for SSH access to the instance.
- An existing Subnet ID in the region where you plan to launch the EC2 instance.
- Appropriate IAM permissions to create EC2 instances, VPC-related resources, and CloudFormation stacks.

## Parameters

The template accepts the following parameters:

- **InstanceType**: Choose the EC2 instance type (e.g., `t2.micro`, `t2.small`, `t2.medium`).
- **KeyName**: Provide the name of an existing EC2 Key Pair for SSH access.
- **SubnetId**: Specify the ID of an existing subnet where the EC2 instance will be launched.
- **AMIId**: (Optional) Specify the AMI ID for the EC2 instance (default: `ami-0dee22c13ea7a9a67` for `ap-south-1` region).

## Steps to Deploy the CloudFormation Stack

1. **Download the CloudFormation Template:**
   - Download or copy the `ec2-instance.yaml` file (this CloudFormation template).

2. **Log in to AWS Management Console:**
   - Navigate to the [AWS CloudFormation Console](https://console.aws.amazon.com/cloudformation).

3. **Create a New Stack:**
   - Click on **Create stack** > **With new resources (standard)**.
   - Select **Upload a template file** and choose the downloaded template file.

4. **Configure Stack Options:**
   - Enter a **Stack Name** (e.g., `MyEC2InstanceStack`).
   - Configure the following parameters:
     - `InstanceType`: Choose your preferred EC2 instance type.
     - `KeyName`: Enter the name of an existing EC2 Key Pair for SSH access.
     - `SubnetId`: Provide the Subnet ID where you want to deploy the instance.
     - `AMIId`: (Optional) Provide a custom AMI ID if needed (default: Jenkins-friendly AMI in `ap-south-1`).
     
5. **Configure Stack Options (Optional):**
   - You can optionally add tags, set up permissions, or configure other stack options.

6. **Deploy the Stack:**
   - Click **Next** and review the configuration. If everything is correct, click **Create stack** to start the deployment.

7. **Monitor the Stack Creation:**
   - Monitor the status in the CloudFormation console. Once the stack creation completes, you'll see the status `CREATE_COMPLETE`.

8. **Get Instance Details:**
   - After the stack is successfully created, navigate to the **Outputs** section of the stack to find:
     - **InstanceId**: The EC2 instance ID.
     - **PublicIP**: The public IP address for the instance (useful for SSH access and connecting to Jenkins).

## SSH Access to the Instance

To SSH into the EC2 instance:
```bash
ssh -i /path/to/your-key.pem ec2-user@<PublicIP>
```

Replace `/path/to/your-key.pem` with the path to your Key Pair and `<PublicIP>` with the Public IP address of the EC2 instance (available in the **Outputs** section of the CloudFormation stack).

## Jenkins Setup

Once the EC2 instance is running, Jenkins is installed automatically. You can access Jenkins by opening your browser and navigating to:
```
http://<PublicIP>:8080
```
Use the initial Jenkins admin password from the following command (run in SSH after connecting to the instance):
```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

## Cleanup

To delete the EC2 instance and associated resources, follow these steps:

1. Go to the [CloudFormation Console](https://console.aws.amazon.com/cloudformation).
2. Select your stack.
3. Click **Delete**.

This will remove all resources created by this template.

---

This `README.md` should give clear steps on how to use the CloudFormation template from start to finish.
