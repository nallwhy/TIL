## Why processes trump objects

by Kevin Rockwood.

https://speakerdeck.com/rockwood_slides/elixir-why-processes-trump-objects

### What is Object Oriented?

#### 우리가 듣던것

* Classes
* Methods
* Instances
* Inheritances

#### Let's look at Computer Science Histroy

1940 birth  
1940-1990 Figuring it out  
1990 Object Oriented! Java!

1970년대에 ALAN KAY 라는 쩌는 사람이 객체지향언어의 실질적 원조인 Smalltalk 를 만들었다.  
그 당시 그는 procedure, rigid, structural 한 programming 방식에서 벗어나기 위해 고민했었고,  
molecular biology 도 전공했던 그는 지금의 programming 이 machine 이라면 body 와 같은 방법은 어떨까 상상해보았다.

* 각각의 cell 이 자신의 state 를 가지고 있으면서 완전히 나눠져있고
* 다른 셀과 전달을 통해 데이터를 주고받고
* cell 이 죽어도 생명 자체는 죽지 않는다.
* 거기에 body 는 이미 super complicated system 임이지 않은가! 검증된 방법이다.

이것이 ALAN KAY 가 생각했던 object 였다.
class 나 inheritance, method 같은 얘기는 없었음!

#### So, What is Object Oriented?

* should be completely isolated
* should be only communicate via message passing
* should be be fault tolerant

This is a lot like the internet.


#### Erlang

1986  
Ericsson

What they needs:

* Distributed
* Fault-tolerant
* Real-time
* Highly available

=> Erlang / OTP Framework!

Erlang

* Dynamic
* Compiled
* Functional
* Immutable
* Everthing is a Process - Very lightweight computing process. 1ms - 2ms to responce? isolated

OTP Framework  
managing processes easier

* Implements the actor model with Erlang processes
* Libraries for managing the proess lifecycle
* Hot code swapping
* Data persistance

인터넷에서 필요한거랑 비슷하네? 웹으로 옮겨보면 어떨까?!


#### Elixir

2011
José Valim
Erlang 은 old 한 부분이 많았다. syntax, testing, ...  
=> Erlang ecosystem 에서 돌아가는 현대적 언어를 만들어보자!

##### Processes communicate via messages

process 가 쏜 message 를 mailbox 가 message 를 저장해둔다.  
processes have state.

##### Fault Tolerance

Failures will happen  
Don't try protecting against every possible error condition  
Let each part of your program reboot itself (not taken down the whole system)  
Supervison tree

Reboot! 대부분의 problem 의 원인은 state 이기 때문에 리스타트 하면 다 해결돼!  
해결 안되면 위가 죽고 또 위가 죽고.  

그러므로 fault tolerance 를 기준으로 tree 를 짜야한다.


#### Again, What is object oriented?

* should be completely isolated
* should only communicate via message passing
* should be fault tolerant

Processes are what OO always intended.
