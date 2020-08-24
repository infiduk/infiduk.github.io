---
title: "[Study] 블록체인 면접 공부"
date: 2019-10-26 19:29:00 +09:00
tags: study blockchain
comments: true
---

Blockchain Interview Questions

## 블록체인 면접 대비 공부
- 아직 배우고 있어서 잘못된 내용이 있을 수 있습니다. 언제든지 지적해주세요!

## 하이퍼레저 패브릭(Hyperledger Fabric) 구조 뜯어보기

### 하이퍼레저 패브릭이란?
- Hypereldger 내 블록체인 프로젝트 중 하나로, 기업에서 적용이 가능한 블록체인을 구현하는 목적을 가지고 있다.
- 다른 블록체인과 다른 컨소시움(Consortium) 블록체인으로, MSP를 통해 허가된 참여자만 접근이 가능하다. (private과 permissioned)
- 채널을 생성하여 참가자 그룹이 별도의 원장을 생성할 수 있도록 한다.

### 하이퍼레저 패브릭 구성요소

### Membership Service Provider(MSP)
- 주민등록증 발급 기관이라고 생각하면 된다!
- 멤버쉽 서비스
- 인증서 발급 및 유효성 검사와 사용자의 신원 인증에 필요한 모든 암호화 규칙을 추상화하고 정의한다.
- 트랜잭션 결과에 서명(보증)할 수 있다.
- 인증 기관(CA)을 사용한다. (기본 인터페이스로 Fabric-CA API가 사용되는데, 외부 CA를 사용할 수 있다.)
- 종류
  - Local MSP(로컬 MSP): 관리 권한이나 참가 권한을 가진 사용자를 로컬 레벨에서 정의한다. -> 모든 사용자나 노드는 정의된 로컬 MSP가 있어야 한다.
  - Channel MSP(채널 MSP): 관리 권한이나 참가 권한을 해당 조직의 구성원이 참여하는 채널 레벨에서 정의한다. -> 채널에는 정의된 채널 MSP가 있어야 한다.
  - 로컬 MSP와 채널 MSP는 동작 방식이 아닌 동작 범위의 차이점이 있다.

### Certificate Authority(CA)
- 인증 기관으로, 사용자 등록 및 블록체인에서 호출된 트랜잭션 및 구성 요소간의 보안 연결과 관련이 있다.
- 네트워크에 참여할 수 있는 인증서를 발급하고 배포한다.
- 하이퍼레저 패브릭에서는 X.509 디지털 인증서를 사용한 PKI 방식을 사용한다.
- 종류
  - Fabric CA
    - 내장 CA 구성요소로, X.509 디지털 인증서 형태의 개인 Root CA 공급자
    - Root CA를 위한 맞춤 CA
  - Root CA
    - 패브릭 참가자의 디지털 인증서를 관리한다.
  - Intermediate CA
    - 루트 CA의 노출을 제한하기 위해 사용한다.
    - 루트 CA에서 발급한 인증서나 다른 Intermediate CA에서 발급한 인증서가 존재할 수 있다.
    - 여러 조직에서 인증서를 발급할 때 유연하게 활용할 수 있다.
  - CA에서 발급한 인증서로 'Chain of Trust'를 형성해 CA의 기능을 확장하고 Root CA의 노출을 제한(인증서를 사용하는 조직이 신뢰를 갖고 중간 CA를 사용하도록 유도 -> 보안성 높임)할 수 있다.

