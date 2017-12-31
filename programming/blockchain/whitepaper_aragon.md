# Aragon

A decentralized infrastucture for **value exchange**

## Abstraction

Aragon 네트워크는 토큰에 의해 통치되는 디지털 관활권 that 글로벌 비차별적인 경제 발전을 위한 베스트 컨디션에 집중한. Aragon 은 ecosystem 이다 조직, 사업가, 투자자들이 효율적이고 보안적으로 안전하게 거래하는 기술적 버그나 악의적 파티에 의한 리스크 없이.

Aragon Network organizations 는 Solidity DAO(decentralized autonomous organization) 프레임워크와 web-based dApp 인 Aragon Core 로 만들어진다. Aragon Core 는 capitalist companies 에 특화되어 있었으나, 다른 타입의 조직에서도 사용하기 좋도록 충분히 모듈화 되어 있다.

이 페이퍼는 먼저 Aragon Core 의 조직과 기능의 원리에 대해 설명한다. 다음으로 Aragon Network 의 token 모델과 network governance 를 설명한다. 마지막으로 Aragon Network 가 성공하기 위해 반드시 구현되어야 할 두가지 중심 서비스, decentralized court solution 과 upgrade mechanism 을 정의한다. decentralized court solution 은 논리적으로 스마트 컨트랙트에 적힐 수 있는 human conflict 중재를 위해 제공된다. Aragon Core organizations 의 upgrade mechanism 은 non-technical 의 주류 채택을 촉진하는 데 필요한 유용한 업그레이드를 용이하게한다.

Aragon 프로젝트는 지난 수십 년 동안 수천 명의 개인에 의해 이루어진 진전을 토대로 제작되었다. 그 중 Aragon 에 큰 영감을 준 몇몇 사람들을 highlight 하고자 한다.

blabla


## 1. Introduction

### 1.1. About Aragon Core

Aragon 은 누구나 어떤 종류의 조직(회사, 오픈소스 프로젝트, NGO, foundations?, 헷지 펀드) 이든 관리할 수 있게 해주는 이더리움 브록체인 상의 dApp 이다.

Aragon 은 조직의 기본 feature 인 cap table, token transfers, voting, role assignments, fundraising, accounting 등을 구현하였다. Aragon 조직의 행동은 bylaws 의 변경을 통해 쉽게 customizing 할 수 있다. Aragon 조직은 조직의 계약들과 interact 하는 third party 모듈들을 통해 확장 가능하다.

### 1.2. Current limitations

이더리움 블록체인의 properties 는 기록의 immutability, transparency, fast transaction 을 포함한. 탈중앙화된 조직의 설립과 관리 unique 한 기회를 보여준다. 하지만 사람들이 transact, 밸류를 만들어내기 위해 필요로 하는 여러 요구사항을 만족 시키기 위해, 이것의 가장 윗 레이어는 이 시스템에 참여한는 모두에 대한 incentive 를 align 하기 위해 만들어져야 한다.

Aragon Core를 설계 할 때 대부분의 사람들이 분산 된 조직을 만들고 실행하며 상호 작용하는 것을 막을 수있는 여러 문제가 다뤄졌다.

- Subjective beaches(주관적인 위반): 스마트 컨트랙은 거의 모든 가능은 계약 위반을 인코딩할 수 있지만, 이것은 인간 관계 속에서 늘 주관적이었다. 갈등이 스마트 컨트랙트 코드로 명시적으로 해결되지 않는 케이스들을 위해 선입견 없는 (unbiased) 중재 (arbitraion) 시스템이 필요하다.

- Software bugs: 의자와 키보드 사이에는 항상 에러가 존재한다. 코드는 버그를 가지고 있을 수 있기 때문에 소프트웨어는 쉽게 업그레이드 가능해야 하고, 잠재적 공격자가 공격을 하는 대신에 보상을 요구할 수 있도록 믿을 만한 버그 보상 메커니즘이 존재해야 한다.

- Reward systems: 특정 프로토콜 및 시스템에 대한 수익 창출은 이 시점에서 명확하지 않다. 일부 플레이어는 조직을 구성하는 데 핵심이되므로 간단한 보상 메커니즘이 필요하다.


## 2. Aragon Core organization

## 2.1. Organization specs

조직은 여러가지 요구사항이 있는데, 주요 사항들은 아래와 같다.

- Identity: 우리는 그들과 운영하기 전 각 entity 들의 identity 를 세워야 하기 때문에 이것은 가장 첫 기둥이다.
- Ownership: 주식은 설립자, 투자자, 고문, 파트너, 직원들에게 리워드를 줄 수 있는 방법이고, 오너쉽과 회사의 방향을 결정할 수 있다.
- Voting: 회사의 주주들은 회사의 액션에 대해 의견을 제시할 수 있어야 한다. 이것은 오너쉽과 직접 연결된다.
- Capital: 벤처는 위험성이 있고 운영이나 성장을 위해 어떤 goods 들을 습득해야 하기 때문에 투자나 대출의 형태로 자본이 필요하다.
- People: 결국 조직을 만드는 것은 사람이다. 그들을 쉽게 온보딩 (identity) 하고 리워드 (payroll) 할 수 있는 방법이 필요하다.
- Outreach: 회사는 청중들이 회사의 프로덕트를 사도록 타겟팅 해야한다. 인터넷 시대에는 도메인을 가지는 것만으로도 충분했다.
- Payment processor: 조직은 지불 받을 수 있어야 한다. 쉽게 결제를 capture? 할 수 있는 방법이 그들에게 필요하다.
- Accounting: 지출, 화상?(burn) 비율, 사업 결정을 결정하기 위해 그들은 book-keeping 을 관리할 필요가 있다.
- Insurance: 회사는 주로 risky 해서 뭔가 잘못될 때를 대비해 보험을 살 필요가 있다.

