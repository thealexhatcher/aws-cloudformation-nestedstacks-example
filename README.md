# aws-cloudformation-nestedstacks-example

This is a boilerplate template for building and deploying complex sets of AWS resources. AWS Cloudformation with nested stacks, we are able to achieve the following goals:

1. Easily build, package, and deploy all infrastructure and application code for local testing and debugging. 
2. Easily develop subcomponents that can be tested independently of the full AWS infrastructure architecture. 
3. Use a Simple CI/CD Pipelinethat requires minimal updates as new application features are added.

This project uses a vscode devcontainer environment. More information on setup can be found [here](https://code.visualstudio.com/docs/remote/containers).

### Prerequisites 

1. You have an AWS Account 
2. You have an IAM User or Role with permissions to create the required IAM User Account and IAM Role for AWS Cloudformation actions.
3. You have obtained [AWS Access Keys and Secret Keys](https://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html#access-keys-and-secret-access-keys) for your IAM User Account or Role
4. You are running this example in the vscode devcontainer environment
5. You have [configured the aws cli](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-quickstart.html#cli-configure-quickstart-config) to use your AWS Access Key and Secret Key.

### Execution



#### Local Build

Create a bucket for local packaged artifacts.
```bash
export S3_BUCKET=aws-nestedstacks-example-package-bucket && aws s3 mb s3://$S3_BUCKET
```

Validate, Package, and Deploy all aws-cloudformation-nestedstacks-example resources
```bash
cd src 
make deploy \
 STACKNAME=aws-nestedstacks-example-resources \
 S3_BUCKET=$S3BUCKET S3_PREFIX=local 
cd -
```

Destroy all aws-cloudformation-nestedstacks-example resources 
```bash
cd src 
make destroy
cd -
```

#### Pipeline Build

Make a bucket for cicd pipeline artifacts.
```bash
export S3_BUCKET=aws-nestedstacks-example-artifact-bucket && aws s3 mb s3://$S3_BUCKET
```

Make an AWS CodeStar Connection to GitHub.
```bash
export CONNECT_ARN=$(aws codestar-connections create-connection --connection-name aws-nestedstacks-example-conn --provider-type GitHub --output text)
```

Update the AWS CodeStar Connection which is in a PENDING state by following instructions given (here)[https://docs.aws.amazon.com/dtconsole/latest/userguide/connections-update.html].

Deploy the CI/CD pipeline
```bash
cd cicd 
make deploy \
 STACKNAME=aws-nestedstacks-example-cicd \
 ARTIFACT_BUCKET=$S3_BUCKET \
 CONNECTION_ARN=$CONNECTION_ARN \
 REPO_ID=thealexhatcher/aws-cloudformation-nestedstacks-example \
 BRANCH=main
cd -
```

Destroy the CI/CD pipeline
```bash
cd cicd 
make destroy
cd -
```

