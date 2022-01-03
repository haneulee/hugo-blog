---
title: "TIL📚 앱개발 스터디 - 4 week"
date: 2022-01-03T12:57:22+09:00
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

# TIL📚 앱개발 스터디 - 4 week

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/til/til.png)

## Firebase 👩🏻‍💻

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/til/firebase.png)

{{< alert info >}}
파이어베이스는 구글에서 만든 서버리스 서비스
{{< /alert >}}

- 데이터베이스
- 이미지 파일 서버
- 푸시 알람 기능
- 로그인 인증 기능

### Serverless

1. 데이터 생성
2. 데이터 조회
3. 데이터 삭제/수정 등을 제공해주는 서비스들이 존재합니다.

### 파이어베이스 설치

```
npm install firebase
yarn add firebase
expo install firebase
```

### 파이어베이스 config 설정

처음에 데이터베이스 연동이 되지 않아 확인해봤더니 지역 설정이 맞지 않는 경우가 있어
databaseURL을 따로 설정해주었다.

```
// 사용할 파이어베이스 서비스 주석을 해제합니다
//import "firebase/compat/auth";
import "firebase/compat/database";
//import "firebase/compat/firestore";
//import "firebase/compat/functions";
import "firebase/compat/storage";

import firebase from "firebase/compat/app";

// Initialize Firebase
//파이어베이스 사이트에서 봤던 연결정보를 여기에 가져옵니다
const firebaseConfig = {
  apiKey: "",
  authDomain: "sparta-react-native-11669.firebaseapp.com",
  projectId: "sparta-react-native-11669",
  storageBucket: "sparta-react-native-11669.appspot.com",
  messagingSenderId: "",
  appId: "",
  measurementId: "",
  databaseURL:
    " https://sparta-react-native-11669-default-rtdb.asia-southeast1.firebasedatabase.app",
};
//사용 방법입니다.
//파이어베이스 연결에 혹시 오류가 있을 경우를 대비한 코드로 알아두면 됩니다.
if (!firebase.apps.length) {
  firebase.initializeApp(firebaseConfig);
}

export const firebase_db = firebase.database();

```

### Storage

멀리 있는 파일 저장소에 이미지 및 사용 할 파일을 올려두고, 필요할 때마다 꺼내 쓰는 용도로 사용

```
const ref = firebase_storage.ref("general/main.png");
const url = await ref.getDownloadURL();

```

### Realtime Database

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/til/firebase-screen.png)

#### 데이터베이스 API

아래와 같이 config의 firebase_db를 연결하여 "/tip" 을 ref로 넣고
snapshot.value로 값을 가져온다.

사용방법은 공식문서에서 확인!!

[firebase API 👉](https://firebase.google.com/docs/reference/rest/database)

```

import { firebase_db } from "../firebaseConfig";

firebase_db
        .ref("/tip")
        .once("value")
        .then((snapshot) => {
          let tip = snapshot.val();
          console.log("MainPage > 파이어베이스에서 데이터 가져왔습니다!!", tip);

          setState(tip);
          setCateState(tip);
          getLocation();
          setReady(false);
        });
```

## TIL ✅

파이어베이스의 스토리지, 데이터베이스가 주된 학습 내용이었고,
weather API 적용도 해보았다.

expo-constants의 installationId 가 deprecated 되어
uuid를 사용하여 아이디 설정을 하였고,
추후 로그인 기능이 필요해보인다.

---

참고 :
[스파르타 코딩클럽](https://spartacodingclub.kr/),
[React Naitve](https://reactnative.dev/),
[Firebase](https://firebase.google.com/),
