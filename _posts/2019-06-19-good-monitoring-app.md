---
title: "Good Monitoring app"
date: 2019-10-21 17:59:00 +09:00
tags: android java xml mysql project
---

Supporters Recruitment Monitoring App with android

## 2019 캡스톤 디자인 프로젝트 - Good Monitoring App

## 프로젝트 팀원
- 자바조 (4명)
- [원소희](https://github.com/infiduk)

## 프로젝트 기간
- 2019.03 ~ 2019.06

## 프로젝트 개요
- 2019년 1학기 캡스톤 디자인 프로젝트입니다.
- [(주)굿 모니터링](http://goodmonitoring.com) 회사와 연계해 산업체 연계 과제로 진행하였습니다.

### 현황 및 문제점
1. 현재 다양한 분야(일반, 주부, 학생, 시니어 등)의 서포터즈(모니터링) 공고가 있음에도 불구하고, 그 공고들을 모집 대상들에게 알려주는 **안드로이드 앱**은 매우 **부족**합니다.
2. 기존의 모니터링 사이트들은 대부분 **웹**상에서만 존재합니다.
3. 교내에서 진행하는 프로젝트로는 한계가 있다고 생각하여, 실무에서 직접 개발을 진행해보고자 합니다.

### 제안
1. **굿 모니터링**과 연계를 통해 **접근성이 용이**하고, 모집 공고가 **한 눈**에 들어오는 **안드로이드 앱**을 만들고자 합니다.
2. 회원가입 시 **기관**과 **사용자**로 구분하여 기관의 경우에는 프로젝트 공고 등록 신청 및 공고 관리가 가능하도록 하고, 사용자의 경우에는 메인으로 공고 목록을 띄워 자신이 마음에 드는 공고에 신청할 수 있도록 합니다.
3. 서포터즈 신청과 함께 **굿 모니터링 메일링 신청**도 **함께**할 수 있도록 유도해 굿 모니터링 메일링 회원을 증가시키고자 합니다.
4. 추후 유지보수를 위해 **확장성 있는 개발**을 목표로 합니다.

## 개발 언어 및 구성 환경
- Language: Java, XML
- IDE: Android Studio
- DB: MySQL
- OS: Window

## 구현 내역
1. 회원 구분을 관리자, 기관, 사용자로 나누어 구현하였습니다.
  - 기관은 모니터링 정보에 대한 공고 목록 보기, 공고 등록, 수정 및 삭제가 가능합니다.
  - 사용자는 모니터링 모집 공고를 보고 원하는 모집 공고에 지원할 수 있습니다.
2. 초기 화면 진입시 최신 등록된 공고, 인기 있는 공고 순으로 모집 공고를 열람할 수 있습니다.
3. 사이드 바를 이용해 사용자가 메뉴를 이동하는데 어려움이 없도록 구현하였습니다.
<br />
<br />
- 화면 리스트
<br />
  - 메인 화면
  <br />
  ![image_01](https://user-images.githubusercontent.com/48206157/67191186-2f406b00-f42c-11e9-8cdd-a5d121d5c826.png)
  <br />
  <br />
  - 공고 등록 화면
  <br />
  ![image_02](https://user-images.githubusercontent.com/48206157/67191244-42533b00-f42c-11e9-9a87-6a4985149d53.png)
  <br />
  <br />
  - 사이드 바 화면
  <br />
  ![image_03](https://user-images.githubusercontent.com/48206157/67191289-572fce80-f42c-11e9-9246-47cb9b590e0c.png)

## 프로젝트 내 역할
- 프로젝트 기획 및 총괄
- Front-end
- Back-end

## Github
- [Good Monitorig app Github Link](https://github.com/infiduk/good-monitoring-app)