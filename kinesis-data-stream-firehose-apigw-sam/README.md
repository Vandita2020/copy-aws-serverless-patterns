# Kinesis Data Stream to API Gateway via Data Firehose

This sample project demonstrates how to send data received by Kinesis Data Stream to a HTTP Endpoint with Authorization (here API Gateway REST API) using Kinesis Firehose

Learn more about this pattern at [Serverless Land Patterns](https://serverlessland.com/patterns/kinesis-data-stream-firehose-apigw-sam).

Important: this application uses various AWS services and there are costs associated with these services after the Free Tier usage - please see the [AWS Pricing page](https://aws.amazon.com/pricing/) for details. You are responsible for any AWS costs incurred. No warranty is implied in this example.

## Requirements

* [Create an AWS account](https://portal.aws.amazon.com/gp/aws/developer/registration/index.html) if you do not already have one and log in. The IAM user that you use must have sufficient permissions to make necessary AWS service calls and manage AWS resources.
* [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html) installed and configured
* [Git Installed](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [AWS Serverless Application Model](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-install.html) (AWS SAM) installed

## Deployment Instructions

1. Create a new directory, navigate to that directory in a terminal and clone the GitHub repository:
    ```
    git clone https://github.com/aws-samples/serverless-patterns
    ```
1. Change directory to the pattern directory:
    ```
    cd kinesis-data-stream-firehose-apigw-sam
    ```
1. From the command line, use AWS SAM to deploy the AWS resources for the pattern as specified in the template.yml file:
    ```
    sam deploy --guided
    ```
1. During the prompts:
    * Enter a stack name
    * Enter the desired AWS Region
    * Enter Secret Name. To use default, click Enter.
    * Allow SAM CLI to create IAM roles with the required permissions.

    Once you have run `sam deploy --guided` mode once and saved arguments to a configuration file (samconfig.toml), you can use `sam deploy` in future to use these defaults.

## Testing

* Visit [Kinesis Management Console](https://us-east-1.console.aws.amazon.com/kinesis/home)
* Select 'Data streams', copy name of the Data Stream having prefix `firehose-apigw-MyKinesisStream-`.
* Replace  `<KinesisDataStreamName>` in the following command with the copied name of the Kinesis Data Stream in above step to get the test command.
  ```
  aws kinesis put-record --stream-name <KinesisDataStreamName> --partition-key 001 --data $(echo -n "{\"hello\" : \"world\"}" | base64)
  ```
* Run the above command a few times and check the logs of Test Lambda Function to see the records put to Kinesis Data Stream

## AWS Documentation
- [Stream data to an HTTP endpoint with Amazon Kinesis Data Firehose](https://aws.amazon.com/blogs/big-data/stream-data-to-an-http-endpoint-with-amazon-kinesis-data-firehose/)
- [Kinesis Data Firehose HTTP Endpoint Destination](https://docs.aws.amazon.com/firehose/latest/dev/create-destination.html#create-destination-http)

## Cleanup

1. Delete the stack
    ```bash
    sam delete
    ```

