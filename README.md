# aws-s3-signed-url-burn-after-reading

Project designed for invalidation of S3 objects that are temporarily stored in particular S3 bucket. (file share)
You can use delete or move "burn after reading" mechanism however with the move, there is still need to create some
random path to store moved objects (otherwise it can be easily guessed).

## Usage
Just create new AWS stack from **s3-signed-url-burnafterreading.yaml** template and use.
In order to create the stack you need to have required permissions for createing Cloudtrail Trail, Lambda Function
and Cloudwatch Event Rule.