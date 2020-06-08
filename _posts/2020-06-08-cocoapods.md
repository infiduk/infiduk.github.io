---
title: "[Xcode/CocoaPods] Library not found for - IFirebaseCore"
date: 2020-06-08 11:44:00 +09:00
tags: study xcode cocoapods swift ios error
comments: true
---

Error: Library not found for - IFirebaseCore

## Library not found for - IFirebaseCore

## 로그
``` swift
Library not found for - IFirebaseCore
```
![image_01](https://user-images.githubusercontent.com/48206157/83988312-d8b57c00-a97d-11ea-838e-b9e3dab55826.png)

## 발생 원인
- 개발자분이 넘겨주신 소스를 그대로 받아서 실행시켰는데, **IFirebaseCore**를 찾지 못해서 발생
- 해당 **Library**가 설치된 경로 및 캐시 문제로 인해 발생

## 해결 방법
- 프로젝트 폴더에 있는 **Pods 폴더**와 **.xcworkspace 파일**, **Podfile.lock 파일**을 삭제
- `Pod install` 을 다시 진행
  ``` shell
  # 사용한 Podfile
  target 'xxx' do
    use_modular_headers!

    ...

    # Pods for xxx
    pod 'Firebase/Core'
    pod 'Firebase/Messaging'

    ...

  end
  ```
- 새로 생긴 **.xcworkspace 파일**로 프로젝트를 열고, 실행시키면 해결