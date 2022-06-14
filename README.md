# CloudFormation Template for SPA
CloudFormation Template for publishing SPA with CloudFront + S3 on custom domain.

## How to use
1.
```
aws cloudformation create-stack \
  --stack-name acm-route53-waf  \
  --template-body file://./cloudformation/acm-hostedzone-waf.yaml \
  --region us-east-1 \
  --parameters ParameterKey=DomainName,ParameterValue={my domain}
```

2.
```
aws cloudformation create-stack \
  --stack-name cloudfront \
  --template-body file://./cloudformation/waf-acm.yaml \
  --region ap-northeast-1 \
  --parameters \
    ParameterKey=CertificateArn,ParameterValue={acm arn} \
    ParameterKey=WebACLArn,ParameterValue={web acl arn} \
    ParameterKey=DomainName,ParameterValue={my domain}
```