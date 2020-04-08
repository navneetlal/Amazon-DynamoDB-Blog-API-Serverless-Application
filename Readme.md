# Amazon DynamoDB Blog API Serverless Application Project

This starter project consists of:
* serverless.template - an AWS CloudFormation Serverless Application Model template file for declaring your Serverless functions and other AWS resources
* Function.cs - class file containing the C# methods mapped to the Serverless functions declared in the template file
* Blog.cs - file containing a C# class representing a blog entry in the DynamoDB table
* aws-lambda-tools-defaults.json - default argument settings for use with Visual Studio and command line deployment tools for AWS

You may also have a test project depending on the options selected.

The generated project contains a Serverless template declaration for a simple web API for blogging with the blog data stored in a DynamoDB table. The blogging API functions are hosted as a set of AWS Lambda functions that will be exposed through Amazon API Gateway as HTTP operations. Edit the template to customize the functions or add more functions and other resources needed by your application, and edit the function code in Function.cs/Blog.cs. You can then deploy your Serverless application.

## Here are some steps to follow from Visual Studio:

To deploy your Serverless application, right click the project in Solution Explorer and select *Publish to AWS Lambda*.

To view your deployed application open the Stack View window by double-clicking the stack name shown beneath the AWS CloudFormation node in the AWS Explorer tree. The Stack View also displays the root URL to your published application.

## Here are some steps to follow to get started from the command line:

Once you have edited your template and code you can deploy your application using the [Amazon.Lambda.Tools Global Tool](https://github.com/aws/aws-extensions-for-dotnet-cli#aws-lambda-amazonlambdatools) from the command line.

Install Amazon.Lambda.Tools Global Tools if not already installed.
```bash
    dotnet tool install -g Amazon.Lambda.Tools
```

If already installed check if new version is available.
```bash
    dotnet tool update -g Amazon.Lambda.Tools
```

Execute unit tests
```bash
    cd "BlueprintBaseName/test/BlueprintBaseName.Tests"
    dotnet test
```

Deploy application
```bash
    cd "BlueprintBaseName/src/BlueprintBaseName"
    dotnet lambda deploy-serverless
```

## using sam

We can also use [AWS SAM](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/what-is-sam.html) for deploying our serverless application. Since also provide functionality of testing and debugging locally.

To do so, first install [AWS SAM CLI](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-install.html) and follow the commands below.

Start AWS DynamoDB local
```bash
    docker create network --driver bridge lmbda-local
    docker-compose up -d
```

Create a table in local DynamoDB
```bash
    aws --profile local dynamodb create-table --cli-input-json file://blog-table.json --endpoint-url http://localhost:8000
```

Build the application before testing any api's
```bash
    sam build --template serverless.template
```

Start the api's locally
```bash
    sam local start-api --docker-network lambda-local --profile local
```
