SHELL := /bin/bash
STACKNAME?= "encapture-stacks"
S3_BUCKET?= "056234693470-us-east-2-deployment" #OVERRIDE THIS BUCKET NAME
S3_PREFIX?= "local"
clean:
	rm -f lambda1/template.out.yml
	rm -f lambda2/template.out.yml
	rm -f resources.out.yml
validate:
	aws cloudformation validate-template --template-body file://lambda1/template.yml --output text
	aws cloudformation validate-template --template-body file://lambda2/template.yml --output text
	aws cloudformation validate-template --template-body file://resources.yml --output text
package: clean 
	find ./lambda1 -not -path '*/.*' -exec touch -a -m -t"201001010000.00" {} \;
	aws cloudformation package --template-file lambda1/template.yml --s3-bucket $(S3_BUCKET) --s3-prefix $(S3_PREFIX) --output-template-file lambda1/template.out.yml
	find ./lambda2 -not -path '*/.*' -exec touch -a -m -t"201001010000.00" {} \;
	aws cloudformation package --template-file lambda2/template.yml --s3-bucket $(S3_BUCKET) --s3-prefix $(S3_PREFIX) --output-template-file lambda2/template.out.yml
	aws cloudformation package --template-file resources.yml --s3-bucket $(S3_BUCKET) --s3-prefix $(S3_PREFIX) --output-template-file resources.out.yml
deploy: package 
	aws cloudformation deploy --stack-name $(STACKNAME) --template-file resources.out.yml --parameter-overrides file://resources.params.local.json --capabilities CAPABILITY_NAMED_IAM CAPABILITY_AUTO_EXPAND 
destroy:
	aws cloudformation delete-stack --stack-name $(STACKNAME)
