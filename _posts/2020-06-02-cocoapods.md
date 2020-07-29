---
title: "[Xcode] CocoaPods(코코아팟) 설치 및 사용법"
date: 2020-06-02 09:55:02 +09:00
tags: study xcode cocoapods swift ios
comments: true
---

How to use CocoaPods in Xcode

## CocoaPods(코코아팟) 설치 및 사용법

> iOS 프로젝트를 CocoaPods로 우아하게 만들어보자!

## CocoaPods?
- The Dependency Manager for iOS & Mac projects.
- 라이브러리 의존성 관리 매니저로, 굉장히 많은 라이브러리들이 있고.. 실 사용되는 앱에 굉장히 많이 사용되고 있다!

## 1. CocoaPods 설치

### 1.1 CocoaPods 사이트 접속
- `CocoaPods` 사이트에 접속합니다.
<br />
(아래 이미지를 클릭하시면 바로 접속하실 수 있습니다.)
<br />
[![image_01](https://user-images.githubusercontent.com/48206157/83469085-aefde000-a4b9-11ea-9aff-55d51b8a694e.png)](https://cocoapods.org)
<br />
<br />
- 사이트에 접속하지 않고, 터미널에 [아래](#install)의 명령어를 입력하셔서 바로 설치하셔도 됩니다!

### 1.2 CocoaPods 설치
- #install 설치 명령어를 터미널에 입력해 `CocoaPods`를 설치하실 수 있습니다!
<br />
  ``` shell
  $ sudo gem install cocoapods
  ```
- 아래 스크린샷처럼 나왔다면 설치 완료!
<br />
![image_02](https://user-images.githubusercontent.com/48206157/83470821-1a49b100-a4be-11ea-9303-91aa6e76623f.png)

## 2. CocoaPods 적용하기

### 2.1 CocoaPods를 적용할 프로젝트로 이동
- `CocoaPods` 설치가 완료 되었으니 적용을 시켜봅시다.
- 현재 개발 진행 중인 프로젝트의 경로로 이동합니다.
<br />
![image_03](https://user-images.githubusercontent.com/48206157/83471362-7cef7c80-a4bf-11ea-8f83-055ac610a8e4.png)

#### 2.1.1 프로젝트가 없다면?
- 먼저 `Xcode`에서 프로젝트를 생성해주세요!

### 2.2 CocoaPods Init
- 해당 경로에서 `CocoaPods`를 `init` 해주세요!
