Introduction:

Terraform is Infrastructure as a Code. Infrastructure means resources required to maintain an application. 
This means whatever infrastructure the application has is obtained to us through code(terraform). 
Resources are anything and everything that is created on cloud. (e.g S3 bucket, EC2 instance, IAM user, etc.)
Terraform helps to create these resources. 
Terraform has predefined templates which can be used to create resources on any cloud. These predefined templates of terraform are different for different clouds. And to use them for example for AWS, we need to define them in the main.tf file by using the AWS provider. AWS provider gives me the ability to use these predefined templates. 
To install this provider, we need to do terraform init.

Log in:
Terraform needs to log in inside any cloud to create resources. For logging in, it requires credentials. These credentials are set as environment variables. E.g. In AWS, these environment variables are Access Key and Secret Access Key. We also need to set up the region so we know in which region the resources are created.
Let’s take an example:
Create a S3 bucket that has server side encryption enabled and bucket versioning enabled.
Create an AWS RDS database instance with encryption enabled and not publicly accessible.
Create AWS EKS cluster with basic config. (create subnets in two different availability zones terraform)

We have to tell terraform to initiate AWS configurations. This is called as “AWS Provider”

“Provider” enables you to create resources.

# terraform init -> it is used to initialize and install the provider and make it ready for creating resources.

For creating resources, terraform needs to log in into the AWS account. For logging in, credentials are required. These are “Access Key” and “Secret Access Key”. These credentials are exported as environment variables. These environment variables provide authentication.

# export AWS_ACCESS_KEY_ID=””
# export AWS_SECRET_ACCESS_KEY=””

resource “aws_s3_bucket” “example” {
  bucket = “sonuli”
}

resource -> It is a terraform key word that specifies we want to create a resource
“aws_s3_bucket” -> It is a terraform keyword that specifies terraform to create an S3 bucket.
“example” -> This is the name of the resource for terraform. This can be any name
bucket -> This is a keyword. There are various attributes associated with a resource. This is one of the attributes for the “aws_s3_bucket” resource. This specifies the name of the bucket in AWS. 

# terraform plan -> This command gives a plan of what will be created.
# terraform apply -> This command will create resources as per the plan.
# terraform destroy -> This command will destroy the resources.


Terraform State File:

The Terraform state file stores the record of the infrastructure managed by your code. It is a JSON file that stores info about the resources created, their attributes and dependencies. By default, the state file is stored locally as “terraform.tfstate” file. However, for collaborative environments it is stored remotely for e.g. on the S3 bucket.

 If there are any changes to be made to the infrastructure, the state file is pulled locally, changes are made and then the updated state file is again pushed remotely. This way any developer will have the most recent state of the infrastructure.


Data Source: the data from terraform’s database which can be used in the current terraform file. 

A data source in Terraform is a mechanism to retrieve information about resources that are not managed by the current Terraform configuration. Data sources do not create or modify resources; instead, they provide a way to access and use data to inform the configuration of your resources.
Use case for terraform: 

I used terraform for the integration test suite. In my current job, I write security controls. To test these security controls, I need to create resources ( good terraform, bad terraform: good S3 bucket and bad s3 bucket). To create these resources, I use terraform. I run the control against these resources. The control should pass against good and fail against bad terraform respectively. 
Once this individual control is working as expected, I had to ensure that this control is working in accordance with the rest of the controls. Hence I created an integration test suite. There were 200 controls. I understood the use case of each control and created a good terraform for that particular control and bad terraform as well. Once the good terraform was created for all the controls and if those controls passed against the good terraform, the good terraform was destroyed. Then bad terraform was created, controls failed against bad terraform, bad terraform was destroyed. This indicated that all the controls are working together in an orderly manner in each other’s presence. 
Once this testing is completed (integration test suite), we now need to run the controls against all the cloud accounts. This was done by building an architecture on GCP. Resources for this architecture were created and managed using Terraform. 


Local block-  Variable value. It's essentially a temporary, read-only variable for internal calculations.