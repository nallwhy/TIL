# Peer to peer & Blockchain & Hash

## Byzantine Generals Problem

비잔티움의 장군들 중에는 '충직한 장군'과 '적군의 장군'이 섞여 있을 때, 공격 계획을 수립하고 도시를 함락하기 위해

1. 최소 '충직한 장군'의 비율이 얼마나 있어야 하는가?
2. 장군들은 어떠한 규칙에 의해서 안전하게 교신해야 하는가?

### Hash function

입력을 받으면 일정 길이의 문자열을 출력하는 함수.

1. 동일한 입력에는 동일한 출력
2. 입력이 조금만 바뀌어도 출력이 완전히 바뀜
3. 출력으로 입력을 알아낼 수 없음
4. 출력이 충돌하지 않게 설계하는 것이 중요

* 충돌 가능성이 발견된 hash fucntion들: md5, sha1, crc32

### Conclusion

다수!
교신은 hash 로!

## Blockchain 이란 무엇인가

모든 참여자가 공유하는 회계 시스템.

장부 한 장은 한 block.
이전 block 에서 변경점을 모아 새로운 block 을 만들어 연결한 것이 blockchain.
현재 거래 내역을 변경하기 위해서는 가장 첫 장부부터 수정해야함.


## 기타

state root: transaction 들을 짝지어 계속 hash 를 구해 마지막에 구해진 값.

light node: block id + state root 로만 이루어진 blockchain을 가지고 있는 node.

full node 여야만 검증이 가능하다. 잔고를 알아야 거래가 valid 한지 알 수 있어.

3으로 시작하는 비트코인 주소는 multisig address.


## 궁금점

다른 노드들이 있는지 어떻게 알고 트랜잭션을 전송하지?
