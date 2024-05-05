# ![aws](https://github.com/julien-muke/Search-Engine-Website-using-AWS/assets/110755734/01cd6124-8014-4baa-a5fe-bd227844d263)     Create EC2 Instance using Terraform


## <a name="introduction">🤖 Introduction</a>

We are going to learn how to create an Amazon EC2 instance using Terraform. Terraform is a popular tool for building, changing, and versioning infrastructure safely and efficiently. 

With the apply command, Terraform compares the current state of the Target infrastructure against the desired state defined in the configuration and determines what actions are necessary to achieve the desired state.


![Serverless Web Application on AWS(1)](https://github.com/julien-muke/aws-ec2-terraform/assets/110755734/3e8c84c5-c7a8-41a3-9ae9-f4dc7c68ee7f)


## <a name="steps">☑️ Steps</a>

* Create an IAM User, and the Access Key
* Build a Lambda function to handle the CRUD operations on the DynamoDB table
* Use S3 to store and host the web application's static files (HTML, CSS, and JavaScript)
* Create a CloudFront distribution to serve the S3-hosted static files with low latency

## <a name="quick-start">🤸 Quick Start</a>

Follow these steps to set up the project locally on your machine.

**Prerequisites**

Make sure you have the following installed on your machine:

- [terraform](https://www.terraform.io/)
- [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)


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



