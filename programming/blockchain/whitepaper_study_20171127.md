# 0x

Decentralized Exchanges

## 중앙화 거래소의 문제

- 해킹 타겟
- 내부자 절도
- 보안 문제
- DDos 취약

## 탈중앙화 거래소(DEX)

사용자들의 코인을 사용자의 지갑에 보관

문제점
- Latency
- Gas Cost
- Liquidity 부족

## 0x 등장 배경

- 블록체인에는 최종 settlement
- orderbook 관리는 off-chain network

이더리움 블록체인에서 분산된 교환을 위한 개방형 프로토콜.

0x 프로토콜은 하나의 거래소가 **아님**.

## Relayer

Maker(오더 만드는 사람) -> Relayer(거래 연결) -> Taker(오더를 승낙하는 사람)

- 자신의 수수료 정책을 공개적인 곳에 업로드.
- orderbook 을 관리하고 taker 를 모집.
- 거래소 역할
- 대가로 ZRX Token 수수료를 받음

## 특징

- 중계를 Relayer 에게 위임
- 거래 내용은 암호화 되어 Relayer 가 간섭 불가
- 만료 일자가 있어서 시간 지나면 못함
- P2P 거래로도 사용 가능
- on-chain 거래는 1회
- 거래 기능을 가진 dApp 간에 유동성 교환 표준 프로토콜 지향 (부족한 코인을 거래소간 교환 가능)
- 부분 거래 가능

## 단점

ERC20 Token 에만 작동

## Flow

1. Maker 가 입금 (DEX 에게 Token A 접근을 허용)
2. Maker 가 Order 작성
3. Maker 가 Order 전달
4. Taker 가 Order 를 선택
5. Taker 가 입금 (DEX 에게 Token B 에 접근을 허용)
6. Taker 가 Order 를 DEX 에 제출
7. DEX 가 Order 를 체결 (Order 가 유효한가, Token 상호 전달, fee 지불)

## Relayer 의 order 전달 자세하게

1. Relayer 가 수수료 정책과 지갑 주소 게시
2. Maker 가 Relayer 의 수수료 정책에 맞게 Order 생성
3. Maker 가 Signed order 를 Relayer 에게 전달
4. Relayer 가 Signed order 검증하고 등록
5. Taker 가 orderbook 받음
6. Taker 가 order 선택

## 잘문

상수배 효율 o


# Airswap

- Intercoin 간의 Exchange. P2P not decentralized.
- DEX level 에서 protocol level 로
- Orderbook 이 없음

## 질문

Oracle 가능한가?
