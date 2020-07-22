# Tech Insiders Globant 2020

This project deploys a Python microservice in AWS ECS, using Pulumi and Python to define the infrastructure. Additionally it uses AWS Codepipeline to deploy continously to the Production branch.

# Requirements

* **Python:** Infrastructure and microservices were built in python. Python 3.6 or later is required.
* **AWS Account:** The Pulumi code was created to deploy resources in AWS, you need an AWS account and create an IAM user with programmatic access.
* **Pulumi Account:** You need a Pulumi account to store the state of your infrastructure and manage your project, please follow this link for more information.

https://www.Pulumi.com/docs/intro/console/accounts-and-organizations/accounts/
* **Pulumi CLI:** You need the Pulumi CLI to deploy the infrastructure changes in AWS.

https://www.Pulumi.com/docs/get-started/install/

# AWS Architecture

![aws diagram](./docs/aws_architecture.jpeg)

# Structure

In the infrastructure folder is the python code used to deploy the AWS resources. This code use python local package and are stores in aws_components folder, this folder contains a package for each component required.
Pulumi uses a python virtual environment, the file requirements.txt is used to specify the package that the code will use into the virtual environment, feel free adding new package if the code requires them.

# Set up an environment

When you create a Pulumi account, Pulumi creates an organization by default, for a free account you can create only one organization. Each organization can have projects and stacks.

1. Login
    With the account already create and Pulumi CLI installed you can authenticate your terminal with Pulumi service.
    ```sh
    $ Pulumi login
    ```
    Pulumi will prompt you for an access token, including a way to launch your web browser to easily obtain one. Also,you can use `PULUMI_ACCESS_TOKEN` environment variable to set the Pulumi token.

2. Create Pulumi project and stack
    Create a file  from `Pulumi.yml.example`  and set it the name Pulumi.yml
    to create the project and stack run:
    ```sh
    $ pulumi stack init <STACK_NAME>
    ```
3. Create a Python virtual environment
    install the dependent packages

    ```bash
    $ python3 -m venv venv
    $ source venv/bin/activate
    $ pip3 install -r requirements.txt
    ```
4. Set AWS Configurations
    Pulumi creates a file named Pulumi.<Stack_Name>.yml with some configurations by default, for instance, the AWS Region. These configurations can be accessed into the python code.
    For this project you need to set two configurations for each stack, the AWS region in which you want to create the resources and the AWS profile that contains the AWS credentials.

    Configure the AWS credentials into your laptop(for Linux  ~/.aws/credentials), you need to use the following format:

    ```bash
    [Profile_name]
    aws_access_key_id = Replace_for_correct_Access_Key
    aws_secret_access_key = Replace_for_correct_Secret_Key
    ```

    Run the following commands to set the configurations into the stack

    ```bash
    $ pulumi config set  aws:region <AWS_Region>

    $ pulumi config set  aws_profile <AWS_profile>
    ```
# Deploy

You can make a review of the resources that pulumi will create or modify.
```bash
$ pulumi preview
```

If you are sure that the changes that pulumi will create or modify are the correct, you can apply the changes.
```bash
$ pulumi up
```

# Destroy
If you don't want to maintain the resources created and delete the stack please run:

```bash
$ pulumi destroy

$ pulumi stack rm

$ pulumi logout
```
