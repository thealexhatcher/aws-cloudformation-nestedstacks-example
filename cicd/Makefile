SHELL := /bin/bash
STACKNAME?="encapture-cfn-example-pipeline"
ARTIFACT_BUCKET?="056234693470-us-east-2-deployment"
REPO_NAME?="encapture-cfn-example"
BRANCH?="master"

validate:
	aws cloudformation validate-template --template-body file://codepipeline.yml --output text
deploy: 
	aws cloudformation deploy --stack-name $(STACKNAME) --template-file codepipeline.yml --parameter-overrides ArtifactBucket=$(ARTIFACT_BUCKET) RepoName=$(REPO_NAME) Branch=$(BRANCH) --capabilities CAPABILITY_NAMED_IAM CAPABILITY_AUTO_EXPAND 
destroy:
	aws cloudformation delete-stack --stack-name $(STACKNAME)-resources && aws cloudformation wait stack-delete-complete --stack-name $(STACKNAME)-resources
	aws cloudformation delete-stack --stack-name $(STACKNAME) && aws cloudformation wait stack-delete-complete --stack-name $(STACKNAME)
