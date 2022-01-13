# Important Notes
When deploying the terraform application, it's important to note that it won't be successful unless the relevant resources are first deleted so that they can be created again by this application. So for example, the security groups and clusters that get created must be deleted either within the AWS console or CLI before being able to deploy successfully.

To run the application:

terraform init
terraform apply

# main.tf:
Contains the primary functionality for the terraform script. It instantiates the load balancer, rds cluster, the ecs cluster, IAM roles and policies, and secrets manager secret, among other resources.

# iam.tf
Creates the necessary IAM permissions for the user to perform all the necessary tasks. This includes creating a role that has an attached policy that has the necessary permissions so that the user can perform all the tasks throughout the terraform script such as creating log groups and using secrets manager to verify the identity of the user creating all the resources for the application

# data.tf
Creates the id for the ecs subnets and the iam policy for kms. Secrets manager uses kms to encrypt and decrypt the "secret" that protects the user's data and permissions.

# variables.tf
Contains all the variables for the terraform script. Most of them are defaulted for the user's ease as some of them include inputting the subnets for the rds cluster and ecs cluster, which would be hard to know if you aren't very aware of the program.

# security-groups.tf
Creates the proper security groups for the different parts of the program such as the ecs and rds cluster. These services need the correct inbound and outbound rules to allow for communication between the different services.

# outputs.tf
Contains the key identifiers of many of the resources used throughout the prorgram such as the kms key id, ecs task arn, and rds cluster endpoint. After a successful deployment, all the identifiers in the output.tf file will be outputted in the console.

# providers.tf
Contains the required providers for the application, which includes the aws and random providers. The aws provider contains the lifecycle management of AWS resources such as ECS, RDS, VPC, etc. The random provider allows the use of randomness within Terraform configurations so that resources can generate random values and hold onto those values until the inputs are changed. The database password was generated randomly, for example, which used the random provider.

# wordpress.tpl
Template file for the wordpress application, which contains the configuration for the application and helps put all the resources of the application together to create the final product. The configuration includes the environment, the mount points, and the necessary ports for the application to run.

# Acronyms
lb - load balancer
rds - relational database service
ecs - elastic container service
efs - elastic file system
kms - key management service
db - database