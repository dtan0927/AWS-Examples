##Create a bucket
```sh
aws s3 mb s3://encryption-dt-bucket
```
##Create a file
```sh
echo "Hello World" > hello.txt
aws s3 cp hello.txt s3://encryption-dt-bucket
```

##Put Object with KMS encryption

aws s3api put-object \
--bucket encryption-dt-bucket \
--key hello.txt \
--body hello.txt \
--server-side-encryption aws:kms \
--ssekms-key-id

##Put Object SSE-C

export BASE_64_ENCODE_KEY=$(openssl rand 32 | base64)
echo $BASE_64_ENCODE_KEY

export MD5_VALUE=$(echo -n $BASE_64_ENCODE_KEY | base64 --decode | md5sum | awk '{print $1}' | base64)
echo $MD5_VALUE

aws s3api put-object \
--bucket encryption-dt-bucket \
--key hello.txt \
--body hello.txt \
--sse-customer-algorith, AES256 \
--sse-customer-key $BASE_64_ENCODE_KEY \
--sse-customer-key-md5 $MD5_VALUE

#aws example of sse-c key
openssl rand -out ssec.key 32

aws s3 cp hello.txt s3://encryption-dt-bucket/hello.txt \
--sse-c AES256 \
--sse-c-key fileb://ssec.key