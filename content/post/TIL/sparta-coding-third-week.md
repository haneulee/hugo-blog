---
title: "TIL📚 앱개발 스터디 - 3 week"
date: 2021-12-25T00:07:10+09:00
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

<!--adsense-->

# TIL📚 앱개발 스터디 - 3 week

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/til/til.png)

## React Navigation 🔥

{{< alert info >}}
react native 앱의 네비게이션 기능과 히스토리를 간단히 관리할 수 있는 라이브러리
{{< /alert >}}

### 설치

```
yarn add @react-navigation/native
yarn add @react-navigation/stack

expo install react-native-gesture-handler react-native-reanimated react-native-screens react-native-safe-area-context @react-native-community/masked-view
```

### Stack Navigator 📑

스택 네비게이션은 컴포넌트에 페이지 기능을 부여해주고
컴포넌트에서 컴포넌트로 이동, 즉 페이지 이동을 가능하게 해준다.

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/til/stack-navigator.png)

```
<Stack.Navigator
            screenOptions={{
                headerStyle: {
                    backgroundColor: "black",
                    borderBottomColor: "black",
                    shadowColor: "black",
                    height:100
                },
                //헤더의 텍스트를 왼쪾에 둘지 가운데에 둘지를 결정
                headerTintColor: "#fff",
                headerBackTitleVisible: false
            }}
        >

            {/* name에 해당 하는 부분이 페이지의 타이틀이 됩니다.*/}
            <Stack.Screen name="MainPage" component={MainPage}/>
            <Stack.Screen name="DetailPage" component={DetailPage}/>
        </Stack.Navigator>
```

### 페이지 이동

```
//해당 페이지의 제목을 설정할 수 있음
navigation.setOptions({
   title:'나만의 꿀팁'
})

//Stack.screen에서 name 속성으로 정해준 이름을 지정해주면 해당 페이지로 이동하는 함수
navigation.navigate("DetailPage")

//name 속성을 전달해주고, 두 번째 인자로 딕셔너리 데이터를 전달해주면, Detail 페이지에서
//두번째 인자로 전달된 딕셔너리 데이터를 route 딕셔너리로 로 받을 수 있음
navigation.navigate("DetailPage",{
  title: title
})
```

## 공유하기 (Share Contents) 👉

```
import { Share } from 'react-native';

Share.share({
            message:`${tip.title} \n\n ${tip.desc} \n\n ${tip.image}`,
        });
```

## 외부 링크 연결 (Open Link) 🔗

### 설치

```
expo install expo-linking
```

### 사용

```
import * as Linking from 'expo-linking';

Linking.openURL("https://spartacodingclub.kr")
```

## 상단 status bar

### 설치

```
expo install expo-status-bar
```

### 사용

```
import { StatusBar } from 'expo-status-bar';

<StatusBar style="black" />
```

## TIL ✅

리액트 네이티브에서 페이지 전환에 사용되는 리액트 네비게이션을 학습했다.
특히 스택 네비게이터를 이용해 페이지 이동을 구현했고,
이 외에도 탭 네비게이터도 많이 사용한다.

expo에서 제공하는 기능 중,
외부 링크 연결, 상단 status bar를 컨트롤할 수 있다.
RN에서 제공하는 share 도 마찬가지!

보통 expo로 개발하면 편하지만 ios/android를 따로 설정하기 어렵기 때문에
커스텀하게 사용하려면 react native cli로 설치하면 된다.

---

참고 :
[스파르타 코딩클럽](https://spartacodingclub.kr/),
[React Naitve](https://reactnative.dev/),
[React Navigation](https://reactnavigation.org/),
[Expo API](https://docs.expo.dev/versions/latest/?redirected),
[Expo status bar](https://docs.expo.io/versions/latest/sdk/status-bar/)
