## AWS X-Ray Serverless Samples

These samples are originally pulled from AWS X-Ray Serverless Samples [here](https://github.com/aws-samples/aws-xray-serverless-samples).

The samples in this repository demonstrate different ways to integrate AWS X-Ray within a serverless application.

* **xray**: Simple tracing without code instrumentation.
* **xray-instrumented**: AWS X-Ray tracing with code instrumentation.

The **pipeline** folder contains an AWS CloudFormation template for a pipeline using AWS CodeCommit, AWS CodePipeline and AWS CodeBuild.

The **helpers** folder contains script to help deploy Serverless applications locally and run calls against API Gateway.

## Usage

### 1. Deploy

To deploy any sample, go to the sample folder and run the following commands:

```
export S3_BUCKET="serverless-samples-observability"
make
```

### 2. Send test traffic

To send test traffic for a particular sample, run this command in the sample folder:

```
make calls
```

By default, this will send 10 PUT requests and 500 GET requests.

### 3. Check traces

After sending test traffic, you can check traces and the service map in the [AWS Console](https://console.aws.amazon.com/xray/home).

### 4. Cleanup

To tear down resources, run this command in the sample folder:

```
make delete
```


## Requirements

The samples require these programs to be installed on your computer:

* [AWS Command Line Interface](https://aws.amazon.com/cli/)
* [AWS SAM CLI](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-install.html)
* [Docker](https://docs.docker.com/install/)
* [Go](https://golang.org/dl/)
* [Python 3](https://www.python.org/downloads/)

You would also need to install the [cfn_flip](https://github.com/awslabs/aws-cfn-template-flip) package for Python3. You can install it with Pip by running `python3 -m pip install cfn_flip`.

The easiest way to do this is to setup a Cloud9 environment on AWS and use it for experimentation. 
AWS Cloud9 is a cloud-based integrated development environment (IDE) that lets you write, run, and debug your code with just a browser. It includes a code editor, debugger, and terminal. Cloud9 comes prepackaged with essential tools for popular programming languages, including JavaScript, Python, PHP, and more, so you don’t need to install files or configure your development machine to start new projects.
[Getting started with AWS Cloud9](https://aws.amazon.com/cloud9/getting-started/))

Please delete the Cloud9 environment once you are done with experimentation.


## Troubleshooting

### I keep getting "socket: too many open files" errors when running "make calls"

The **get** program triggers 500 HTTP calls by default, which can exceed the default limit of open file descriptors. You can increase this limit by running `ulimit -n 4096`, which should be enough for the default case.

To learn more about this, check the ulimit help by typing `help ulimit` or the man page for `limits.conf`.

## License Summary

This sample code is made available under the MIT-0 license. See the LICENSE file.
