# Dao. Casino

도박 산업의 문제점 해결. 특히 이용자 입장에서.


## 구성원

일반 도박 구성원에는 없는 새로운 구성원:

- Random Number Providers
- Bankroll Backers(재정 후원자)

### Game Developer

Dao. Casino 플랫폼 내에서 게임 제작. 보상 지급이 보장됨.

### Platform Operator

게임이 실행될 수 있는 플랫폼을 운영하는 사람. 게임 결과로 분배할 보상의 양을 결정할 수 있음.

### Referrer

새로운 플레이어를 데려오는 사람.

### Random Number Provider

난수 제공 자체를 다른 사람에게 맡겨서 신뢰성을 높힘. Smart Contract 안에 Token 보증금을 넣어서 악의적 난수 생성이 들키면 Token 반환.

### Bankroll Backers

Token 제공

### Player

Bankroll Backers 로 부터 Token 을 받거나, Referrers 가 Player 가 되거나, Crowd Funding 형태로 Token 을 받거나.

### Autonomous Agents = Smart Contract

Token 관리. 다수의 합의에 의해서는 계약의 변경이 가능.


## Token

1. ERC20 으로 제작
2. 기존 명성 시스템보다 우수한 보상 시스템(Smart Contract 기반)
3. 해커들에게 공격 받으면 토큰이 무가치해진다..?

## Random Number Generating

Pseudo Random Number Generator(PRNG)

난수를 흉내내는 알고리즘. 주기성 있음. Dao. Casino 플랫폼 내에서 잘 처리해서 예측하기 어렵게 함.

cf) Centralized Casino 에서의 난수 확보 방법: 신뢰할 수 있는 제 3의 기관에서 난수를 얻어옴. 악의, 해킹 위험성.

임의의 숫자는 누구든 예측할 수 없어야 함.

Signidice 알고리즘

게임에 참여한 사람만 영향을 줄 수 있음.
참여자 수가 정해진 게임에 우용함.

## Conclusion

1. 시스템을 구성하는 모든 구성원에게 인센티브가 존재해야 한다.
2. 더욱 신뢰할 수 있는 PRNG 알고리즘을 개발해야 한다.
3. 개발자가 Solidity 언어를 몰라도 게임을 만들 수 있어야 한다.
4. 플랫폼 운영자가 블록체인 기반의 심층적인 지식이 없어도 게임의 설정을 만들고 운영할 수 있어야 한다.


## 질문?!

악의적 난수 생성을 어떻게 확인할 수 있지?
악의적 난수 생성했을 때 손해 볼만큼이라면 얼마나 토큰을 넣어야 하지?


# FunFair

## 특징

기존 블록체인 기반 게임의 문제점: transaction 속도로 인한 느린 게임 속도, 상대적으로 높은 gas fee

우리는!:

- Fate Channel 을 이용해서 해결하겠다!
- Civic 을 이용해서 가입을 쉽게 하겠다
- 바이럴 관련 서비스 지원

### State Channel

두 address 사이에 왔다갔다 하는걸 한 번에 처리할 수 없을까?

=> Off chain 사이에서의 private 한 거래를 요약해서 confirm

### Fate Channel

둘이 합의되지 않았을 때 State Channel 은 불가능.

예시

8번의 게임 중 2번의 transaction

1. Random number generation + 배팅금과 게임에 대한 smart contract
2. 총 게임 결과

#### 블록체인 상의 여러 난수 생성의 문제점

- 각 트랜잭션마다 난수 생성이 필요.
- Oracle: 블록체인 컨펌, 시간 문제 발생.
- block hash: block hash 값을 seed 로 생성한 후 salted(양념): 블록 생성자가 게임에 들어와서 패배하면 블록 폭파?..

#### 특징

- 공정성: 복잡도가 높은 데이터를 RNG 소스로 사용 + Smart Contract 에 의해 게임 규칙 인코딩
- Reverse Hash Chain: hash 값 대조를 통한 검증으로 조작을 방지함. 여러개의 hash 를 생성하고 게임이 진행될 때마다 앞의 hash 를 seed 로 사용하여 게임 진행. 마지막에 channel 에 올릴 때 게임 마지막에 사용된 hash 와 끝 hash 를 이용해 게임을 검증. Fate channel 을 위한 것.
- Off chanel


## 질문?

라이센스 구매가 쉽다면 라이센스의 의미는 무엇인가?
=> 실제 라이센스 지원.
