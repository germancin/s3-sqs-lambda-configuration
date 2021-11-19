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




