# serverlessApp

Prerequisites:

 - AWS Account (With Access to create lamda and api gateway, or one with admin access, as well the access keys downloaded in csv format)
 - AWS CLI downloaded and installed on local machine
     - For a Windows machine, [click here](https://awscli.amazonaws.com/AWSCLIV2.msi)
     - For a Linux machine, [click here](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-linux.html#cliv2-linux-install)
     - For MacOS, [click here](https://awscli.amazonaws.com/AWSCLIV2.pkg)
 - Terraform downloaded and installed on local machine
     - For Windows, [32-bit](https://releases.hashicorp.com/terraform/0.13.4/terraform_0.13.4_windows_386.zip) | [64-bit](https://releases.hashicorp.com/terraform/0.13.4/terraform_0.13.4_windows_amd64.zip)
     - For Linux , [32-bit](https://releases.hashicorp.com/terraform/0.13.4/terraform_0.13.4_linux_386.zip) | [64-bit](https://releases.hashicorp.com/terraform/0.13.4/terraform_0.13.4_linux_amd64.zip)
     - For MacOS , [64-bit](https://releases.hashicorp.com/terraform/0.13.4/terraform_0.13.4_darwin_amd64.zip)

   - Configure AWS credentials locally using:

     ```$ aws configure ```

This repository uses the [example](https://learn.hashicorp.com/tutorials/terraform/lambda-api-gateway) provided by Terraform to create a Lambda function with an API Gateway which returns a hard-coded "Hello world!" response in the object structure that an API Gateway expects.

The build artifacts are normally created using a CI tool and uploaded to an S3 bucket. For now, the artifact have been manually created and uploaded to the s3 bucket. Steps to add this using Github Actions will be updated in the future.


To manually upload the file, use the following commands:

#### Create a bucket using the command line

` aws s3api create-bucket --bucket=<unique-bucket-name>  --region=<aws-region>  // for aws-region=us-east1 

 aws s3api create-bucket --bucket=<unique-bucket-name> --region=<aws-region> --create-bucket-configuration LocationConstraint=<aws-region> // for any other region `

#### Manually upload the file

 ``` aws s3 cp <build-artifact> s3://<unique-bucket-name>/v1.0.0/example.zip ```

#### Creating the lambda function

The terraform code to create the lambda function is available in the terraform/lambda.tf file. This file creates an IAM role for the lambda function with no access to any other AWS services.

In terraform/lambda.tf, Edit Line 10 to change the region name and Line 27 to change the bucket name. Future iterations would have ways to paramterize this.

To apply the configurations:


#### Switch to the terraform directory 

``` cd terraform ```

#### Initialize the new terraform directory 

``` terraform init ```

#### Apply the configurations

``` terraform apply ```

#### To clean up the resources 

 ``` terraform destroy -var="app_version=1.0.0" ```