이 중 몇몇은 다음과 같은 dependency graph 를 만든다. 결국 순환으로 끝나는.

- Identity: No dependencies
- Ownership: Depends on Identity 자신이 옳바른 entity 와 interacting 하고 있는지 확인하기 위해
- Voting: Depends on ownership, ownership 이란 control 을 의마히기 때문에
- Captial: Depends on voting, 주식 발행을 의미하기 때문에
- People: Depends on capital, 사람을 뽑기 위해 필요하기 때문에

## 2.2. Implementation

### A. dApp runner

이더리움 개발 플랫폼의 주요 장점은 dApp 을 돌릴 수 있는 여러가지 방법이다. Aragon 의 기본 dApp runner 을 고려할 때, 우리는 여러가지 옵션들의 장단점을 비교했다.

| Runner | Description | Pros | Cons |
|---|---|---|---|
| MetaMask | 구글 크롬 브라우저에서 이더리움을 가능하게 하는 플러그인. 유저는 사인되지 않는 트랜젝션을 확인하거나 거부할 수 있다. | 적은 마찰, 설치하기 쉬움 | 아직 베타, 크롬에서만 가능, 풀노드가 아니여서 그들의 블록체인을 믿어야함 |
| Mist | dApp 과 interaction 하기 전에 사용자에게 허가를 받는 dApp 브라우저 | 풀 이더리움 노드, 이더리움 공식 dApp 브라우저, 하드웨어 지갑 호환 | 동기화 하는데 오래 걸림, 큰 마찰 (설치하고 dApp 을 이용하는데 1시간 이상 걸림) |
| Parity | 폴노드 dApp 브라우저 크롬 익스텐션 | 풀노드, 하드웨어 지갑 호환 | 높은 마찰 (얘도 1시간) |
| Native Aragon app | 주요 데스크탑 플랫폼에서 돌아가는 Elentron 으로 만들어진 native app | 모든 UX 를 컨트롤 가능: 이더리움이 처음인 사용자들도 사용하도록 할 수 있다 | 엄청난 요구사항, 앱을 다운 받도록 해야하는 마찰 |

Aragon Core 가 지금은 위의 모든 구성을 순수한 dApp 으로 실행하지만, 궁극적으로는 직관적인 설치와 친숙한 유저 인터페이스를 위해 Electron wrapper 로 native Aragon app 을 구현했고, 이 안에 최고의 유저 경험 콘트롤을 제공하는 MetaMask 를 주입했다.

우리는 이것을 기본 Aragon 경험으로 밀고나갈 것이고, 우리는 이것이 이더리움에 대해 들어본 적이 없는 사람들이 이것을 처음 접하고 Aragon Core 조직을 15분 내에 관리하기 시작하려는데 친숙할 것이라고 생각한다.

### B. Identity

새로운 토큰을 발행하거나 직원에게 paying 할 때, 조직은 올바른 사람에게 asset 이 보내졌는지 알 수 있어야 한다. 이 요구사항을 해결하기 위해 우리는 cryptographic entities 에 identity 를 부여할 수 있는 Keybase 를 통합했다. 우리는 현재 uPort 를 비롯한 다른 identity provider 를 Aragon 에 통합하기 위해 조사하고 있다. 우리는 Aragon blog 에 identity 관리에 대한 우리의 생각을 올렸다.

### C. Permissions

Identity 는 우리에게 permission 을 제공한다. 아래와 같은 permission 예가 있을 수 있다.

- Shareholder: 배당금을 받을 권리를 가지며, 나갈 때 voting power 에 의해 정해진 threshold 를 벗어나지 않는 선에서 share 를 다른 party 에게 양도한다.
- Exsecutive: 더 많은 permission 을 가지고 투표를 통한 승인 없이도 몇몇 task 를 수행할 수 있다.

하지만 탈중앙화된 trustless 조직은 조직의 서로 다른 개개인들에게 좀 더 유연한 관계를 허가해줄 수 있다. Aragon 조직은 fine-grain customization 을 승인하는 into 액션을 취할 수 있는 사람 (간부는 직원을 payroll 에 추가할 수 있다) 또는 액션이 허가되기 전에 일어나야 하는 일 (토큰 발행을 승인하기 위한 투표가 필요하다) 커스텀 가능한 조례들을 가지고 있다.

### D. Reputation

