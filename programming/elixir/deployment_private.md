## Regions

EC2: ap-northeast-2
S3: ap-northeast-2
RDS: ap-northeast-2
Elasticsearch Service: ap-northeast-2
CodeBuild: ap-northeast-1
ECS: ap-northeast-1


## AWS ElasticSearch Service

딴건 모르겠고 snapshot time 은 19:00UTC 로. (한국 새벽 4시)

Instance count 는 나중에라도 신경써야 할 부분. (shard)

access policy 는 IP(ec2)와 user(kibana 접속을 위해) 로 세팅

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "",
      "Effect": "Allow",
      "Principal": {
        "AWS": "*"
      },
      "Action": "es:*",
      "Resource": "arn:aws:es:ap-northeast-2:692650672373:domain/elixir-test/*",
      "Condition": {
        "IpAddress": {
          "aws:SourceIp": [
            "13.124.102.153",
            "211.245.121.131" // my ip
          ]
        }
      }
    },
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::692650672373:user/jinkyou"
      },
      "Action": "es:*",
      "Resource": "arn:aws:es:ap-northeast-2:692650672373:domain/elixir-test/*"
    }
  ]
}



replica 세팅..
number_of_shard, number_of_replicas 에 대해서는 제대로 된 파악이 필요.

Reference: https://cloudncode.blog/2017/01/16/how-to-set-up-elastic-search-kibana-on-aws/


## ECR 세팅

permission
Unable to pull customer's container image.
https://forums.aws.amazon.com/thread.jspa?messageID=760990&tstart=0


## CodeBuild 세팅

https://medium.com/mint-digital/elixir-deployments-on-aws-ee787aa02a9d

ECR 에서 퍼미션 줘야함
CodeBuildRolePolysy?

Buildspec
http://docs.aws.amazon.com/ko_kr/codebuild/latest/userguide/build-spec-ref.html

Docker 로 ecr 에 올리기
http://docs.aws.amazon.com/ko_kr/codebuild/latest/userguide/sample-docker.html

https://forums.aws.amazon.com/thread.jspa?messageID=761184&#761184
custom 은 안돼! 하지만 될지도 몰라?

role
http://docs.aws.amazon.com/ko_kr/codebuild/latest/userguide/setting-up.html#setting-up-service-role


## VM 세팅

이것 때문에 encoding 세팅
warning: the VM is running with native name encoding of latin1 which may cause Elixir to malfunction as it expects utf8. Please ensure your locale is set to UTF-8 (which can be verified by running "locale" in your shell)

build

이것저것

run

이것저것



