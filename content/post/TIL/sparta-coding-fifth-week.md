---
title: "TIL📚 앱개발 스터디 - 5 week"
date: 2022-01-05T19:26:50+09:00
categories:
  - development
  - react native
tags:
  - development
  - front-end
  - react-native
  - javascript
  - til
  - sparta
  - coding
  - 스파르타코딩
  - react native
  - android
  - expo
  - ios
  - app
keywords:
  - development
  - front-end
cover: ""
thumbnailImagePosition: left
thumbnailImage: https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/til/til.png
# coverImage: //https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/hugo/github-site.png
metaAlignment: center
coverMeta: out
draft: false
---

<!--toc-->

{{< adsense >}}

# TIL📚 앱개발 스터디 - 5 week

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/til/til.png)

## 구글 앱스토어 출시

{{< alert info >}}
아직 검토중!
{{< /alert >}}

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/til/appstore-screen.png)

## 프로젝트 녹화 영상

<img src="https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/til/honeytip-video.gif" alt="drawing" width="200"/>

## 취지 & 설명

꿀팁에 대한 정보를 담은 앱

## 기술 설명

- 파이어베이스
- 리액트 네이티브
- expo
- axios
- ...etc

```
"@expo/vector-icons": "^12.0.0",
"@react-native-async-storage/async-storage": "~1.15.0",
"@react-native-community/masked-view": "^0.1.11",
"@react-navigation/native": "^6.0.6",
"@react-navigation/stack": "^6.0.11",
"axios": "^0.24.0",
"expo": "~43.0.2",
"expo-ads-admob": "~11.0.3",
"expo-app-loading": "~1.2.1",
"expo-asset": "~8.4.3",
"expo-constants": "^13.0.0",
"expo-font": "~10.0.3",
"expo-linking": "~2.4.2",
"expo-location": "^14.0.1",
"expo-status-bar": "~1.1.0",
"firebase": "^9.6.1",
"react": "17.0.1",
"react-dom": "17.0.1",
"react-native": "0.64.3",
"react-native-gesture-handler": "~1.10.2",
"react-native-reanimated": "~2.2.0",
"react-native-safe-area-context": "3.3.2",
"react-native-screens": "~3.8.0",
"react-native-uuid": "^2.0.1",
"react-native-web": "0.17.1"
```

## 어려웠던 점 & 극복 방법

실제 기술스택 버전이 업데이트 되거나 deprecated 된 함수도 있었다.
파이어베이스 리얼타임 데이터베이스를 연동할 때는 오류가 있어서
firebaseConfig에 아래와 같이 데이터베이스 url 코드를 추가해주었다.

```
databaseURL:
    " https://sparta-react-native-11669-default-rtdb.asia-southeast1.firebasedatabase.app",
```

그리고 AsyncStorage 로 uuid 를 사용해 user Id를 발급하고
처음에 앱 로딩 시, 로컬스토리지에 아이디를 저장하도록 개발했다.
추후, 로그인 기능을 구현하면 좋을 것 같다.

## 5주간의 앱개발 수업 후기 ✅

5주동안 매주 숙제와 개발일지를 통해 한주에 배운것들을 복습할 수 있었고,
어떤걸 배웠는지 까먹지 않게 잘 기록도 했던것 같다.
마지막 5주차에는 실제 배포한 앱을 공유하는 것인데
내가 원하는 앱을 따로 만들기에는 시간이 부족해
앞으로 차차 개발하여 올려볼 예정이다.

---

참고 :
[스파르타 코딩클럽](https://spartacodingclub.kr/),
[React Naitve](https://reactnative.dev/),
[Firebase](https://firebase.google.com/),
