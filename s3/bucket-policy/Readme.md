##Create a bucket
aws s3 mb s3://bucket-policy-examples-dt

##

aws s3api put-bucket-policy --bucket bucket-policy-examples-dt --policy file:///workspace/AWS-Examples/s3/bucket-policy/policy.json

##Cleanup
aws s3 rm s3://bucket-policy-examples-dt

aws s3 rb s3://bucket-policy-examples-dt