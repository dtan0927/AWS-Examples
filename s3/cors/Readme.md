```sh
##Create a bucket
aws s3 mb s3://cors-fun-dt
```
##Change block public access
```sh
aws s3api put-public-access-block \
    --bucket cors-fun-dt \
    --public-access-block-configuration "BlockPublicAcls=true,IgnorePublicAcls=true,BlockPublicPolicy=false,RestrictPublicBuckets=false"
```
##Create a bucket policy
```sh
aws s3api put-bucket-policy --bucket cors-fun-dt --policy file://cors-policy.json
```
##Turn on static website hosting
```sh
aws s3api put-bucket-website --bucket cors-fun-dt --website-configuration file://website.json
```
##upload our index.html file and include a resource that would be cross origin
```sh
aws s3 cp index.html s3://cors-fun-dt
```

##Get website endpoint for s3
```sh
#Could be this for us east
http://cors-fun-dt.s3-website.us-east-2.amazonaws.com
#also could be this for other regions
http://cors-fun-dt.s3-website-us-east-2.amazonaws.com
```
##apply a CORS policy