# Cardano

## Philosophy

2015 년에 시작. 암호화폐가 설계되고 개발되는 과정을 바꾸기 위한 노력으로 시작.

전반적인 초점은 통합을 추구하는 다른 시스템뿐 아니라 사용자들의 요구를 더 잘 accounts 하는 좀 더 균형있고 지속가능한 생태계.

많은 오픈소스 프로젝트들의 정신처럼, Cardano 는 포괄적인 로드맵이나 권위있는 백서로부터 출발하지 않았다. 오히려 그것은 설계 원칙 모음, 엔지니어링 모범 사례 및 탐사 방법들을 포함하고 있다.

- accounting 과 computation 을 다른 레이어로 분리
- 고도로 모듈화된 기능 코드로 핵심 요소 구현
- 피어 리뷰 연구와 경쟁하는? 작은 학자 및 개발자 그룹
- InfoSec 전문가의 조기 사용을 포함한 학제간 팀의 heavy 한 사용
- 리뷰 중에 발견된 문제를 해결하는데 필요한 백서, 구현, 새로운 연구 사이의 빠른 반복
- 네트워크를 파괴하지 않고 사후 구축된 시스템을 업그레이드 할 수 있는 능력 구축
- 향후 연구를 위한 분산 자금 조달 메커니즘 개발
- 합리적으로 안전한 사용자 경험을 통해 모바일 장치에서 작동할 수 있도록 암호화폐의 설계를 향상시키는 장기적인 관점
- stakeholders 이해관계자들을 그들의 암호홮폐의 운영과 유지보수에 closer 하게 한다
- 동일한 원장에 있는 여러 자산을 account 해야할 필요성을 acknowledging
- 레거시 시스템의 요구사항을 잘 준수하기 위해 optional 메타데이터를 포함하도록 트랜젝션을 추상화
- 1000 여개의 알트코인으로부터 make sense 한 기능들을 채택하여 배우기
- Internet Engineering Task Force 에서 영감을 얻은 표준 기반 프로세스를 채택, using 최종 프로토콜 설계를 lock down 하기 위한 dedicated foundation 을 이용하여
- 상거래의 사회적 요구 탐구
- Bitcoin 에서 상속받은 몇 가지 핵심 원칙을 손상시키지 않으면서 규제 기관이 상거래와 상호작용할 수 있는 건전한 middle ground 를 찾는다.

이러한 구조화되지 않은 아이디어를 바탕으로, Cardano 에서 동작하는 원칙들은 암호화폐 literature 를 explore 와 추상화 도구 모음을 만들기 시작했다. 이러한 연구의 결과물은 IOHK 의 광범위한 문서 라이브러리, 광범위한 조사 결과(최근 스크립팅 언어에 대한 overview , Ontology of Smart Contract, Scorex 프로젝트 같은)
Lesson 들은 암호화폐 산업의 비정상적이고 때때로 비생산적인 성장에 대한 교훈을 주었다.

## Academic papers

https://iohk.io/research/papers/

엄청 많은 페이퍼들

### Ouroboros: A Provably Secure Proof-of-Stake Blockchain Protocol

Ouroboros: 입증 가능한 안전한 PoS 블록체인 프로토콜

#### Abstract

최초로 엄격한 보안 보증을 받은 PoS.
보상 메커니즘! 정직한 행동이 근사적인 내쉬 균형을 이루므로 selfish mining 같은 공격을 중화한다.

#### Introduction

PoW 에서는 selfish mining 같은 것이 가능하다.
PoS 가 좋은 해결책이 될 것이다.
하지만 아직 여러 해결해야할 문제들이 많다.

##### PoS Design challenge

Stakeholder 들 사이에서 무작위 선거를 달성하기가 어렵다. 이를 위해서는 엔트로피 시스템을 도입해야하는데, 엔트로피를 도입하는 메커니즘은 적의 조작에 취약할 수 있다. 예: PoS 순서를 조작(grinding attacks)

##### Ouroboros

1. PoS 기반 블록체인 프로토콜을 현실화 하는는 문제를 형식화하는 모델을 제공한다. persistence and liveness. peristence: 어떤 한 노드가 어떤 트랜젝션을 stable 하다고 선언하면 다른 노드들이 그것을 확인하고 stable 하다고 인정. k block 이상이면 stable. liveness: once an honestly generated transaction 충분한 시간 동안 네트워크 노드들에서 available 해진 트랜젝션들은 (u time steps) stable. 두개의 conjunction 은 강력한 거래 원장을 제공, 정직하게 생성된 거래가 채택되어 불변된다는 의미에서.