### Peer
  - 체인코드를 실행하고 저장(Block, Transaction, State)한다.
  - 종류
    - Endorsing Peer
      - 클라이언트로부터 트랜잭션 요청이 들어오면 실행 후 Read/Write set을 클라이언트에게 반환한다.
      - 이 때 트랜잭션은 원장에 commit되지 않는다.
    - Committing Peer
      - 생성된 트랜잭션 블록을 수신하면 피어 노드 원장 사본에 commit 되기 전에 유효성을 검사한다.
      - 모든 피어는 Committing Peer이다.
    - Leader Peer
      - Ordering Peer로부터 조직의 다른 Committing Peer로 트랜잭션을 책임지고 배포한다.
      - 자동 선출(조직 당 하나의 피어만 선출)과 수동 선출(0개 또는 원하는 수의 피어를 선출)로 리더를 선출하고, 자동 선출에서 리더의 네트워크가 끊어졌을 경우 남은 피어들 중 리더를 재선출한다.
    - Anchor Peer
      - 다른 조직의 피어와 통신한다.
      - 채널 구성에서 정의할 수 있으며, 0개 이상의 Anchor Peer가 존재할 수 있다.
  - 한 개의 노드가 Endorsing, Committing, Leader, Anchor Peer의 역할을 할 수 있다.

### Organization(Org)

### Orderer

### Channel

### Chaincode

