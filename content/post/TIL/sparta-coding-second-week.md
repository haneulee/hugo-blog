---
title: "TIL📚 앱개발 스터디 - 2 week"
date: 2021-12-20T12:19:04+09:00
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

# TIL📚 앱개발 스터디 - 2 week

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/til/til.png)

## Expo 설치 👉

**Expo 란?**

{{< alert info >}}
expo는 리액트 네이티브를 크로스 플랫폼으로 개발하기 위한 빌드도구
네이티브 모듈을 보다 쉽고 편하게 사용할 수 있으며 빠르게 실제 기기에서 테스트해볼 수 있도록 해주는 테스트 통합 환경
{{< /alert >}}

```
npm install -g expo-cli // expo 설치 (npm)
yarn -global add expo-cli // expo 설치 (yarn)

expo init [프로젝트 이름] // 프로젝트 생성
expo start // 실행
```

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/til/expo-install-1.png)

---

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/til/expo-install-2.png)

## React Native 🤔

React Native is like React, but it uses native components instead of web components as building blocks. So to understand the basic structure of a React Native app, you need to understand some of the basic React concepts, like JSX, components, state, and props. If you already know React, you still need to learn some React-Native-specific stuff, like the native components. This tutorial is aimed at all audiences, whether you have React experience or not.

### React Native 장단점 👍

#### 장점

- 네이티브와 비교해 월등히 빠른 생산성. 체감으론 3~4배
- UI 등 패키지 40여개
- 라이브 리로딩
- 코드 푸시
- 간편한 문법

#### 단점

- 초기 퍼포먼스는 좋지만 뷰 스택이 쌓일수록 느려짐
- 비지니스 로직이 복잡하면 느려짐
- 네이티브 뷰 <-> JS 로직간 소통이 많으면 느려짐
- 미묘한 UI 의 이상 동작
- 써드파티 SDK 탑재 제약

### React Native Components

#### View

- The most fundamental component for building a UI, View is a container that supports layout with flexbox, style, some touch handling, and accessibility controls.
- div 태그와 비슷

```
import React from "react";
import { View, Text } from "react-native";

const ViewBoxesWithColorAndText = () => {
  return (
    <View
      style={{
        flexDirection: "row",
        height: 100,
        padding: 20
      }}
    >
      <View style={{ backgroundColor: "blue", flex: 0.3 }} />
      <View style={{ backgroundColor: "red", flex: 0.5 }} />
      <Text>Hello World!</Text>
    </View>
  );
};

export default ViewBoxesWithColorAndText;
```

#### Text

- A React component for displaying text.
- Text supports nesting, styling, and touch handling.

```
import React, { useState } from "react";
import { Text, StyleSheet } from "react-native";

const TextInANest = () => {
  const [titleText, setTitleText] = useState("Bird's Nest");
  const bodyText = "This is not really a bird nest.";

  const onPressTitle = () => {
    setTitleText("Bird's Nest [pressed]");
  };

  return (
    <Text style={styles.baseText}>
      <Text style={styles.titleText} onPress={onPressTitle}>
        {titleText}
        {"\n"}
        {"\n"}
      </Text>
      <Text numberOfLines={5}>{bodyText}</Text>
    </Text>
  );
};

const styles = StyleSheet.create({
  baseText: {
    fontFamily: "Cochin"
  },
  titleText: {
    fontSize: 20,
    fontWeight: "bold"
  }
});

export default TextInANest;
```

#### ScrollView

- Component that wraps platform ScrollView while providing integration with touch locking "responder" system.
- 컨텐츠가 넘쳤을 때 스크롤을 생성하고 가려지는 부분을 보여줌
- [https://reactnative.dev/docs/scrollview](https://reactnative.dev/docs/scrollview)

```
import React from 'react';
import { StyleSheet, Text, SafeAreaView, ScrollView, StatusBar } from 'react-native';

const App = () => {
  return (
    <SafeAreaView style={styles.container}>
      <ScrollView style={styles.scrollView}>
        <Text style={styles.text}>
          Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do
          eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad
          minim veniam, quis nostrud exercitation ullamco laboris nisi ut
          aliquip ex ea commodo consequat. Duis aute irure dolor in
          reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla
          pariatur. Excepteur sint occaecat cupidatat non proident, sunt in
          culpa qui officia deserunt mollit anim id est laborum.
        </Text>
      </ScrollView>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    paddingTop: StatusBar.currentHeight,
  },
  scrollView: {
    backgroundColor: 'pink',
    marginHorizontal: 20,
  },
  text: {
    fontSize: 42,
  },
});

export default App;
```

#### TextInput

- A foundational component for inputting text into the app via a keyboard.

```
import React from "react";
import { SafeAreaView, StyleSheet, TextInput } from "react-native";

const UselessTextInput = () => {
  const [text, onChangeText] = React.useState("Useless Text");
  const [number, onChangeNumber] = React.useState(null);

  return (
    <SafeAreaView>
      <TextInput
        style={styles.input}
        onChangeText={onChangeText}
        value={text}
      />
      <TextInput
        style={styles.input}
        onChangeText={onChangeNumber}
        value={number}
        placeholder="useless placeholder"
        keyboardType="numeric"
      />
    </SafeAreaView>
  );
};

const styles = StyleSheet.create({
  input: {
    height: 40,
    margin: 12,
    borderWidth: 1,
    padding: 10,
  },
});

export default UselessTextInput;
```

## TIL ✅

react native 로 실제 메인 페이지를 만드는 작업을 진행
기본적인 컴포넌트들 사용 연습 및 테스트함 !
라우팅을 사용해 다양한 페이지 레이아웃 구성을 해봐야 할 것 같다.

참고 :
[스파르타 코딩클럽](https://spartacodingclub.kr/),
[React Naitve](https://reactnative.dev/),
[RN vs Native vs Flutter 비교](https://yozm.wishket.com/magazine/detail/567/)
