
##Get VPC ID
```sh
aws ec2 describe-vpcs \
  --filters "Name=tag:Name,Values=nacl-example-vpc" \
  --query "Vpcs[0].VpcId" \
  --output text
```
##Create NACL
```sh
aws ec2 create-network-acl --vpc-id vpc-0d12cd396dd61ac51
```