## 미디움 블록체인 개발자 면접 오픈북
- 출처: [[미디움] 블록체인 R/D 부분 면접 오픈북 (HAMA 블로그)](https://hamait.tistory.com/1054)

### Blockchain 2. 토큰과 코인의 차이
- 토큰
  - 독립된 블록체인 네트워크(메인넷)를 가지고 있지 않고, 기존 플랫폼에서 파생되어 만들어진 암호화폐 (ex. 이더리움 플랫폼에서 만들어진 토큰)
- 코인
  - 독립된 블록체인 네트워크를 가지고 있는 암호화폐 (ex. BTC, ETH ...)

### Hyperledger Fabric 1. 하이퍼레저 패브릭 트랜잭션 흐름
![image_01](https://user-images.githubusercontent.com/48206157/68653439-16c8f980-056f-11ea-92b7-9a7178a73423.png)
<br />
<br />
1. 앱에서 클라이언트가 SDK를 이용해 트랜잭션을 발생시킨다.
2. Endorsing Peer가 트랜잭션을 검증하고 실행한 후 Read/Write Set을 클라이언트에 반환한다.
- 트랜잭션이 잘 구성되었는지, 서명이 유효한지 MSP를 사용해 검증
- 원장 업데이트는 진행되지 않는다.
3. 클라이언트는 반환 받은 응답을 Orderer에 브로드캐스트한다.
- 트랜잭션에는 Read/Write Set, 서명, 채널 ID 등이 포함
4. Orderer는 트랜잭션을 정렬한다.
- 모든 채널로부터 트랜잭션을 받고, 시간순으로 트랜잭션을 정렬
5. 트랜잭션이 검증되고 commit 된다.
- 트랜잭션은 채널의 모든 피어에게 전달된다.
- 검증된 후 트랜잭션의 유효, 무효 여부가 구분된다.
6. World State에 값이 저장되고 원장이 업데이트 된다.

### Hyperledger Fabric 4. 하이퍼레저 패브릭 MSP
- 멤버쉽 서비스
- 인증서 발급 및 유효성 검사와 사용자의 신원 인증에 필요한 모든 암호화 규칙을 정의한다.
- 트랜잭션 결과에 서명(보증)할 수 있다.
- 인증 기관(CA)을 사용한다. (기본 인터페이스로 Fabric-CA API가 사용되는데, 외부 CA를 사용할 수 있다.)
- 종류
  - Local MSP(로컬 MSP): 관리 권한이나 참가 권한을 가진 사용자를 로컬 레벨에서 정의한다. -> 모든 사용자나 노드는 정의된 로컬 MSP가 있어야 한다.
  - Channel MSP(채널 MSP): 관리 권한이나 참가 권한을 해당 조직의 구성원이 참여하는 채널 레벨에서 정의한다. -> 채널에는 정의된 채널 MSP가 있어야 한다.
  - 로컬 MSP와 채널 MSP는 동작 방식이 아닌 동작 범위의 차이점이 있다.

### Hyperledger Fabric 5. 하이퍼레저 패브릭 채널 MSP와 네트워크 MSP
- Channel MSP
- Network MSP

### Hyperledger Fabric 7. 하이퍼레저 패브릭 Fabric-CA가 하는 역할
- Fabric CA
  - 내장 CA 구성요소로, X.509 디지털 인증서 형태의 개인 Root CA 공급자
  - Root CA를 위한 맞춤 CA

### Hyperledger Fabric 14. 하이퍼레저 패브릭 리더피어와 앵커피어
- Leader Peer
  - Ordering Peer로부터 조직의 다른 Committing Peer로 트랜잭션을 책임지고 배포한다.
  - 자동 선출(조직 당 하나의 피어만 선출)과 수동 선출(0개 또는 원하는 수의 피어를 선출)로 리더를 선출하고, 자동 선출에서 리더의 네트워크가 끊어졌을 경우 남은 피어들 중 리더를 재선출한다.
- Anchor Peer
  - 다른 조직의 피어와 통신한다.
  - 채널 구성에서 정의할 수 있으며, 0개 이상의 Anchor Peer가 존재할 수 있다.

### Consensus 1. Safety(Finality) & Liveness
- Safety(Finality)
  - 문제 없는 노드 사이에서는 잘못된 합의가 이루어지지 않는다.
  - 아무 문제 없는 두 노드가 서로 다른 값으로 합의했다는 것은 같은 높이에서 서로 다른 블록이 생성되었다는 것이다.
  - 유효한 트랜잭션을 가진 체인은 둘 이상 존재하지 않는다.
- Liveness
  - 문제 없는 노드들은 반드시 합의를 한다.
  - 분산 시스템에서의 합의는 노드 간의 메시지를 주고 받으며 각 노드의 상태를 변경시키며 이루어진다. 이떄, 문제 없는 노드들은 무한 루프에 빠지지 않고 반드시 상태 변경이 종료되어야 한다.

### Consensus 2. CFT vs BFT
- CFT
  - 분산 시스템에서 노드에 비정상적인 충돌이 일어나 문제가 발생하더라도 나머지 시스템에서 서비스를 진행할 수 있게 하는 것이다.
- BFT
  - 잘못된 정보를 전달하는 배신자 노드가 있더라도 동작하는 것이다.
  - 시스템에 장애가 생기더라도 견디는 것.

### Consensus 3. POW와 POS의 가장 큰 차이점
- Safety(Finality) & Liveness 관점
- POW
  - 문제를 더 빨리 풀 경우 그 체인을 유효한 체인으로 판단한다.
  - 즉, 지금 체인보다 더 긴 체인을 만들 수 있을 만한 파워를 가지면 기존의 합의된 블록을 언제든지 바꿀 수 있다 -> Finality가 보장되지 않는다. (Liveness를 위해 Safety를 포기)
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
- [Hyperledger Fabric Interview Questions (영문)](https://vitalflux.com/hyperledger-fabric-distributed-ledger-interview-questions-notes/)
- [2018년 12월 hyperledger fabric interview questions (영문)](https://www.biganalytics.me/2018/12/hyperledger-fabric-real-interview.html)
- [Top blockchain interview questions (영문)](https://intellipaat.com/blog/interview-question/blockchain-interview-questions/)
- [Top 55 blockchain interview in 2019 (영문)](https://www.edureka.co/blog/interview-questions/blockchain-interview-questions/)
- [하이퍼레저 패브릭 소개 및 구조 설명](https://blog.naver.com/mage7th/221493540794)
- [블록체인 기술 개요 - 아이콘루프](https://blog.theloop.co.kr/2017/03/15/%eb%b8%94%eb%a1%9d%ec%b2%b4%ec%9d%b8-%ea%b8%b0%ec%88%a0-%ea%b0%9c%ec%9a%94/)
- [LINE 개발자분 인터뷰](https://blog.naver.com/PostView.nhn?blogId=mage7th&logNo=221575023525)