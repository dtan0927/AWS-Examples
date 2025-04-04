##Make bucket

aws s3 mb s3://metadata-fun-dt

##Create a new file
echo "Hello Mars" > hello.txt

##Upload file with metadata

aws s3api put-object --bucket="metadata-fun-dt" --key="hello.txt" --body hello.txt --metadata Planet=Mars

##Get metadata through head objext

aws s3api head-object --bucket="metadata-fun-dt" --key="hello.txt"