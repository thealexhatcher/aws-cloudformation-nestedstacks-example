# aws-cloudformation-nestedstacks-example

This is a boilerplate template for building and deploying complex sets of AWS resources. AWS Cloudformation with nested stacks, we are able to achieve the following goals:

1. Easily build, package, and deploy all infrastructure and application code for local testing and debugging. 
 Examples: 
 - Manage resource dependencies and deployment orchestration at dev time.
 - run "make deploy" to run and end-to-end test locally and "make destroy" to delete all resources without a trace.
2. Easily develop subcomponents that can be tested independently of the full AWS infrastructure architecture. 
 Examples:
 - develop new lambda functions locally and them to the parent template as a nested stack
 - test subcomponents in an end-to-end context before committing changes.
3. Create a simple CI/CD process that requires minimal changes as new application features are added.

This project uses a vscode devcontainer environment. More information on setup can be found [here](https://code.visualstudio.com/docs/remote/containers).

### Prerequisites 

1. You have an AWS Account 
2. You have an IAM User or Role with permissions to create the required IAM User Account and IAM Role for AWS Cloudformation actions.
3. You have obtained [AWS Access Keys and Secret Keys](https://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html#access-keys-and-secret-access-keys) for your IAM User Account or Role
4. You are running this example in the vscode devcontainer environment
5. You have [configured the aws cli](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-quickstart.html#cli-configure-quickstart-config) to use your AWS Access Key and Secret Key.

### Execution

#### 1.  


#### 2.  Setup
