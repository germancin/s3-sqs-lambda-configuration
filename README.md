# S3 SQS && Lambda Pipeline

### 1. Create a SQS service

Create an standar `SQS Service`.

### 2. Create a lambda function

- Create a lambda function select`Author from scratch` 
- In the Lambda code add a console log so you can verify later is working.


### 3. Create a S3 bucket 

Create an S3 bucket.


# Let's create our pipeline

The goal here is make the `S3` to create a `SQS` which will trigger a `Lambda function`

Basically we need to connect them all and for this we will need several configurations in place and some roles to have permitions to write and send messages from the `S3` to the `SQS` and in the same way more permitions to connect SQS to trigger the `lambda fucntion`


### Create the permitions to connect `S3` with `SQS`

Go to the SQS you just create and go the the `Access Polici` and press Edit

Now the file should be like this where

`"Resource":` Is making reference to the current queue we want to link

`"aws:SourceArn":` Reference the bocket we want to connect to.

`"Service":` Is the service we want to use to connecto this 2 

If everythin is ok it will let you save other way will tell you the errors.

```
{
  "Version": "2008-10-17",
  "Id": "resize-policy-id",
  "Statement": [
    {
      "Sid": "resize-queue-statement-id",
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::046091930617:root",
        "Service": "s3.amazonaws.com"
      },
      "Action": "SQS:*",
      "Resource": "arn:aws:sqs:us-east-1:046091930617:resize-queue",
      "Condition": {
        "StringEquals": {
          "aws:SourceAccount": "046091930617"
        },
        "ArnLike": {
          "aws:SourceArn": "arn:aws:s3:*:*:resize-bc"
        }
      }
    }
  ]
}
```

### NOW !
Go to `S3` Service and now we are going to connect the `S3` bucke so it send the notification to the `SQS`

In the `S3 bucket` go to the `properties` section and add a `Event Notification`

Add a name.

Select the `All object create events` 

Go to the bottom and select 
`` SQS queue
    Send notifications to an SQS queue to be read by a server.``

Then Select the `SQS Service we create`