명성은 free market 에서 굉장히 중요한 가치이다. 우리는 원하는한 모든 interaction 이 평가되길 원한다.
예를 들어, 이것은 조직이 contractor 의 일을 평가하고 contractor 가 회사를 평가할 수 있게 한다.
우리는 모든 관계 감사 기록을 가지고 있기 때문에, 우리는 review 가 실제로 진짜이도록 쉽게 interaction 을 추적할 수 있다. 이것은 원한다면 완전 익명으로 처리된다.

### E. Onboarding

app 이 열리면, 이더리움 계정을 만들고 안전하게 백업할 수 있어야 한다.
그 후에
- interact 하고 싶은 회사의 주소를 넣거나
- 새 회사 contract 를 deploy 한다. 이 경우 dApp 은 자동으로 그 contract 를 contract 의 주소로 연결한다.
onboarding 프로세스는 암호화화폐에 빠진 사람이 아니더라도 누구에게나 친숙해야 한다. 그것이 이것이 이렇게 쉬워야만 하는 이유다.

### F. Ownership

Aragon Core 조직의 ownership 은 투명하고 이동 가능하다. 각 stakeholder 들의 홀딩은 공개적이고 stakeholder 는 ownership 을 다른 party 에게 건낼 권리를 갖는다. Aragon Core 에는 ownership 의 4가지 투명한 기능들이 있다.

- 모든 stakeholder 들과 그들의 holdings 에 대한 리스트
- 임의로 혹은 파라메터를 가지고 share 발행
- 토큰을 팔거나 전송
- 새 토큰을 발행

조직은 Vesting Calendar 또는 다른 기준에 따라 양도가 제한된 토큰을 발행할 수 있다.

발행되는 모든 토큰이 ERC20 토큰 기준에 부합한다. 이것은 stakeholder 들의 주소가 이름, 태그와 연결되거나 안전한 identity provider 로부터 가져와질 수 있다는 것을 의미한다.

### G. Capital

스타트업 조직은 빠르게 자본을 raise 할 수 있어야 한다. 전통적인 스타트업들에서는 VC 유니콘 롤러코스터를 타거나, third party (eg. Kickstarter) 를 통해 크라우드 펀딩을 받거나, 비지니스 대출을 받거나, 친구나 지인들로부터 받거나 투자에 대한 연결을 말한다. Aragon Core 조직은 자본과 교환하기 위한 새 share 를 third party 없이 직접 판매 혹은 공모를 통해 쉽게 발행할 수 있다.

- Aragon Core 조직은 적절한 양의 currency 를 보낸 다른 party 에게 직접 share 를 발행할 수 있다.
- 조직이 자본을 공개적으로 raise 하고자 한다면, Aragon Core 조직은 marketplace 에 share 공모를 할 수 있다. 투자자들은 직접 협상을 위해 contact 하거나 한정된 수의 share 에 투자할 수 있다.

### H. Rewards

직원을 고용하고 지불하는 것은 불필요하게 복잡하다. Aragon Core 는 이 과정을 단순화한다. Aragon Core 조직은 사람들을 payroll 에 추가하고 시간 and/or task 기반 퍼포먼스를 포함하는 특정 parameter 에 따라 그들에게 토큰을 발행할 수 있다.

유저 인터페이스는 유저가 amount to pay, requency, shares to reward, parameter 를 정할 수 있게 한다. 이 과정을 더욱 효율적으로 만들기 위해 리워드는 어떤 이더리움 기반 토큰 (0x 프로토콜로 powered 된 것 같은 탈중앙화 교환을 통해) 으로도 가능고 또는 Cosmos 나 Polkadot 같이 inter-blockchain currency exchange 를 가능하게 하는 솔루션이 가능한 어떤 암호화화폐로도 가능하다.

명목화폐가 선호된다면, 회사 자금으로부터 명목화폐로 채워진 신용카드를 생성할 수 있는 옵션도 있다. 즉석, 익명 VISA 카드를 만들 수 있는 API 를 제공하는 Shake 같은 솔루션은 Aragon Core 에 직접 통합될 수 있다.

### I. Payment processor

들어오는 지불의 경우 고객이 ShapeShift 와 같은 서비스를 사용하여 기업간의 통화 선택으로 변환할 수 있는 암호화화폐를 살 수 있다.
사용자가 그 암호화화폐를 얻은 다음 결제를 계속 진행한다.
하지만 그들에게 이것은 single step 일 것이고 모든 것은 background 에서 투명하게 진행될 것이다.
우리는 이것이 유저가 지갑을 바로 만드는 대신 처음에 가장 일반적으로 사용할 흐름이라고 예상한다.

우리는 Stripe 같이 smooth 한 사용자 경험을 위해 암호화화폐 교환과 providers 를 통합할 것이다.

### J. Accounting

회계기능은 완벽하게 구축되어 있으며, 필요없는 삽질을 하지 않기 위해 우리는 third party 시각화 서비스에 대한 연결을 제공할 것이다.

## 2.3. Modular Software

Aragon Core 는 이더리움 네트워크에서 조직의 최소 principle (앞에서 본) 을 가진 조직을 운영하하는데 필요한 모든 요소이다. 하지만 조직들은 out-of-the-box Aragon Core 소프트웨어에서 사용할 수 없는 고유의 요구사항을 가지고 있다. 이 이슈를 해겨하기 위해 우리는 Aragon Core 모듈러 시스템으로 구축해서 위에 추가 기능을 개발할 수 있도록 했다.

