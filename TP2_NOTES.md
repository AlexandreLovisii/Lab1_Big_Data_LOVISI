# Lab 2 - Notes on the errors encountered

## Context
- Bucket: user-a-lovisi-ece (created by opening "Personal Bucket" in Onyxia)
- S3 profile pasted from Onyxia (gear icon next to "default")

## Timeline
1. `aws s3 ls "s3://user-a-lovisi-ece/"`: NoSuchBucket (the bucket did not exist yet)
2. Opened "Personal Bucket" in Onyxia: the bucket now appears
3. Upload of users.csv:
   `An error occurred (InternalError) when calling the PutObject operation (reached max retries: 2): We encountered an internal error, please try again.`
4. Profile pasted again, same error
5. Upload of test.txt through the Onyxia interface: same error
I don't know what to do

## Conclusion
Reading (ls) works, but every write (PutObject) fails, both from the CLI and from the Onyxia interface.
The problem seems to come from the platform's S3 server.
