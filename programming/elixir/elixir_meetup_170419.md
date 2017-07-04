# A practical Guide to Protocols

Protocol

clown nose -> Abstraction

Programes are made of two element
data  & operations

expression problem?!

We want to add new data (types) and new oepratios without modifying existing ones

oop
add data? ok
add operation? no!

functional programming
add data? no
add operation? ok!

this is the expression problem

Protocol! can sollve this problem by decoupling the definition of an operation from it's implementation.

(influenced by clojure)
                  
                  Do I have the implementation of the function?
Datatype -> Protocol -> Implementation


implement protocol in the custom datatypes.

functional programming + protocol
add data? ok!
add operation? ok!


protocol or behavior

behavior: module that confirms some specs..(error at compile)

Can each implementation of my operation take the same data type?
yes -> behavior
no -> protocol

ex) %Message{to: , subject:, body:}

defmoudle Mailer do
  def deliver_now(message) do
    apdater.deliver
  end
end

defmodule SMTPAdapter do
  deliver(message) do: .
end

so on so on 


!Don't get carried away!


## 통합 cdci

- daily cd
- why aws?
- why elastic beanstalk?

continuous deployment?
ci 보다 넓은 범위. release 까지.

주로 computing 만 하는 서버군에 적용하기 쉬움 (rest api)
반대로 뭔가 저장하는 서버군은 적용하기 힘듦. (db, storage)

devops 에서 굴러보니..
- 자동화는 장기적으로 언제나 승리한다.
- repeatable, reproducible, reliable
- 서버는 오래되면 갑자기 맛이 간다. ec2 라 할지라도
- reboot 한지 오래 된 서버일 수록 위험하다

추구
non-stop server patch
ha, dr ? 
항상 깨끗한 서버.

목표.
매일 vm 새로 다시 deployment 해서 이전 서버와 교체하자 (하루살이 서버)
3r
non-stop
ha, dr

so, why aws?

not ec2 server! ec2 instance
vm 역시 bug 가 있는 software
언제든 갑자기 망가질 수 있음.
=>"빠른 복구"가 가능하도록 system architecture 를 구성해야한다!

aws
높은 신뢰성
3rd party
낮은 비용
다양한 troubleshooting. 이미 문제를 겪은 사람들이 많았어서 솔루션 찾기가 쉬움.
지속적 확장중

1 ec2 + elb 조합으로 daily cd 도전
절반 정도를 떼서 패치.
패치한것 붙인 후에 나머지 떼고 패치.

문제점:
AMI version 관리가 힘듦.
...

2 elasticbeanstalk
elb 단위로 (eb env) 통째로 교체 (cname swapping)

단점:
eb 의 동작원리를 이해해야함
기본설정을 너무 건드리면 알 수 없는 문제가 발생할 수 있음
교체한 후에도 dns caching 때문에 1시간 정도 바뀌어야 실제로 바뀜

장점:
요구사항 만족
..
* 서버 작게 쪼개서 t2 띄우면 bonus cpu credit! 으잉

tiamat (opensource)

daily cd 단점
provisioning code 관리에 공수가 아주 없지 않음
철학을 이해 못하면 전체 운영이 어려워짐
'기능 구현, bug 수정이 급한데, 왜 이걸로 시간과 돈을 들임?'
이건 개발 배포속도를 빠르게 하는게 아니라 덜 느려지게 하는 것이다


2부!

CI
build & package 를 자주 행함
코드 병합이 되었을 때 생기는 문제를 미리 감지
언제든 최신 build 를 고객에게 바로 제공가능

Cd
deployment 를 자주 행함
system, application 최대한 fresh하게
장시간 운영 시 발생하는 문제를 예방

기존: jenkins, bamboo 등 이용

but,
설치/운영비용 소요
여러 job 들이 같은 서버에서 실행해서 side effect.
활용률 매우 낮음. 24시간 안돌려!

github + travis 최적의 조합. codeship 도 좋아여..
docker 기반. 정말 쉬움.

하지만
job 기반이 아닌 저장소 기반
GUI 에서 할 수 있는게 거의 없음
cronjob 이 beta
cron expression 을 지원 안함. ?

lambda cron + travis ci api

결과!
높은 신뢰성 (managed + managed)
문제 생기면 slack 으로 바로 noti
3000 build 동안 중단 및 장애 거의 없음.

여러개 돌릴 수록 막대하게 저렴.

then, code build & code deploy?
충분한 reference 없음.
기존에 비해 충분한 기능?

가능성
안정성, 가격측면!

한가지를 잘 하는 것들을 만들고, 인터페이스를 좋게 만들고, 같이 일하도록 하라. unix