2. Pos 를 기반으로 한 블록체인 프로토콜을 설명. 리더쉽 선거 과정의 무작위성을 만들어내기 위해 coin-flipping protocol 의 매우 간단하고 안전한 멀티파티 구현을 활용한다. 블록체인의 현재 상태를 기반으로 그런 값을 정의하거나 엔트로피를 도입하는 방법으로 collective coin flipping 을 사용하는 사용한 다른 이전 솔루션과 차별되고 grinding attack 을 방지한다.
또 고유한 점은 시스템이 round-to-round 지분 변경을 무시한다는 점. 대신 현재 이해 관계자 집합의 스냅샷을 epoch 라는 일정한 간격마다 가져온다. 각각 그러한 간격에서 브로드캐스트 채널로서 블록 체인 자체를 이용하여 안전한 multiparty computation 이 수행한다. 구체적으로 말하면, 각 epoch 마다 무작위로 선택된 이해 관계자들이 commitee 를 구성하며, 이 commitee 는 동전 뒤집기 프로토콜을 수행할 책임이 있다. 이 프로토콜의 결과는 다음 epoch 에 이 프로토콜을 시행할 다음 이해 관계자들을 결정한다.

3. 누구도 persistence 와 liveness 를 깰 수 없다. 이 프로토콜은 여러가지 가정하에 보장된다.

- 1) 네트워크는 정직한 이해 관계자가 다른 이해 관계자와 의사 소통 할 수 있는 상한선을 결정할 수 있다는 의미에서 동기식이다.
- 2) 정당한 다수로부터 끌어 낸 많은 이해 관계자들이 필요에 따라 각 epoch 에 참여할 수 있다.
- 3) 이해 관계자가 오랜 시간 동안 오프라인 상태가 되지 않는다.
- 4) the adaptivity of corruptions 는 라운드 마다 측정되는 측정되는 security parameter 에 linear 한 작은 지연에 영향을 받는다. (또는 플레이어가 발신자 - 익명의 브로드 캐스트 채널에 액세스 할 수 있음)

우리의 보안 논쟁의 핵심은 우리가 공식화하고 증명하며 또한 실험적으로 검증하는 "forkable strings"의 결합 개념에 관한 확률 론적 주장이다. 우리의 분석에서 우리는 비밀 공격 (covert attacks), 일반 포크 공격의 특수 클래스를 구별합니다. 여기에있는 "은밀함"은 은밀한 적의 정신으로 해석됩니다.
공격자가 프로토콜을 깨기를 원하지만이를 포착하지 않기를 원하는 보안 다중 파티 계산 프로토콜에 대해. 우리는 비밀리에 포크 가능 문자열이 밀도가 훨씬 적은 포크 가능 문자열의 하위 클래스임을 보여줍니다. 이를 통해 우리는 효율성과 보안 성 측면에서 서로 다른 절충점을 달성하는 두 가지 뚜렷한 보안 주장을 제시 할 수 있습니다.
우리의 forkable 문자열 분석은 PoS 설정의 보안 인수의 일부로 적용 할 수있는 자연스럽고 일반적인 도구입니다.

4. 우리는 프로토콜의 인센티브 구조에주의를 돌린다. 우리는 (대략적인) 내쉬 평형을 증명하는 참가자들에게 시스템에 인센티브를주기위한 새로운 보상 메커니즘을 제시한다. 이런 방식으로, 블록 원천 징수 및 이기적 채광과 같은 공격은 우리의 설계로 완화됩니다. 보상 메커니즘의 핵심 아이디어는 프로토콜과 다른 당사자 연합에 의해 억압 될 수없는 프로토콜 작업에 대해 긍정적 인 보수를 제공하는 것입니다. 이런 식으로, 프로토콜 실행 비용이 적다는 전제하에, 프로토콜을 충실히 따르는 것이 모든 플레이어가 합리적 일 때 균형이라는 것을 보여줄 수 있습니다.

5. 블록 체인 프로토콜에 원활하게 추가 할 수있는 스테이크 위임 메커니즘을 소개합니다. 위임은 이해 관계자 집합이 매우 분열되어있는 상황에서도 프로토콜을 확장 할 수 있기를 원할 때 특히 유용합니다. 이러한 경우 위임 메커니즘을 통해 이해 관계자는 자신의 "투표권", 즉 권한을 위임 할 수 있습니다.

