# ![aws](https://github.com/julien-muke/Search-Engine-Website-using-AWS/assets/110755734/01cd6124-8014-4baa-a5fe-bd227844d263)     Create EC2 Instance using Terraform


## <a name="introduction">🤖 Introduction</a>

We are going to learn how to create an Amazon EC2 instance using Terraform. Terraform is a popular tool for building, changing, and versioning infrastructure safely and efficiently. With the apply command, Terraform compares the current state of the Target infrastructure against the desired state defined in the configuration and determines what actions are necessary to achieve the desired state.



## <a name="design">📐 Design</a>

![Serverless Web Application on AWS](https://github.com/julien-muke/Serverless-Web-Application-on-AWS/assets/110755734/9c7fefe7-014e-4648-a105-fc67b201d882)


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