또한 우리는 Aragon Core 를 이용하는 개발자들이 조직을 생성하거나 운영하는 것과는 관계 없는 use case 를 만들어 줄 것으로 기대하고 있습니다. 우리가 상상하는 Aragon Core 를 이요한 가능한 use case 는 아래를 포함한다:

- Political election voting module: 소규모 예측 시장은 선출직 공무원이 공약을 지키고 그들에게 투표한 사람들에게 보상을 제대로 하는지 확인할 수 있다.
- Contractor payment module: 당신의 프로젝트를 위해 일하거나 어떤 마일스톤을 달성했을 때 contractor 에게 지불하기
- Accounting module: advanced 데이터 시각화 (Aragon Core 에서 제공되는 것이 아닌) 을 이용한 회계 모듈

중요하게도, 모든 모듈은 스탠다드 웹 기술로 코딩될 수 있다. 이를 통해 개발자들은 강력한 샌드박스와 보안을 유지하면서 그들이 원하는대로 사용할 수 있다.

## 2.4. Aragon Core summary

Aracon Core 는 조직의 행동을 위한 커스텀 로직이 있는 곳이다. 정리하자면, Aragon Core 어플리케이션 레이어의 주요 컴포넌트들은:
- 유저의 permission 을 결정하는 bylaws. 예) 누가 액션을 취할 수 있는가
- 결정을 내리기 위한 관리 시스템
- 토큰을 발급하고 컨트롤 하기 위한 capital 시스템
- 펀드 매니징을 위한 회계 시스템

각 컴포넌트들은 효율적이고 공정한 조직의 원칙을 분산된 방식으로 충족시키기 위해 함께 작동한다. 또한 시스템의 모듈적인 특성으로 인해 Aragon Core 조직은 그들의 unique 한 요구에 맞게 소프트웨어를 커스텀하거나, Aragon Core 를 다른 용도에 (political election 을 위한 투표) 맞도록 개조할 수 있다. Aragon Core 는 Module System 을 구현해서 더 많은 기능을 구현할 수 있다.


* 여기 organ 을 조직이라고 번역했는데 다시 봐야할듯
# 3. DAO architecture: Kenel, Organs and Application

이하 세션은 Decentrailized Autonomous Organization 의 최소 정의, Aragon Core 와 Aragon Network 가 adopt 한 DAO 의 principles, DAO Kernel 의 구조와 기능에 대해 다룬다.

## 3.1. The minimum definition of a DAO

우리는 DAO 가 최소한의 표현으로 정의되어야 한다고 빋는다. 이것은 영원히 identity 를 잃지 않고 자신을 성공적으로 업데이트 할 수 있는 능력을 소유한 조직으로 정의된다.

## 3.2. Principles of the DAO

Before defining the different components this kernel for the DAO has, 우리가 성취하기 원하는 DAO 의 기본 원리에 대해 정의해보자.

- She is. 우리는 영원한 존재를 세계에 존재하는 entity 로 인식해야한다.
  - DAO 는 자기 자신이 존재하기를 중단하기 전까지 존재할 것이다. 그 시점에서 그것은 영원히 사라질 것이다.
  - DAO 는 같은 entity 로 계속해서 인식 되면서 스스로의 기본 컴포넌트들을 스스로 업데이트 할 수 있다.
- She owns. DAO 는 내부 자본을 보유하므로 주로 디지털 자산 형태로 자산을 보유한다. (암호화화폐, 토큰, 도메인이나 IP 같은 디지털 property)
- She acts. DAO 는 바깥 세상이나 자신을 향해 행동을 취할 수 있다. DAO 의 소프트웨어는 스마트 계약 형태로 컴퓨터 코드르 실행한다.
- She is governed. 미리 프로그래밍된 액션 외에도, 외부의 사람이나 기계의 액션도 DAO 액션을 트리거 할 수 있다.

## 3.3. Kernel Functions

kernel 의 핵심 기능은 조직 및 각자의 우선 순위 수준을 정의하는 레지스트리 역할을 하는 것이다. 각 조직에는 고유한 우선순위가 있다는 점에 유의해야 한다. 그러므로 새로운 조직이 이미 존재하는 우선 순위 레벨로 설정되면 원래의 조직이 대체된다.

kernel 은 다른 타입의 entry point 트랜잭션을 수락할 책임이 있으며 표준 API를 사용해서 조직에 그것을 보낸다. 현재 kernel 에서 support 되는 entry point 들은
- Standard transfer, value transfer in ether: 자신에게 붙어있는 가치를 가지고 있는 순수한 이더리움 트랜젝션
- Pre-authorized transfers, value transfer in ether: kernel 은 특정 발신자에 의해 이전에 서명된 DAO 호출을 지원한다. 

... 나중에 보자


# 4. The Aragon Network

Aragon Network(AN) 은 조직과 사업가와 투자자가 운영을 매우 쉽고 친숙하게 할 수 있도록 하는 digital jurisdiction(관활권?) 을 목표로하는 최초의 DAO 가 될 것이다.

