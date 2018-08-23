# AWS Summit

## 시골개발자

### t2.family

가격 대비 성능 우수
CPU credit 에 제한이 있음. 나중에는 속도가 느려짐.
-> 모니터링, 스트레스 테스팅이 필요
cloud watch 같은거로 봐도 되겠네요.

cpu 사용을 줄이도록 해보자.
zabbix 를 이용해서 aws SDK -> cloud watch 를 보는 식으로 하려고 해봤지만 cpu 소모가 커서 크레딧이 떨어짐
=> lambda 로 모니터링을 하도록 하여 문제 해결
=> 아예 lambda 로 하지 왜?

cloudflare CDN 를 이용해서 정적 요소들을 다 처리함.

pay-per-use service 사용. lambda, s3 를 많이 사용.
통계처리
s3 로 데이터를 업로딩 lambda 에서 가져와서 처리 후 s3 로 다시 보냄

notification system for aws maintenance
이메일로만 받으면 놓칠 가능성이 높음
cloudwatch 에서 하루 한 번 lambda 를 돌리고 각 계정별 maintenance 를 처리한 후 slack 으로 보냄. KMS?

Bigdata analysis
사진, 관광객, wiki access log, open data 를 이용해 관심도 처리.
lambda, dynamodb,cloud vision

aws 는 소규모에서 쓰기 좋다
t2.family 싸고 좋음.
+ pay-per-use 로 싸게 ...


### javascript tools

browser sdk?

javascript sdk

lambda + aws-sdk

amazon api gateway - you can generate your own sdk

lambda + step functions


## Lambda Can Do That?!?!

셀피 찍고 트위터에 올리면 자도으로 받아서 닌자로 변환하고 자기 트윗에 올리는 작업을 보여줌.

lambda 의 제한은 당신의 코드에만 있을뿐

randhunt@amazon.com

service unit of scale level of abstraction
ec2 vm h/w
ecs task os
lambda function runtime

async or sync

rails 도 lambda 에 올릴 수 있다고?


You can do anything.

focus on the business logic


AWS lex - chat bot

serverless application model sam

com.amazonaws.serverless.* (github.com/awslabs)
labmda-refarch-* (github.com/awslabs)

local testing: localstack, palcebo, moto
fake events: s3.json, kinesis.json


## microsoft architecture

service-oriented architecture - 서비스들이 네트워크를 통해 서로 통신한다
loosely coupled elements - 서비스는 독립적으로 업데이트하며 서로 영향을 주지 않는다
bounded contexts - 다른 서비스의 내부 구조를 알지 못해서, 내 서비스 코드를 업데이트 할 수 있다.

구성
data store + application/logic
public api를 통해 서로 통신

패턴

전통적: elb - ec2(s) - rds
좀 더 유연하게? eb

content delivery - api layer - application layer - persistency layer

api layer -> api gateway 사용
application layer -> ecs 로 배포하면 빠름. 혹은 lambda
persistency layer -> dynamodb 로 변경하면 성능이 유동적

vingle 의 사례

* opsworks?

ror 서버 하나에 모든게 다 들어있었어서 unit test 30 분 deployment 30 분 걸렸음..

* kurt lee..

문제점
언제나 모든 서비스를 함께 deploy / scale
ex) front 만 늘어날때 그냥 통째로 늘리는 수 밖에..
새로운 기술 도입이 어려움
기술적으로 자유로운 사고가 어려움! 생산성 저하.

new goal
independent +
scaling
deployment
stack
development
testing & monitoring


* API 변경이 있을 때는 어떻게 하는거죠?
* http 통신을 하여 생기는 latency 는요?
* cloudwatch + slack noti

lambda!
모든 infrastructure 를 code 로 관리
사실상 무한, 자동 스케일링 (lambda + dynamodb!)
code 를 upload 만 하면 무중단 배포

* serverless + typescript

로직에만 집중!
cloudwatch dashboard 로 서비스 상태 파악 용이

lesson learned

1. 새로 추가되거나 변경이 필요한 기능부터 하나씩 분리
- 잘 돌아가고 있는 오래된 기능의 재작성은 리스크 높고 이득도 적음
- 리스크가 작은 것부터 시작해서 팀 단위 운영/개발 노하우를 쌓아야함

2. business domain 단위로 서비스 구성
- cache, db (x)
- feed, notification (o)

3. 서비스의 존재 목적은 사용 되어지는 것
- 다른 개발자 / 시스템에서 쓰기 쉽도록 인터페이스를 갖춰야함
- rest api 라면 swagger 등을 통해 문서화

* cloudsearch? kinesis stream?

4. infrastructure as a code! (aws cloudformatino)
시간이 조금만 지나면, aws 내 많은 리소스를 관리하기 어려워짐.
aws cloudformation 을 통해 리소스들을 코드화/데이터화

모범사례1
lambda version 기능
api gateway 스테이지 기능 (변수 조정가능)

모범사례2
polyglot
개별적인 데이터 스토어 구성 => 빠르고 독자적인 확장성 제공
복구.. 각 서비스 마다 롤백이 가능해야한다. 관리해줘야함.
=> aws step function!
시작적 워크플로를 사용해 분산 앱 및 마이크로서비스 구성 요소 저장 및 실행
lambda 와 함께
(lambda 에서 다음꺼 부르고 이러지 않아도 step function 이 다 관리해줌)

모범사례3
api 외부요소 모니터링
latency, rps, error rate
내부 모니티렁
cloudwatch, os, application, 
...

실시간 로그 대시보드 구성

cloudwatch logs -> elasticsearch -> kibana
s3 -> athena (query) -> quicksight

x-ray
ec2 에ㅓ 설치해서 사용.
완전 관리형 분산 애플리케이션 성능 추적 서비스. 마이크로서비스 시작과 끝에 대한 디버깅 및 추적.

모범사례4
보안

모범사례5
api 생태계 확산을 통한 비지니스 창출

api gateway developer portal
api monetization in marketplace

모범사례6
기술 너머 조직의 변화

모범사례7
자동화!

* aws code start


## Docker swarm on AWS

cf 를 이용하여 aws docker swarm cluster 생성.
쉽고 빠르게 무중단, 모니터링까지.

* docker swarm?

clust 내에서 단체로 짜잔


Docker swarm on aws

docker for aws (cf 설정)
elb - manager nodes(1, 3, 5 ..) - worker nodes

vs ECS: ECS 만큼 쉽고 몇가지 더 낫기도 하다
vs Kubernetes 더 다양한 기능을 제공하지만 설정과 관리가 어렵다.

* 발표자 팔로우!

## cf

cf 를 사용한 인프라 설계
cp 설정을 위한 cf

CI: 소스 -> 빌드
CDelivery: 소스 -> 빌드 -> 테스트 -> (검수) -> 프로덕션
CDeployment: 소스 -> 빌드 -> 테스트 -> 프로덕션

인프라 지속적 전달을 위해 필요한 것은 무엇인가요?
인프라를 코드로 취급하는 방법
인프라 리소스를 생성하고 업데이트하는 워크플로우를 관리할 수 있는 도구
변경사항을 테스트 하고 검수할 수 있어야함
=> 코드형 인프라 + 워크플로(빌드 프로세스)
CF + CP
(CF 버저닝도 된대)

yaml 되면서 많이 시워졌다.
visual 로도 설정 가능
change set 으로 미리 어떻게 변할지 확인 가능
서로 참조 가능
모듈화 가능

github.com/awslabs/ecs-refarch-cloudformation
ECS 기반의 MSA

아키텍처 이쁘다.
