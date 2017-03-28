## AWS CodeBuild

https://aws.amazon.com/codebuild/

A build service provided by AWS.

You can have your own build server very easily.


### Benefits

Scaling: It runs each build immediately and concurrently.

Pay as You Go: You are charged based on the number of minutes it takes to complete your build.
(Free tier: 100 min / each month)


### Tutorial

http://docs.aws.amazon.com/ko_kr/codebuild/latest/userguide/sample-ruby-hw.html

[Example source codes](./codebuild_tutorial_source)

We're gonna use `awscli` to create and run this tutorial.


#### Create project

Fill the params of `create-project.json`.

For example,
```json
// create-project.json
{
  "name": "sample-ruby-project",
  "source": {
    "type": "S3",
    "location": "sample-ruby-project-source/RubySample.zip"
  },
  "artifacts": {
    "type": "S3",
    "location": "sample-ruby-project-bucket",
    "packaging": "NONE",
    "name": "build"
  },
  "environment": {
    "type": "LINUX_CONTAINER",
    "image": "aws/codebuild/ruby:2.3.1",
    "computeType": "BUILD_GENERAL1_SMALL"
  },
  "serviceRole": "arn:aws:iam::xxxx:role/service-role/codebuild-elixir-test-service-role"
  "encryptionKey": "arn:aws:kms:ap-northeast-1:xxxx:alias/aws/s3",
}
```
>You need to create encryptionKey, serviceRole first.

Run create-project command.
```
aws codebuild create-project --cli-input-json file://create-project.json
```

Reference: http://docs.aws.amazon.com/ko_kr/codebuild/latest/userguide/create-project.html#create-project-cli


#### Upload source to s3
```
aws s3 cp RubySample.zip s3://sample-ruby-project-source/
```


#### Run build

Run start-build command.
```
aws codebuild start-build --project-name sample-ruby-project
```

That's all! Check the artifacts are in your S3 repository.
