# ![aws](https://github.com/julien-muke/Search-Engine-Website-using-AWS/assets/110755734/01cd6124-8014-4baa-a5fe-bd227844d263)     Create EC2 Instance using Terraform


## <a name="introduction">🤖 Introduction</a>

We are going to learn how to create an Amazon EC2 instance using Terraform. Terraform is a popular tool for building, changing, and versioning infrastructure safely and efficiently. 


![Serverless Web Application on AWS(1)](https://github.com/julien-muke/aws-ec2-terraform/assets/110755734/3e8c84c5-c7a8-41a3-9ae9-f4dc7c68ee7f)


## <a name="steps">☑️ Steps</a>

1. Create an IAM User
2. Configure AWS profile and set up the AWS CLI
3. Create Terraform file (.tf) and write the Script
4. Execute the Terraform Script
5. Verify S3 Bucket is created 

## <a name="quick-start">🤸 Quick Start</a>

Follow these steps to set up the project locally on your machine.

**Prerequisites**

Make sure you have the following installed on your machine:

- The [Terraform CLI](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli) (1.2.0+) installed.
- The [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) installed.
- The [AWS account](https://aws.amazon.com/free/) and [associated credentials](https://docs.aws.amazon.com/IAM/latest/UserGuide/security-creds.html) that allow you to create resources.

  
## ➡️ Step 1 - Create an IAM User, and the Access Key

First, we need to create a user and then create access keys for that particular user so that we can work with them for our authentication purpose.

1. Navigate to your AWS Console, search for AWS Identity and Access Management (IAM)
2. Go the Tab at righ hand side and choose "Users"
3. Click "Create user"

![Screenshot 2024-05-05 at 12 56 48](https://github.com/julien-muke/aws-ec2-terraform/assets/110755734/ded49b4d-5a14-4db0-8cc0-fabcbfcd3474)


4. Enter the "User name" i will use `ec2-terraform` then click "Next"

![Screenshot 2024-05-05 at 12 57 20](https://github.com/julien-muke/aws-ec2-terraform/assets/110755734/457b10b7-aa88-436c-9eb2-e1d99b2f9346)

5. Set permissions, choose "Attached policies directly" search and choose `AmazonEC2FullAccess` then click "Next"

![Screenshot 2024-05-05 at 12 58 56](https://github.com/julien-muke/aws-ec2-terraform/assets/110755734/30f06e43-5147-49ec-b22a-608add702318)


6. Review the details and click "Create user"

Now you can see that our user has been successfully created.

7. Next, let's create the access key for the user
8. Click on the user we just created

![Screenshot 2024-05-05 at 12 59 44](https://github.com/julien-muke/aws-ec2-terraform/assets/110755734/5c8a1851-c9d4-4500-9816-d913cf133e2c)


9. Scroll down to security crendentials tab, and click "Create access key"
10. Since I am going to work with command line interface, we will choose CLI and check the confirmation box and click "Next"

![Create-access-key-IAM-Global](https://github.com/julien-muke/aws-ec2-terraform/assets/110755734/38d247fc-4ed8-4e45-962c-c8c17400dbd3)

11. The access key is successfully created, now it will show the access key as well as the secret access key, I will simply go and download the CSV file.

![Screenshot 2024-05-05 at 13 00 36](https://github.com/julien-muke/aws-ec2-terraform/assets/110755734/0c21c652-5cf0-4b8f-8e8e-bfb828a03e2c)


## ➡️ Step 2 - Configure AWS profile and set up the AWS CLI

We are going to configure basic settings that the AWS Command Line Interface (AWS CLI) uses to interact with AWS. These include your security credentials, the default output format, and the default AWS Region.


1. Open VS Code (or any IDE of your choise) and run the command `aws configure`
2. Copy and paste your AWS Access Key ID
3. Copy and paste your AWS Secret Access key
4. Keep as default region name and output format

![1](https://github.com/julien-muke/aws-ec2-terraform/assets/110755734/ad38c212-ed4a-4730-9614-8a8959faab10)

5. To check if the AWS profile is configured run the following command `aws configure list`

![2](https://github.com/julien-muke/aws-ec2-terraform/assets/110755734/3d5a2a6f-9d22-4cf7-b065-3e5d2b0765c7)


## ➡️ Step 3 - Create Terraform file (.tf) and write the Script


1. Create a file to define your infrastructure by running the following command:

```bash
touch main.tf
```

2. Open main.tf in your text editor, paste in the configuration below, and save the file.


```bash
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 4.16"
    }
  }

  required_version = ">= 1.2.0"
}

provider "aws" {
  region  = "us-east-1"
}

resource "aws_instance" "YOUR-INSTANCE-NAME" {
  ami           = "YOUR-AWS-AMI"
  instance_type = "t3.micro"

  tags = {
    Name = "MyEC2Instance"
  }
}

```
NOTE: 
     <br>* Name your ES2 instance
     <br>* Copy the AMI from your EC2 instance console
     <br>* Choose an instance type: t2.micro or t3.micro

![3](https://github.com/julien-muke/aws-ec2-terraform/assets/110755734/edcffead-f92f-447a-b9a1-983a85fd9b83)


This is a complete configuration that you can deploy with Terraform. 

Let's review each block of this configuration in more detail:

* Terraform Block 

The `terraform {}` block contains Terraform settings, including the required providers Terraform will use to provision your infrastructure. For each provider, the `source` attribute defines an optional hostname, a namespace, and the provider type. Terraform installs providers from the [Terraform Registry](https://registry.terraform.io/) by default. In this example configuration, the `AWS` provider's source is defined as `hashicorp/aws`, which is shorthand for `registry.terraform.io/hashicorp/aws`

* Providers

The `provider` block configures the specified provider, in this case AWS. A provider is a plugin that Terraform uses to create and manage your resources.

* Resources

Use `resource` blocks to define components of your infrastructure. A resource might be a physical or virtual component such as an EC2 instance.


## ➡️ Step 4 - Execute the Terraform Script

1. It's recommended using consistent formatting in your configuration files. To automatically updates configurations in the current directory for readability and consistency run the following command:

```bash
terraform fmt
```

2. You need to initialize the directory with the command `terraform init`. Initializing a configuration directory downloads and installs the providers defined in the configuration, which in this case is the `AWS` provider.

```bash
terraform init
```

3. Terraform will download the `aws` provider and will install it in a hidden subdirectory of your current working directory, named `.terraform`. The `terraform init` command will print out which version of the provider was installed. Terraform also creates a lock file named `.terraform.lock.hcl` which specifies the exact provider versions used, so that you can control when you want to update the providers used for your project.

![4](https://github.com/julien-muke/aws-ec2-terraform/assets/110755734/4f8d4c31-9019-48de-9fcc-57e2d42df61c)


4. You can also make sure your configuration is syntactically valid and internally consistent by using the `terraform validate` command.

```bash
terraform validate
```

![5](https://github.com/julien-muke/aws-ec2-terraform/assets/110755734/ea78429e-7729-4ef5-a416-8ec67d1008fc)


5. Next, I'll try to preview the changes with the help of `terraform plan` command

```bash
terraform plan
```

6. As you can see below, terraform will perform the following actions:
- It wil create a resource that is AWS instance
- It will create the Amazon Machine Image (AMI) as we specify
- The rest of the configuration will be applied automatically

![6](https://github.com/julien-muke/aws-ec2-terraform/assets/110755734/53794b97-78ad-41d6-996c-70bcba9a5b0f)
![7](https://github.com/julien-muke/aws-ec2-terraform/assets/110755734/7a509edb-85fd-4a70-a21d-b11aace73706)
![8](https://github.com/julien-muke/aws-ec2-terraform/assets/110755734/a8441e38-1874-41b0-8aea-8fe9129978aa)


7. Apply the configuration now with the `terraform apply` command the confirm by `yes`. Also terraform apply command we create
`terraform.dfstate` file. Terraform will print output similar to what is shown below.

```bash
terraform apply
```

![9](https://github.com/julien-muke/aws-ec2-terraform/assets/110755734/e74c3408-96fe-4180-ad5a-386c82ce3fb2)

## ➡️ Step 5 - Verify S3 Bucket is created 

1. Open your AWS Management Console, seach for EC2 instance, as you can see below our EC2 instance has been successfully created  and it's in a running state.

![Screenshot 2024-05-05 at 13 46 13](https://github.com/julien-muke/aws-ec2-terraform/assets/110755734/0af68101-c649-41d4-9d99-27520763eef4)


🏆 We have successfully created an EC2 instance with the help of Terraform.


## 💰 Cost

All services used are eligible for the AWS Free Tier. However, charges will incur at some point so it's recommended that you shut down resources after completing this tutorial.

To delete the EC2 instance, run the command `terraform destroy`

```bash
terraform destroy
```







