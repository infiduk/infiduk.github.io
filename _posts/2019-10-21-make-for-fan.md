---
title: "[Project] Make for Fan"
date: 2019-10-21 15:56:00 +09:00
tags: hyperledger-fabric react javascript go mongo project
comments: true
---

Fan Vote App Project based on Hyperledger Fabric

## 2019 KBCI, 공개SW Hackathon 프로젝트 - Make for Fan (of the Fan, by the Fan, for the Fan)

## 프로젝트 팀원
- 3명
- [원소희](https://github.com/infiduk)
- [박찬형](https://github.com/ch-4ml)
- [최한솔](https://github.com/9992)

## 프로젝트 기간
- 2019.10 ~ 2019.11

## 프로젝트 개요
- 2019 KBCI, 공개SW Hackathon 프로젝트입니다.
- 팬을 위한 투표 앱입니다.

### 현황 및 문제점
1. 최근 서바이벌 **오디션 프로그램**이 폭발적인 인기를 끌었습니다. 시청자는 **국민 프로듀서**가 되어 자신이 좋아하는 연습생에게 표를 행사하고 투표한 **결과**에 따라 연습생들이 그룹을 이루어 **데뷔**하게 되는데, 이렇게 데뷔한 그룹들은 차세대 **K-POP 인기의 주역**이 되었습니다.
2. 하지만, 얼마 전 **100%** '국민 프로듀서'의 투표로만 데뷔 멤버가 정해진다는 방송국 측의 말과 달리 **내부자**가 투표에 관여해 결과를 **조작**했다는 사실이 발각되었습니다. 이에 따라 해당 오디션 프로그램으로 데뷔하게 된 연습생들이 더이상 방송 활동을 하지 못하게 조치가 취해졌고 있고, 분노한 시청자들은 제작진에게 책임을 묻고 있습니다.

### 제안
1. 팬들에게 **투명한** K-POP 투표 시스템을 제공하고자 합니다. 나아가 K-POP 팬들에게 **혜택**이 돌아가는 서비스를 제공합니다.
2. **두 가지 선택지**를 주고, 사용자들에게 **재미**와 **흥미** 요소를 제공하는 프로젝트로 진행합니다.
3. 투표 진행 및 투표 결과를 **블록체인**에 **기록**함으로써 소비자, 즉 투표권을 가진 사람들에게 알 권리 및 투표 결과에 대한 **신뢰성**을 **보장**해주고자 합니다.
4. 일상에서 충분히 접할 수 있는 선택지를 문제로 제공해 사용자들의 자연스러운 참여를 유도하고, 그에 따른 데이터를 모으고자 합니다.

## 기획 및 설계 문서
- [Make for Fan Notion Link](https://www.notion.so/ilovekakao/QnQ-5005e961e4bf4a7ca1021eb32a439e8a)
<br />
![image_01](https://user-images.githubusercontent.com/48206157/68637534-431a5100-0542-11ea-949c-8bb64ce43cb5.png)

## 개발 언어 및 구성 환경
- Blockchain: Hyperledger-Fabric
- Language: javascript, go
- Library: React.js
- DB: Mongo (Heroku)
- OS: Window, iOS, Android, Linux
- IDE: VSCode

## 구현 내역

### 기능
1. 다수의 팬들이 선택한 선택지가 해당 투표의 답으로 인정되어 그 선택지를 선택한 팬에게 혜택이 돌아가도록 구현하였습니다.
2. 문제가 오픈되면 사용자들이 자유롭게 투표에 참여할 수 있도록 합니다.
  - 투표 결과는 특정 시간 이후 모두 공개되며, 승리한 쪽은 패배한 쪽의 티켓을 공평하게 나누어 갖습니다.
3. 진행된 문제는 모두 공개합니다.

### 화면
- 게임 리스트 화면
<br />
![image_01](https://user-images.githubusercontent.com/48206157/68011846-b8c52800-fccb-11e9-98dc-b3c115bb21e0.png)
<br />
<br />
- 게임 화면
<br />
![image_02](https://user-images.githubusercontent.com/48206157/68011890-d2ff0600-fccb-11e9-9707-4c8a0cea3315.png)
<br />
<br />
- 게임 결과 화면
<br />
![image_03](https://user-images.githubusercontent.com/48206157/68011922-ead68a00-fccb-11e9-8f4e-ffd0d08f14f0.png)

## 프로젝트 내 역할
- Front-end

## Github
- [Make for Fan Github Link](https://github.com/infiduk/fff)
