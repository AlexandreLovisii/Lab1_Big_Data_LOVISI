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
echo "$LAB_BUCKET_NAME"
aws s3 --profile 'default' ls "s3://$LAB_BUCKET_NAME/"
ls -lh orders_large.csv

## Update: S3 incident resolved
After the teacher fixed the platform, uploads worked again. The next error was `InvalidAccessKeyId`,
caused by expired temporary credentials. Pasting the S3 profile script again from Onyxia solved it.
The S3 lab was then completed: upload, metadata, presigned URLs, multipart, versioning, lifecycle,
bucket policy (the delete was correctly denied, then the policy was removed), consistency and cleanup.

## Lab 4 - DuckDB
- `Authentication Failure` when reading S3: the persistent secret `s3_onyxia_connection` was outdated.
  Fixed by exporting the current profile credentials (`aws configure export-credentials`) and
  recreating the secret with `CREATE PERSISTENT SECRET ... PROVIDER credential_chain`.
- `bronze/` had been emptied by the S3 lab cleanup, so `users.csv` and `orders.csv` were generated and uploaded again.
- SQL part done in the DuckDB CLI: reading CSV from S3, tables, quality checks, aggregations, joins,
  window functions, pivot and exercises.
- Parquet part: export, Hive partitioning, CSV vs Parquet comparison.
