## AWSCLI-S3 Cheatsheet

### cp
```
# Copying a local file to S3
aws s3 cp test.txt s3://mybucket/test2.txt

# Copying a local file to S3 with an expiration date
aws s3 cp test.txt s3://mybucket/test2.txt --expires 2020-10-01T20:30:00Z

# Copying a file from S3 to S3
aws s3 cp s3://mybucket/test.txt s3://mybucket/test2.txt

# Copying an S3 object to a local file
aws s3 cp s3://mybucket/test.txt test2.txt

# Copying an S3 object from one bucket to another
aws s3 cp s3://mybucket/test.txt s3://mybucket2/

# Recursively copying S3 objects to a local directory
aws s3 cp s3://mybucket . --recursive

# Recursively copying local files to S3
aws s3 cp myDir s3://mybucket/ --recursive --exclude "*.jpg"

# Recursively copying S3 objects to another bucket
aws s3 cp s3://mybucket/ s3://mybucket2/ --recursive --exclude "another/*"

# Uploading a local file stream that is larger than 50GB to S3
# The following cp command uploads a 51GB local file stream from standard input to a specified bucket and key. The --expected-size option must be provided, or the upload may fail when it reaches the default part limit of 10,000:
aws s3 cp - s3://mybucket/stream.txt --expected-size 54760833024

```

#### ls

```
# Listing all user owned buckets
aws s3 ls

# Listing all prefixes and objects in a bucket
aws s3 ls s3://mybucket

# Listing all prefixes and objects in a specific bucket and prefix
aws s3 ls s3://mybucket/noExistPrefix

# Recursively listing all prefixes and objects in a bucket
aws s3 ls s3://mybucket --recursive

# Summarizing all prefixes and objects in a bucket
aws s3 ls s3://mybucket --recursive --human-readable --summarize
```

#### mb
```
# Creates a bucket
aws s3 mb s3://mybucket
aws s3 mb s3://mybucket --region us-west-1

```

#### mv
```
# moves a single file to a specified bucket and key
aws s3 mv test.txt s3://mybucket/test2.txt

# moves a single s3 object to a specified bucket and key
aws s3 mv s3://mybucket/test.txt s3://mybucket/test2.txt

# moves a single object to a specified file locally
aws s3 mv s3://mybucket/test.txt test2.txt

# moves a single object to a specified bucket while retaining its original name
aws s3 mv s3://mybucket/test.txt s3://mybucket2/

# 
