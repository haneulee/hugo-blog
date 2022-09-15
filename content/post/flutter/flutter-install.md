---
title: "플러터(flutter) 설치"
date: 2021-05-18T12:40:39+09:00
categories:
  - development
  - flutter
tags:
  - development
  - front-end
  - Android
  - flutter
  - 플러터
  - ios
  - 앱개발
  - mobile
  - 모바일
  - swift
  - javascript
keywords:
  - development
  - front-end
cover: ""
draft: false
thumbnailImagePosition: left
thumbnailImage: "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcvwEfZ%2FbtqIFw2Kt69%2FZrqh8pmu2fyrYUMWykbLwk%2Fimg.png"
# coverImage: //d1u9biwaxjngwg.cloudfront.net/cover-image-showcase/city.jpg
metaAlignment: center
coverMeta: out
---

# 플러터 Flutter 📱

[flutter-ko.dev/docs/get-started/install/macos](https://flutter-ko.dev/docs/get-started/install/macos)

## 플러터 설치 방법은 아래와 같이 2가지가 있다. 

<!--adsense-->

1.  플러터 sdk로 설치하기
2.  git clone 으로 설치하기
    1.  [github.com/flutter/flutter.git](https://github.com/flutter/flutter.git)

## 다음은 아래와 같이 flutter PATH  설정하기

```
cd vi .bash_profile
```

```
export PATH="$HOME/Desktop/flutter/bin:$PATH"
```

:wq로 저장 후 source .bash_profile을 사용하여 적용시켜준다.

플러터 디렉토리 경로로 가서 pwd 로 경로 찾아서 설정해줘도 됨

```
flutter doctor
```

를 실행한다.

ios면 xcode android면 android studio 관련하여 잘 설정이 되었는지 확인할 수 있다.

xcode 버전이 최소 11이상이어야 해서 맥os 업데이트와 xcode 설치까지 오랜 시간이 걸렸다 ㅠㅠ

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbzWjbD%2FbtqIrtUywhh%2FiIIFlKx57k8ecdE1ZdvUz1%2Fimg.png)

나는 ios만 테스트할 것이므로 안드로이드 관련 설정은 패스!!!

## 다음은 flutter 프로젝트 생성!

```
flutter create my_app

cv my_app
```

위와 같이 간단하게 플러터로 프로젝트 생성이 가능하다.

```
open -a Simulator
```

로 xcode simulator 를 실행하고

```
flutter run
```

플러터를 실행하면

앱 연동 완성!!

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcvwEfZ%2FbtqIFw2Kt69%2FZrqh8pmu2fyrYUMWykbLwk%2Fimg.png)
