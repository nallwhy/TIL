# THE LITTLE Elixir & OTP GUIDEBOOK

written by [Benjamin Tan Wei Hao](http://benjamintan.io/).

## 1. Introduction

Elixir 가 Erlnag 위에서 만들어졌기 때문에, Elixir 에 대한 얘기를 시작 전에 Erlang 과 Erlang 의 전설적인 VM 에 대해 얘기하고 넘어가겠다.

Erlnag 은 [soft real-time](https://en.wikipedia.org/wiki/Real-time_computing), distributed, concurrent system 을 만드는데 아주 뛰어난 언어이다.

Criteria for real-time computing
A system is said to be real-time if the total correctness of an operation depends not only upon its logical correctness, but also upon the time in which it is performed.[5] Real-time systems, as well as their deadlines, are classified by the consequence of missing a deadline:

Hard – missing a deadline is a total system failure.
Firm – infrequent deadline misses are tolerable, but may degrade the system's quality of service. The usefulness of a result is zero after its deadline.
Soft – the usefulness of a result degrades after its deadline, thereby degrading the system's quality of service.
Thus, the goal of a hard real-time system is to ensure that all deadlines are met, but for soft real-time systems the goal becomes meeting a certain subset of deadlines in order to optimize some application-specific criteria.

이는 원래 Ericsson 의 telephone switch 를 프로그래밍하기 위해 사용되었다.

이 switch 들은 concurrent, reliable, scalable 해야했다. 거기에 dropped call 이 다른 call 들에 영향을 끼쳐서는 안됐다. 이런 요구사항들이 현재의 Erlang 을 만들었다. 그리고 이는 현재 multicore, web-scale programming 에서 요구하는 것과 같다.

Erlang VM 의 scheduler 는 자동으로 workload 를 processor 들에 분배한다. 이는 더 많은 processor 를 이용할 때 거의 추가비용 없이 성능 향상을 얻을 수 있다는 얘기다.

### 1.1 Elixir

Elixir 는 스스로를 Erlang VM 위에 만들어진 functional, meta-programming-aware language 라고 소개한다.
- functional programming language: immutable state, higher-order functions, lazy evaluation, patern maching 같은 유용한 feature 들을 포함한다.
- meta-programming language: code 가 code 를 만들어내는 것을 의미한다. 이는 code 가 data 로, data 가 code 로 표현될 수 있기 때문에 가능하다.

이 책은 fault-tolerant, scalable, distributed application 을 만들기 위한 framework 인 OTP 에 대한 것이기도 하다.
OTP 가 Erlang distribution 의 일부로 포함되기 때문에 Elixir 도 이를 이용할 수 있다. OTP는 다른 framework 들과는 다르게 세 가지 database, debugging tools, profilers, test framework 등 매우 좋은 요소들을 포함한다.

### 1.2 How is Elixir different from Erlang?

Elixir 와 Erlang 의 차이를 얘기하기 전에 비슷한 점부터 얘기해보자. 둘 다 같은 bytecode 로 컴파일 된다. 즉, 컴파일 되고 나면 같은 VM 에서 돌릴 수 있다.

Elixir 는 Erlang 코드도 바로 호출할 수 있고, 반대도 가능하다. Elixir 에는 없는 기능이 필요할 때 Erlang library 를 이용할 수 있다.

Elixir 는 Erlang 의 semantics 을 따른다.

그럼 왜 Erlang 대신 Elixir 를 사용하는가?

#### 1.2.1 Tooling

##### Interactive Elixir

Interactive Elixir shell(iex) 는 read-eval-print loop (REPL) 이다.

node 들에 연결할 수 있기 때문에 같은 컴퓨터, 네트워크 에서 여러 runtime 들을 돌려 서로 얘기할 수 있게 한다.

`IEx.pry` 를 이용해 debbuging 도 할 수 있다.

iex 에는 계속 새로운 것들이 추가되고 있으니 changelog 를 유심히 보시길!

##### Teting with ExUnit

asynchronously, with beautiful failure message

##### mix

`mix`는 Elixir project 를 만들고 컴파일하고 테스팅하는데 쓰이는 build tool 이다. dependency 관리도 한다.

##### Standard Library

좋다. Erlang 에는 없는 `Stream` 같은 것도 가지고 있다. OTP 에 기능을 추가해 state 를 다루는 `Agent`, one-off asynchronous computation 을 위한 `Task` 등을 만들었다.

##### Metaprogramming

Elixir 는 LISP 같은 macro 를 만들었다. 기존에 있는 것을 이용해 새로운 construct 를 만들거나 boilerplate code 를 줄이기 위해 library 제작자들이 많이 이용한다.

#### 1.2.2 Ecosystem

##### Thank you, Erlang!

Erlang 에 있는거 다 가져다 쓸 수 있다.

##### Learning Resources

좋다

##### Phoenix

Elixir 로 쓰인 web framework 인데, response time 이 micro seconds 단위로 작고, websocket 을 지원하며 OTP 를 이용할 수 있다.

##### It's still evolving

다른 language 들로부터 좋은거 열심히 가져오는 중

### 1.3 Why Elixir and not X?

- Is Elixir gaining traction?
- Are jobs available in Elixir?

아직 어리다. 하지만 functional language 들이 뜨고 있다. Erlang 도 distributed system, IoT 등으로 뜨고 있고 이는 Elixir 로도 이어진다. 나오고서 많은 사람들을 끌어들이고 있지는 않지만, 사용하는 초기 사용자들에게는 매우 큰 보상이 주어지고 있다.

### 1.4 What is Elixir/OTP good for?

- Concurrent
- Scalable
- Fault-tolernat
- Distributed

Good for:
- Chat servers (WhatsApp, ejabberd)
- Game Servers (Wooga)
- Web frameworks (Phoenix)
- Distributed Databases (Riak and CouchDB)
- Real-time bidding servers
- Video-streaming services
- Long-running services/daemons
- Command-line applications

server-side software 를 만들기에 매우 좋다.
- Serve multiple users and clients, often numbering in the thousands or millions, while maintaing a decent level of responsiveness
- Stay up in the event of failure, or have graceful failover mechanisms
- Scale gracefully by adding either more CPU cores or additional machines

Not good for:
- Image processings
- Computationally intensive tasks
- GUI applications
- Hard real-time systems


## 2. A whirlwind tour

skip


## 3. Processes 101

Process 는 Elixir concurrency 기본 단위. Erlang VM 에서 지원하는 process 수는 134 million!

### 3.1. Actor concurrency model

Erlang (그리고 당연히 Elixir) 는 Actor concurrency model 을 사용한다.

- 각 _actor_ 는 _process_
- 각 프로세스는 _specific_task_ 를 수행한다
- 프로세스에게 무엇을 하라고 하기 위해서는 _message_ 를 보내야 한다. 프로세스는 다른 메시지로 답신 가능.
- 프로세스 마다 act 할 수 있는 메시지가 다르다. 메시지는 parttern-matched 된다.
- 프로세스는 다른 프로세스들과 어떤 정보도 공유하지 않는다.

object oriented 와 무엇이 다른가?
- 관심 없는 메시지 무시
- 정보 공유하지 않음

### 3.2. Building a weather application

동시에 100개 도시 온도 받아오기!

#### 3.2.1. The naive version

