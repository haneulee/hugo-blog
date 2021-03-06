---
title: "TIL๐ ์ฑ๊ฐ๋ฐ ์คํฐ๋ - 4 week"
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
  - ์คํ๋ฅดํ์ฝ๋ฉ
  - react native
  - android
  - expo
  - ios
  - app
  - firebase
  - ํ์ด์ด๋ฒ ์ด์ค
  - storage
  - database
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

# TIL๐ ์ฑ๊ฐ๋ฐ ์คํฐ๋ - 4 week

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/til/til.png)

## Firebase ๐ฉ๐ปโ๐ป

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/til/firebase.png)

{{< alert info >}}
ํ์ด์ด๋ฒ ์ด์ค๋ ๊ตฌ๊ธ์์ ๋ง๋  ์๋ฒ๋ฆฌ์ค ์๋น์ค
{{< /alert >}}

- ๋ฐ์ดํฐ๋ฒ ์ด์ค
- ์ด๋ฏธ์ง ํ์ผ ์๋ฒ
- ํธ์ ์๋ ๊ธฐ๋ฅ
- ๋ก๊ทธ์ธ ์ธ์ฆ ๊ธฐ๋ฅ

### Serverless

1. ๋ฐ์ดํฐ ์์ฑ
2. ๋ฐ์ดํฐ ์กฐํ
3. ๋ฐ์ดํฐ ์ญ์ /์์  ๋ฑ์ ์ ๊ณตํด์ฃผ๋ ์๋น์ค๋ค์ด ์กด์ฌํฉ๋๋ค.

### ํ์ด์ด๋ฒ ์ด์ค ์ค์น

```
npm install firebase
yarn add firebase
expo install firebase
```

### ํ์ด์ด๋ฒ ์ด์ค config ์ค์ 

์ฒ์์ ๋ฐ์ดํฐ๋ฒ ์ด์ค ์ฐ๋์ด ๋์ง ์์ ํ์ธํด๋ดค๋๋ ์ง์ญ ์ค์ ์ด ๋ง์ง ์๋ ๊ฒฝ์ฐ๊ฐ ์์ด
databaseURL์ ๋ฐ๋ก ์ค์ ํด์ฃผ์๋ค.

```
// ์ฌ์ฉํ  ํ์ด์ด๋ฒ ์ด์ค ์๋น์ค ์ฃผ์์ ํด์ ํฉ๋๋ค
//import "firebase/compat/auth";
import "firebase/compat/database";
//import "firebase/compat/firestore";
//import "firebase/compat/functions";
import "firebase/compat/storage";

import firebase from "firebase/compat/app";

// Initialize Firebase
//ํ์ด์ด๋ฒ ์ด์ค ์ฌ์ดํธ์์ ๋ดค๋ ์ฐ๊ฒฐ์ ๋ณด๋ฅผ ์ฌ๊ธฐ์ ๊ฐ์ ธ์ต๋๋ค
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
//์ฌ์ฉ ๋ฐฉ๋ฒ์๋๋ค.
//ํ์ด์ด๋ฒ ์ด์ค ์ฐ๊ฒฐ์ ํน์ ์ค๋ฅ๊ฐ ์์ ๊ฒฝ์ฐ๋ฅผ ๋๋นํ ์ฝ๋๋ก ์์๋๋ฉด ๋ฉ๋๋ค.
if (!firebase.apps.length) {
  firebase.initializeApp(firebaseConfig);
}

export const firebase_db = firebase.database();

```

### Storage

๋ฉ๋ฆฌ ์๋ ํ์ผ ์ ์ฅ์์ ์ด๋ฏธ์ง ๋ฐ ์ฌ์ฉ ํ  ํ์ผ์ ์ฌ๋ ค๋๊ณ , ํ์ํ  ๋๋ง๋ค ๊บผ๋ด ์ฐ๋ ์ฉ๋๋ก ์ฌ์ฉ

```
const ref = firebase_storage.ref("general/main.png");
const url = await ref.getDownloadURL();

```

### Realtime Database

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/til/firebase-screen.png)

#### ๋ฐ์ดํฐ๋ฒ ์ด์ค API

์๋์ ๊ฐ์ด config์ firebase_db๋ฅผ ์ฐ๊ฒฐํ์ฌ "/tip" ์ ref๋ก ๋ฃ๊ณ 
snapshot.value๋ก ๊ฐ์ ๊ฐ์ ธ์จ๋ค.

์ฌ์ฉ๋ฐฉ๋ฒ์ ๊ณต์๋ฌธ์์์ ํ์ธ!!

[firebase API ๐](https://firebase.google.com/docs/reference/rest/database)

```

import { firebase_db } from "../firebaseConfig";

firebase_db
        .ref("/tip")
        .once("value")
        .then((snapshot) => {
          let tip = snapshot.val();
          console.log("MainPage > ํ์ด์ด๋ฒ ์ด์ค์์ ๋ฐ์ดํฐ ๊ฐ์ ธ์์ต๋๋ค!!", tip);

          setState(tip);
          setCateState(tip);
          getLocation();
          setReady(false);
        });
```

## TIL โ

ํ์ด์ด๋ฒ ์ด์ค์ ์คํ ๋ฆฌ์ง, ๋ฐ์ดํฐ๋ฒ ์ด์ค๊ฐ ์ฃผ๋ ํ์ต ๋ด์ฉ์ด์๊ณ ,
weather API ์ ์ฉ๋ ํด๋ณด์๋ค.

expo-constants์ installationId ๊ฐ deprecated ๋์ด
uuid๋ฅผ ์ฌ์ฉํ์ฌ ์์ด๋ ์ค์ ์ ํ์๊ณ ,
์ถํ ๋ก๊ทธ์ธ ๊ธฐ๋ฅ์ด ํ์ํด๋ณด์ธ๋ค.

---

์ฐธ๊ณ  :
[์คํ๋ฅดํ ์ฝ๋ฉํด๋ฝ](https://spartacodingclub.kr/),
[React Naitve](https://reactnative.dev/),
[Firebase](https://firebase.google.com/),
