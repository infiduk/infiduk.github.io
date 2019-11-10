---
title: "[Study] 블록체인 면접 공부"
date: 2019-10-26 19:29:00 +09:00
tags: study blockchain
comments: true
---

Blockchain Interview Questions

## 블록체인 면접 대비 공부
- 아직 배우고 있어서 잘못된 내용이 있을 수 있습니다. 언제든지 지적해주세요!

## 미디움 블록체인 개발자 면접 오픈북
- 출처: [[미디움] 블록체인 R/D 부분 면접 오픈북 (HAMA 블로그)](https://hamait.tistory.com/1054)

### Consensus 1. Safety(Finality) & Liveness
- Safety(Finality)
  - 문제 없는 노드 사이에서는 잘못된 합의가 이루어지지 않는다.
  - 아무 문제 없는 두 노드가 서로 다른 값으로 합의했다는 것은 같은 높이에서 서로 다른 블록이 생성되었다는 것이다.
  - 유효한 트랜잭션을 가진 체인은 둘 이상 존재하지 않는다.
<br />
- Liveness
  - 문제 없는 노드들은 반드시 합의를 한다.
  - 분산 시스템에서의 합의는 노드 간의 메시지를 주고 받으며 각 노드의 상태를 변경시키며 이루어진다. 이떄, 문제 없는 노드들은 무한 루프에 빠지지 않고 반드시 상태 변경이 종료되어야 한다.

### Consensus 2. CFT vs BFT
- CFT
  - 분산 시스템에서 노드에 비정상적인 충돌이 일어나 문제가 발생하더라도 나머지 시스템에서 서비스를 진행할 수 있게 하는 것이다.
<br />
- BFT
  - 잘못된 정보를 전달하는 배신자 노드가 있더라도 동작하는 것이다.
  - 시스템에 장애가 생기더라도 견디는 것.

### Consensus 3. POW와 POS의 가장 큰 차이점
- Safety(Finality) & Liveness 관점
- POW
  - 문제를 더 빨리 풀 경우 그 체인을 유효한 체인으로 판단한다.
  - 즉, 지금 체인보다 더 긴 체인을 만들 수 있을 만한 파워를 가지면 기존의 합의된 블록을 언제든지 바꿀 수 있다 -> Finality가 보장되지 않는다. (Liveness를 위해 Safety를 포기)
<br />
- POS
  - 서로 합의하는 과정이 있고, 일정 수 이상의 동의가 필요하다.
  - 전송한 메시지가 시간 안에 도달하는 것을 보장하지 못 하는 비동기 네트워크에서는 합의가 이루어지지 않아 블록이 생성되지 않을 수 있다.

### Consensus 4. PBFT 알고리즘
- 한 노드가 리더가 되고, 리더가 요청을 정리해서 다른 노드들에게 보낸다. 각 노드들은 자신을 제외한 모든 노드에게 다시 내용을 보내고, 일정 수 이상 요청을 수신 및 회신하면 그 내용을 수행하고 결과를 집계한 뒤 다수의 의견에 따라 블록을 확정한다.
- 다수결로 의사결정을 한 후 블록이 생성되기 때문에 분기가 발생하지 않는다. -> 한번 확정된 블록은 바뀌지 않는다. (Finality 보장)
- 부정 노드가 있어도 과반 이상을 확보해야 하고, 리더가 부정 노드일 경우에도 모든 노드가 리더를 감시하고 있기 때문에 시스템적인 장애에 강하다.
- 모든 노드들과 의사결정을 해야하기 때문에 노드의 수가 제한적이다.

<!-- ### Consensus 5. DPOS 알고리즘
-  -->

## 참고 사이트
- [goQuality-dev-contents](https://github.com/Integerous/goQuality-dev-contents)
<br />
- [Hyperledger Fabric Interview Questions (영문)](https://vitalflux.com/hyperledger-fabric-distributed-ledger-interview-questions-notes/)
- [2018년 12월 hyperledger fabric interview questions (영문)](https://www.biganalytics.me/2018/12/hyperledger-fabric-real-interview.html)
- [Top blockchain interview questions (영문)](https://intellipaat.com/blog/interview-question/blockchain-interview-questions/)
- [Top 55 blockchain interview in 2019 (영문)](https://www.edureka.co/blog/interview-questions/blockchain-interview-questions/)
<br />
- [하이퍼레저 패브릭 소개 및 구조 설명](https://blog.naver.com/mage7th/221493540794)
- [블록체인 기술 개요 - 아이콘루프](https://blog.theloop.co.kr/2017/03/15/%eb%b8%94%eb%a1%9d%ec%b2%b4%ec%9d%b8-%ea%b8%b0%ec%88%a0-%ea%b0%9c%ec%9a%94/)
<br />
- [LINE 개발자분 인터뷰](https://blog.naver.com/PostView.nhn?blogId=mage7th&logNo=221575023525)