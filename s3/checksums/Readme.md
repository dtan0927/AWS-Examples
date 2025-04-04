#Create a new s3 bucket
```md
aws s3 mb s3://checksums-examples-dt-123
```

#Create a file that we will do a checksum on

```
echo "Hello Mars" > myfile.txt
```

#Get a checksum of a file for md5
md5sum myfile.txt
#8ed2d86f12620cdba4c976ff6651637f  myfile.txt

##Upload our file to s3
```
aws s3 cp myfile.txt s3://checksums-examples-dt-123
aws s3api head-object --bucket checksums-examples-dt-123 --key myfile.txt
```

##Lets upload a file witha a different kind of checksum
```sh
sudo apt install rhash -y
rhash --crc32 --simple myfile.txt
```
```sh
aws s3api put-object \
--bucket="checksums-examples-dt-123" \
--key="myfilecrc32.txt" \
--body="myfile.txt" \
--checksum-algorithm="CRC32" \
--checksum-crc32="e7c80b87"
```