AN는 covernance 에 의해 투표된 굉장히 얇은 헌법을 기반으로 부트스트랩 될 것이다. AN 의 거버넌스 에 의해 새 법이 추가되거나 개정될 수 있다.

또한 core AN contract 의 굉장히 중요한 역할은 네트워크 내의 조직 구성원들을 확보하고 그들이 정해진 규칙을 따르고 있는지 확인하는 것이다.

네트워크는 네트워크 상에서 거래하는 조직의 운영에 대한 수수료 형태로 자본을 축적함으로써 운영될 것이다. 이 수수료는 네트워크 내부 자본에 기여하여 네트워크 거버넌스가 자유롭게 할당할 것이다. 이 기금의 최종 목적지는 아마 네트워크 운영에 필수적인 네트워크 서비스 제공자일 것이다.

이 메인 서비스들은
- 탈중앙화된 조직을 운영하도록 해주는 Aragon Core contracts 의 개발
- 조직을 동결시킬 수 있는 탈중앙화된 법원 (Appendix A)
- 내장된 버그 보상 메카니즘 있는, 모든 Aragon Core contracts 를 위한 contract 업그레이드 서비스

우리는 AN 이 조직이 번창하기 위해 필요로 하는 모든 것을 제공한다고 말할 수 있다. 현실 세계의 메타포를 찾아보자면, 델라웨어가 현재 회사와 투자자들 사업가들에게 어떤 곳인가가 있다.


# 5. The Aragon Network Token, ANT

거시 경제의 방식에서 통화가 부를 나타내는 것 처럼, 탈중앙화된 Aragon-enabled 경제에서는 ANT 가 부를 나타낸다.

## 5.1. Network Kickoff and ANT Issuance

네트워크를 시동걸려면 제한되지 않은 수의 ANT 가 시간이 흐름에 따라 가격이 증가하는 미리 결정된 함수에 따라 판매된다. 초기 판매로 raised 된 fund 는 Aragon Core 와 Aragon Network 개발하기 위한 자금으로 Aragon Foundation 에 이전된다.

이 판매가 끝나고 조금 지나면, AN 이 AN 의 명시된 미션을 수행하고 하기에 안전하다고 생각되면 Community 멤버 multisig 가 Aragon Network 를 deploy 한다. 이 때 네트워크는 initiate 하고 ANT 토큰 소유자들에 의해 governance decision 이 만들어지기 시작한다.

## 5.2. A Continous Token model

ANT 는 초기 판매와 네트워크 deployment 이후에 네트워크에 의해 계속해서 주조된다. 새로운 토큰을 주조하는 것은 비용이 들고, 조직이 네트워크에 조인하기 위해 지불하는 수수료 비율은 새 토큰 발행에 대한 비용을 지불한다. 이것은 Aragon 조직들이 수수료를 내는데 인센티브를 제공하는데, 기여를 많이한 조직이 더 많은 ANT 를 받게될 것이기 때문이다. 이것은 그 조직이 네트워크 의사결정에 더 많은 영향을 미친다는 의미이다.

새로운 토큰을 주조하는데 드는 비용은 ANT 토큰 소유자에 의해 결정된다. 이것은 아마도 논쟁의 여지가 있는 결정일 것이며, 공급과 수요의 기본적인 경제원칙이 고려되어야 할 것이다. 예를 들어, 토큰 주조 가격이 너무 낮은 경우를 생각해보자. 공급이 수요를 매우 넘어설 때까지 점점 더 많은 토큰이 공급되기 위해 더해질 것이다. 이것은 인플레이션을 일으켜 개별 ANT 의 가치는 떨어질 것이다. 궁극적으로, 우리는 토큰 소유자들이 인플레이션의 건강한 균형을 결정할 것이라고 믿는다. 모든 이해자들의 의견을 수렴함으로써, 시장은 최적의 조폐 비용을 반영할 것이다.

## 5.3. Network Governance

처음에는, Aragon Network 가 liquid democracy (대안들, 예를 들면 futarchy, 또한 고려되고 있고 우리는 능동적으로 그 분야를 following 하고 있다) that 토큰을 발행하고, 기금을 분배하고, 네트워크 룰을 결정하는. figure 5.3 에서 ANT 토큰 소유자들에 의해 결정되는 샘플 결정들을 더 자세하게 보아라.

이것은 의미한데 네트워크가 deploy 될 때 governance 결정이 proposal 과 voting 시스템에 따라 ANT 소유자에 의해 결정될 것이다. 이 메커니즘을 사용하면 메커니즘이 업그레이드 되도록 하는 proposal 을 작성할 수 있다.

## 5.4. Network Adaptablity

Aragon Network 는 탈중앙화된 조직들이 넓게 퍼질 수 있도록 하는 여러 basic 서비스들을 제공할 것이다. 하지만 우리의 의도는 이것이 가능한 글로벌하고 오픈된 상태로 남아있는 것이다.

