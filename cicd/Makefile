SHELL := /bin/bash
STACKNAME?="aws-nestedstacks-example-cicd"
ARTIFACT_BUCKET?="OVERRIDE_REQUIRED"
CONNECTION_ARN?="OVERRIDE_REQUIRED"
REPO_ID?="OVERRIDE_REQUIRED"
BRANCH?="master"

validate:
	aws cloudformation validate-template --template-body file://codepipeline.yml --output text
deploy: validate
	aws cloudformation deploy --stack-name $(STACKNAME) --template-file codepipeline.yml --parameter-overrides ArtifactBucket=$(ARTIFACT_BUCKET) CodeStarConnectionArn=$(CONNECTION_ARN) RepoId=$(REPO_ID) Branch=$(BRANCH) --capabilities CAPABILITY_NAMED_IAM CAPABILITY_AUTO_EXPAND 
destroy:
	aws cloudformation delete-stack --stack-name $(STACKNAME)-resources && aws cloudformation wait stack-delete-complete --stack-name $(STACKNAME)-resources
	aws cloudformation delete-stack --stack-name $(STACKNAME) && aws cloudformation wait stack-delete-complete --stack-name $(STACKNAME)
