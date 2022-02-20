# Lambda To SQS
This is a very simple script that can be deployed as a Lambda function in order to push JSON messages onto an SQS queue.

Also See:
- [SQS Webhook Listener](https://github.com/codebykyle/sqs-webhook)

## Deployment
Create a new Lambda function and add an API Gateway trigger, so that the Lambda function can be reached from the internet.

Copy and paste the content of `lambda_function.py` and save it.

### Permissions
In the configuration for the function, in the Permissions tab, ensure that the function has access to your SQS Queue. 

This can be done with an inline policy.

Here is an example policy:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "sqs:SendMessage",
            "Resource": "your-queues-arn-goes-here"
        }
    ]
}

```


### Environment Variables
In the configuration, go to  Environment variables. There, you must add the following:

| Variable              | Required | Description                                                                              | Default Value             |
|-----------------------|:--------:|------------------------------------------------------------------------------------------|:--------------------------|
| SQS_QUEUE             |    ✔     | The Name of the queue you are pushing to. You can copy this from the SQS page.           |                           |
| SQS_SECRET_ACCESS_KEY |    ✔     | The Queue URL of the queue you are pushing to. This can also be copied from the SQS page |                           |


## Usage

Send a request to the URL you receive in the API Gateway. The body of that request will be pushed into the SQS for processing.


## To do
This can likely be automatically deployed and the code can be further improved to filter out non-compliant requests.

Please feel free to submit a pull request if you'd like to tackle this.