Aragon Network 는 몇가지 헌법과 governance method 를 가지고 있으면서, 모두가 Aragon Network 안에 좀 더 specific set of laws 를 가지고 다른 네트워크를 만들 수 있을 것이다. 예를 들어, 당신은 조직을 만들고, Aragon Network 에 join 하고, 당신의 조직에 맞는 새로운 set of laws 를 투표할 수 있을 것이다. 효과적으로, 조직들은 Aragon Network의 서비스 기본 구성 및 프레임 워크로서의 서비스를 사용하고, 조직내 relationships 를 관리하기 위한 커스텀 set of rules 를 만들 수 있다.

## 5.5. Further uses of the token

ANT 토큰은 governance 나 다른 기능들을 위해 토큰이 요구되는 모든 네트워크 서비스의 기본 토큰이 된다. 예를 들어 court 의 경우에, 소유자들은 그들의 토큰을 사용하여 중재를 돕고 보상을 받을 수 있다.

## 5.6. Token technical features

ANT 는 몇몇 clone-ability 와 Vesting Calendars 내재화 같은 extra feature들이 올라가 있는 ERC20 호환 이다.


# 6. Summary

AN 는 대규모에서 훨씬 잘 작동하는 서비스를 제공하여 완전히 탈중앙화된 조직을 운영하면서 발생하는 중심 이슈들을 해결해, Aragon 조직들을 더 효율적이게 만든다. 이것은 네트워크가 공공재를 지불 할 수 있는 방법을 제공한다.


# Appendix: Network Services

우리는 Aragon Network 가 고용할 두가지 fundamental 네트워크 서비스를 정의 정의할 것이다. 이들은 Aragon Dev 에 의해 개발되었을 수도 아닐 수도 있다.

다음은 프로토콜 스펙은 아니지만 Aragon Network 가 필요로하는 문제와 기능에 대한 우리의 연구를 간단히 정의한 것이다.

## Appendix A: Decentralized arbitraion system for the Aragon Network

### 1. Driving factors

시장에서 거래를 할 때 신뢰가 깨져서 stakeholder 간에 분쟁이 발생할 수 있다.

스마트 컨트랙트의 trustless 한 특성 덕분에, 문제의 많은 면적들이 사라진다, 조건들이 미리 설정되고 그 후에는 누구도 속일 수 없기 때문에. 하지만 코드로는 표현할 수 없는 조건들이 많이 있으며, 따라서 분쟁이 발생할 수 있다.

아래의 두 가지 예를 생각해보자:
- 한 투자자가 조직에 투자를 하고 약간의 투표 power 를 받았다. 그러자 그 조직의 founder 가 rogue(불량자)가 되어 모든 투자 자금을 그의 개인 계좌로 보낸다. 이것이 만약 Aragon 조직이었다면, 투자자는 일정 thershold 이상의 트랜젝션은 과반수 투표로 승인해야 하도록 해야한다.
- 설립자가 시스템관리자를 SaaS 조직에 고용했다. 그 직원은 그들의 가치있는 유저 데이터베이스에 접근해서 그것을 훔치고 그 자신의 이익을 위해 그것을 사용했다. 이더리움 위에서 돌아가는 코드는 어떤 일이 일어났는지 알 수 있는 방법이 없고, 따라서 Aragon 조직은 이러한 human breach of trust 에 취약하다.

우리는 이러한 종류의 인간 행동을 스스로 꺼리는 참여자를 위한 선택 시스템이 있어야 한다고 믿는다.

이에 대한 전통적인 해결책은 정부가 운영하는 jurisdiction 이다. Aragon 조직은 위치와 정부에 독립적이기 때문에 (그들은 이더리움 네트워크 위에서 운영될 예정이므로) 더 나은 솔루션을 내놓았다.

### 2. A decentralized, luquid, forkable jurisdiction

Aragon Network Jurisdiction (ANJ) 은 set of contracts 를 정의한다:
- 두 parties 사이의 어떤 분쟁에도 중재를 지원한다.
- ANT 소유자들이 중재자가 고려할 특정 기본 규칙들에 대해 투표한다.

#### 2.1. Entities

Entities (조직이나 직원 같은) 은 그들의 contract 에 대한 모든 통제권을 ANJ contract 에 넘김으로써 네트워크에 참여 가능하다.

서로 interact 하는 entities는, 예를 들어 조직과 직원, 어떤 암호화된 방식으로라도 그들이 원하는 관계의 자세한 정보 (이미 어느 계약서에 있는 것보다 더) 를 표시할 수 있다. 예를 들어 공통된 문서에 타임 스탬프를 지정하는 것, 양쪽 parties 에 의해 서명된 것 보다는.

#### 2.2. ANT functionality in the ANJ

- Supreme Court 의 일반 기본 규칙이나 판사 교체와 같은 여러 결정과 purpose 에 대한 Voting power
- 중재를 열어 채권을 만드는 능력

#### 2.3. Judges

중재인이 되기를 원하는 entities 는 판사로 참여하기 위해 채권을 게시할 수 있다.

### 3. Arbitration mechanism

중재를 열기 위해서는, 신청자가 채권을 게시해야 한다. 이 채권은 소송에서 해결 된 경우 다시 돌려받고 그렇지 않은 경우에는 압수 당한다.

중재 청원은 또한 동결될 수 있다. 이것은 피고인의 contract (예: 공격자가 버그를 악용한 경우) 를 즉시 동결시킬 수 있다는 것이다. 피고의 조직 stakeholder들 중에 중 신청인만이 이러한 청원을 할 수 있다.

