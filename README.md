# aws-s3-signed-url-burn-after-reading

Project designed for invalidation of S3 objects that are temporarily stored in particular S3 bucket. (file share)
You can use delete or move "burn after reading" mechanism however with the move, there is still need to create some
random path to store moved objects (otherwise it can be easily guessed).

## How it works
Cloudformation stack creates multiple resources. First Cloudtrail Trail is created to get all GetObject events in account. After that Cloudwatch rule is created to trigger Lambda function when there is a GetObject event on defined S3 bucket and path. Lambda function then either delete object from path or move it to /invalid path within the S3 bucket. Signed URL invalidation (burn after reading mechanism) will take roughly 2-5 seconds - during that time the object is still available on signed URL (if not already expired).
Unfortunatelly there is no possibility to trigger Lambda directly from S3 - GetObject event is not in available triggers - therefore we had to use Cloudtrail and Cloudwtch in order to make this functional.

## Usage
Just create new AWS stack from **s3-signed-url-burnafterreading.yaml** template and use.
In order to create the stack you need to have required permissions for createing Cloudtrail Trail, Lambda Function
and Cloudwatch Event Rule.