#### 참조

#### Selfish Mining

다른 네트워크들에게 유효한 솔루션을 배포하지 않는 것. 자신의 리드를 지키면서 계속해서 다음 블록을 발견해나간다. 나머지 네트워크가 selfish miner 를 거의 따라 잡았을 때, 적당한 양의 미리 해결해둔 블록들을 네트워크에 배포한다.

이를 해결하기 위해 나온 BIP(Bitcoin Improvement Proposal)들
- fork 가 일어났을 때 채굴자들을 여러 브랜치들에 랜덤하게 assign 한다
- mining pool 이 도달할 수 있는 임계값 한계를 제공한다.
- 배포 timestamp 와 블록 timestamp 비교를 통해 차이가 많이 난다면 차별한다.

25% 이상이면 가능하다고 알려져있다.

https://bitcoinmagazine.com/articles/selfish-mining-a-25-attack-against-the-bitcoin-network-1383578440/

#### Griding attack

다음 블록이 이전 블록의 요소에 depends 할 때, 블록을 생성하며 다음 블록 리더가 자신이 될 확률을 높히는 것.

솔루션
- randomness 를 만드는데 쓰이는 정보를 쉽게 사용하지 못하도록 함
- validator 들이 공동으로 임의 값을 생성하도록 함.

https://github.com/ethereum/wiki/wiki/Proof-of-Stake-FAQ

#### Persistence/Liveness

- Persistence: parameter k. If an honest party reports a transaction tx k blocks deep, then tx will be always reported, in the same position and equal or more depth by all honest parties.
- Liveness: parameters u, k. If all honest parties attempt to insert the transaction tx in the ledger, then after u rounds, an honest party will report.

### Ouroboros 간단한 버전

ouruboros 알고리즘은 ada 를 지지하는 인프라스트럭처의 중요한 파트. energy-hungry 한 pow 를 종말시키켜 블록체인이 더 넓게 쓰일 수 있도록 scaling up 하는데 도움이 된다. 안전함이 수학적으로 증명가능한 pos 프로토콜, Crypto 2017 에서 peer review 를 받았다.

PoW 에서 채굴자들이 다음 블록을 만들고 리워드를 받는 리더가 되기 위해 컴퓨팅 파워를 투입했다면, PoS 에서 이해관계자들은 블록체인 원장에 따라 자신이 가진 지분의 크기에 비례해 다음 블록을 누가 만들지 선택된다.

블록체인이 안전하다는 것은 다음 블록을 만드는 이해관계자를 정하는 것이 완전히 랜덤이라는 뜻이다. Ouruboros 가 랜덤성을 만들어내는 혁신은 multiparty implementation of a coin-flipping protocol 에서 온다.

게임이론, 내쉬 균형이 중요 포인트.

### IOHK presents at Oxford University: Ouroboros: A provably Secure Proof-of-State Blockchain Protocol

비트코인은 robust transaction ledger = persistence / liveness 를 위한 것인데 이게 가장 베스트 솔루션인가? 사용할 수 있는 다른 assumption & hypotheses (가정)은 없는가?

비트코인은 느리다
비트코인은 에너지를 너무 많이 쓴다

Robust transaction ledger
What are the alternative ways to meet the main objectives?

persistence: once a tx is confirmed by a node, any pother node that reports it will agree with its placement in the ledger. 일단 한 번 confirm 되면 거부당하지 않는다.
liveness: broadcasting a tx to the network will result to it being confirmed by the nodes. tx 가 네트워크에 퍼지면 다른 노드들에 의해 confirm 될 것이다.
이 두가지에 중점을 둔다.

가정
1. 블록체인 네트워크는 매우 동기적이다.
2. 대부분의 선택된 이해관계자는 필요할 때마다 각 epoch 에 필요한 컴퓨팅 성능에 기여할 수 있다. 이해 관계자는 상대적으로 오랜 기간 동안 오프라인 상태가 되지 않는다.
3. 프로토콜 보안 논쟁의 핵심에는 실험적으로 공식화되고 입증된 "forkable string"이라는 결합 개념을 나타내는 확률론적 주장이 있다.

인센티브를 통해 근사 Nash 평형을 나타냄이 입증됨.


## 생각

PoS 는 서로 같은 비율로 지분이 늘어난다고는 하지만, 참여하기 위한 최소조건이 쉽지 않은 관계로 결국 몇몇 대주주만 계속 지분을 늘려나가게 되지 않을까.