human verdicts(평결)을 위해 판사의 결정은 .. 나중에

## Appendix B: Aragon Network smart contract security and upgradeability strategy

스마트 컨트랙트에서 매우 좋으면서도 동시에 문제가 되는 부분이 일단 만들어지면 그것들은 블록체인 위에 존재하면서 어떤 코드든 개발자가 작성한대로 실행된다는 것인데, 그것이 항상 계약을 만든 사람의 의도를 재현하지는 않는다.

가장 중요한 예는 DAO 해킹이다. 예기치 못한 액션의 조합으로인해 컨트랙트가 엄청난 양의 돈을 해커에게 보냈다. 이 경우 자금 누출을 막기 위해 프로토콜 수준에서 하드포크가 진행되었다.

Aragon 에서 우리는 DAO 를 만들고 실행하는데 필요한 소프트웨어를 만들고 있지만, 확장 가능하고 쉬운 방법을 통해 이더리움을 들어본적 없는 사람들도 이것을 이용해 그들의 조직을 운영할 수 있다.
우리는 이런 문제에 익숙하지 않은 사람들이 항상 최신버전의 소프트웨어를 실행해서 그들이 항상 공격으로부터 보안적으로 안전함을 확신하면서 조직을 운영할 수 있는 시스템을 만들어야 한다.

이서비스는 Aragon Network 아네 있는 모든 참여 조직에서 사용할 수 있지만, 조직들은 업그레이드에 대한 완전한 콘트롤(내가 허락하지 않으면 내 조직 내 어떤 코드도 변경될 수 없다)부터 전혀 콘트롤 하지 않음(나를 안전하게 지키면서 나는 아무것도 알고 싶지 않다), 중간 지대(일반적으로는 업그레이드 하지 말아라, 하지만 중요한 보안 문제가 있다면 자동으로 업그레이드 하라)까지 의존 정도를 결정할 수 있다.

이것은 아직 작업 진행중이지만 수천개의 안전한 DAO 가 나타나는 것을 보고 싶다면 네트워크에 중요한 추가 사항이다.

### 1. Component

다음은 네트워크와 개발 조직의 무결성을 보장하기 위해 우리가 현재 계획하고 있는 여러 구성요소다.

#### 1.1. Proxy libraries for upgradeable smart contract

현재 중요한 스마트 컨트랙트 시스템을 배포하는 방법은 일반적으로 계약의 건전한 보안 감사 수행, 네트워크에 업로딩에 의존하고 최상의 결과를 기대한다. 코드가 불변의 법이기 때문에, 버그를 수정하거나 프로그래머의 원래 의도를 더 잘 맵핑할 수 있는 업그레이드를 출시할 수 없다.

또는 스마트 컨트랙을 작성한 프로그래머가 잘못한 것 말고도, 프로토콜의 합의 알고리즘이 변경되고 계약이 새로운 공격 경로에 취약해질 수도 있다.

이것은 시스템이 업그레이드 가능하지 않을 때의 문제이며, 오늘 작성된 계약서는 앞으로 영원히 좋을 것이라고 생각한다. 이것은 간단한 서비스의 경우에는 맞을 수 있지만, Aragon 같이 DAO 나 복잡한 네트워크에서는 아닐 수 있다.

우리는 이 문제를 해결하기 위해 몇 달동안 연구를 했고, 우리의 현재 솔루션은 시스템 비지니스 로직을 Solidity libraries 안에 최대한 캡슐화하기위해 시도하는 것이다. Library Driven Development 를 하고, 비지니스 로직을 컨트렉트에 영원히 연결하는 것 대신에 각 조직이 연결된 라이브러리의 버전을 알고있는 Proxy Dispatcher 컨트렉트를 가지는 것이다. 우리는 이렇게 업그레이드 된 라이브러리의 버전을 dispatch 하는 system of proxies 를 만들기 위해 최고의 스마트 컨트렉트 보안 회사인 Zeppline 와 일하고 있으며, 우리는 최근 이것에 대해 퍼블리쉬 했다.

이러한 기술들은 스토리지가 있는 매우 얇은 조직 계약을 가능하게 하고, 모든 조직에서 사용하는 라이브러리의 모든 로직을 redirect? 할 수 있도록 한다.

버그가 발견된 경우, 새 버전의 라이브러리가 배포되고 네트워크의 모든 조직들은 그들의 설정에 따라 업그레이드 된다:
- 자동 업그레이드
- 업그레이드 하도록 알림을 받지만 승인을 필요로함
- 아무것도 하지 않음. 조직은 업그레이드를 하지 않도록 결정하고 스스로 그 문제를 다루도록 함.

#### 1.2. Network wide bug bounties

여러 조직에 의해 실행되는 같은 계약의 부작용은 이것이 해킹의 대상이 될 수 있다는 것이다. 보다 긍정적인 점은, 해킹이 발생하지 않도록 자원을 할당하기 위해 인센티브된 stakeholder 들이 있다는 것이다.

네트워크는 조직이 rely on 하고 있는 모든 계약과 네트워크 컨트렉트에 대한 버그 보상 프로그램을 만들 것이다. 사람들이 좋은 것을 하도록 경제적으로 인센티브되면, 버그를 찾은 대부분의 사람들은 더 많은 사람을 고통스럽게 할 방법을 찾기 보다는 이것을 프로그램에 리포트하고 보상을 받으려 할 것임을 역사가 보여준다.

체인의 조직 계약을 위한 test suite 를 통해 버그 보상을 꽤 자동으로 만드는 아이디어들을 경험하고 있으며, 만약 누군가가 이 테스트를 깨트릴 수 있다면 심각도에 따라 자동으로 지불한다.

네트워크의 업그레이드 메커니즘은 버그 보상 프로그램과 잘 맞는다, 취약점이 발견되었을 때 업그레이드 트랙에서 모든 사람이 해결될 때까지의 시간이 최소화 되기 때문이다.

#### 1.3. Global safe stop

중대한 버그나 공격이 감지되면, Aragon Network 는 모든 조직 (이 계약을 선택한) 계약을 멈추고 서비스를 복원하기 전에 조사와 코드 업그레이드를 수행할 수 있다.

우리는 Aragon 조직에 들어오는 모든 공개 트랜젝션들을 살펴볼 봇을 만들고 있고, 이것은 위험일 수 있는 이상한 행동이나 예상하지 못한 스테이트 감지한다. Aragon Project 의 누군가를 찾아볼 수 있을 것이다. 봇이 위험이 충분히 크고 액션이 즉각적이어야 한다고 판단하면, 책임이 있는 사람들이 상황을 살펴보는 동안 모든 조직은 멈출 수 있다.

이것은 30초 이내에 모든 조직에서 공격을 멈추고 업그레이드된 메카니즘으로 즉시 수정을 할 수 있다는 것이다. 거짓 긍정의 경우 호출된 사람이 모든 사람이 활동을 다시 시작하고 다운 타임이 10분을 넘기지 않아야 한다.

#### 1.4. ANJ action against bad actors in an organization

Aragon Network Jurisdiction 문서에 정의된대로 네트워크의 모든 조직은 ANJ 탈중앙화 법원에 구속되는 것에 동의한다. 이는 개별 조직의 이해 관계자를 스마트 계약의 순수한 개관성으로부터 보호하여, 특정 사안을 encode 하는 것을 매우 어렵고 비효율적이게 만든다.

case 가 만들어지면, 법원은 조직의 컨트렉트르 변경하거나 취소시킬 수 있게 된다. 이것은 stakeholder 를 위한 보호 조치일 뿐이다. 충분한 채권을 유치함으로써, 조직의 주주들은 ANJ 에 사건을 제출할 수 있으며 보호 조치로 조직을 동결시킬 수 있다. 법원이 사건을 합법적이지 않다고 보면, 그 사람은 법정 (그리고 조직의 일부) 에게 채권을 잃을 것이다.

### 2. Tradeoffs

인생에서 가장 좋은 것들과 마찬가지로, 보안에도 절충점이 있다.
우리는 탈중앙화된 앱을 만들기위해 보안, 탈중앙화, 사용 편의성을 각 꼭지점에 둔 Zooko 의 삼각형과 비슷한 삼각형을 상상해볼 수 있다. 어느 하나에 너무 우선순위를 높히면, 이것은 다른 것의 희생으로 다가올 것이다.

우리는 세 가지 모두 매우 중요하게 생각하지만 세 가지 측면에서 완벽한 시스템을 갖추는 것은 너무 어렵다. 우리의 비전은 모든 사용자 또는 조직이 자신이 편하게 만들 수 있는 타협점을 선택할 수 있는 시스템을 만드는 것이다.

#### A. Security

보안이란 적시에 버그나 위협을 해결할 수 있는 능력을 의미한다.

#### B. Decentralization

업그레이드 메커니즘의 문제점은 최종적으로 신뢰할 수 있는 당사자가 소프트웨어 업그레이드를 수행하는 담당자이고, 이것은 매우 중앙집중화된 요소라는 것이다. 네트워크는 올비른 피어 리뷰를 받은 경우에만 업그레이드가 roll out 하도록 투표 체계를 추가할 수 있다.
이것이 우리의 업그레이드 메커니즘이 opt-in 인 이유다. 많은 보안을 가지지 않고 소프트웨어 업데이트를 수락많은 사람들이 있을 것이다..?

#### C. Ease of use

보안과 분권화를 최적화하는 경우, 누군가 조직을 업그레이드 하기 위해 Aragon 코드를 이해할 수 있어야만 하게 되어 쉬운 사용성이 약화될 수 있고, 이것은 큰 장벽이다.

### 3. Summary

이 문서에 설명된 방법을 사용하여 Aragon Network 는 다음을 보장할 수 있다:
- 향후 버그 수정 및 개선 사항을 계약에 추가할 수 있다.
- 버그 보상 프로그램, 글로벌 세이프 스톱, ANJ 액션 덕분에 중요한 취약점의 영향을 최소화 할 수 있다.




* 발표

Summary 를 먼저 보여주자


* 생각해보기
비용 절감
비효율성 절감
최선의 선택
기존의 비신뢰성
