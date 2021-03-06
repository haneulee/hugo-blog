---
title: "TILð ì±ê°ë° ì¤í°ë - 2 week"
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
  - ì¤íë¥´íì½ë©
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

# TILð ì±ê°ë° ì¤í°ë - 2 week

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/til/til.png)

## Expo ì¤ì¹ ð

**Expo ë?**

{{< alert info >}}
expoë ë¦¬ì¡í¸ ë¤ì´í°ë¸ë¥¼ í¬ë¡ì¤ íë«í¼ì¼ë¡ ê°ë°íê¸° ìí ë¹ëëêµ¬
ë¤ì´í°ë¸ ëª¨ëì ë³´ë¤ ì½ê³  í¸íê² ì¬ì©í  ì ìì¼ë©° ë¹ ë¥´ê² ì¤ì  ê¸°ê¸°ìì íì¤í¸í´ë³¼ ì ìëë¡ í´ì£¼ë íì¤í¸ íµí© íê²½
{{< /alert >}}

```
npm install -g expo-cli // expo ì¤ì¹ (npm)
yarn -global add expo-cli // expo ì¤ì¹ (yarn)

expo init [íë¡ì í¸ ì´ë¦] // íë¡ì í¸ ìì±
expo start // ì¤í
```

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/til/expo-install-1.png)

---

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/til/expo-install-2.png)

## React Native ð¤

React Native is like React, but it uses native components instead of web components as building blocks. So to understand the basic structure of a React Native app, you need to understand some of the basic React concepts, like JSX, components, state, and props. If you already know React, you still need to learn some React-Native-specific stuff, like the native components. This tutorial is aimed at all audiences, whether you have React experience or not.

### React Native ì¥ë¨ì  ð

#### ì¥ì 

- ë¤ì´í°ë¸ì ë¹êµí´ ìë±í ë¹ ë¥¸ ìì°ì±. ì²´ê°ì¼ë¡  3~4ë°°
- UI ë± í¨í¤ì§ 40ì¬ê°
- ë¼ì´ë¸ ë¦¬ë¡ë©
- ì½ë í¸ì
- ê°í¸í ë¬¸ë²

#### ë¨ì 

- ì´ê¸° í¼í¬ë¨¼ì¤ë ì¢ì§ë§ ë·° ì¤íì´ ìì¼ìë¡ ëë ¤ì§
- ë¹ì§ëì¤ ë¡ì§ì´ ë³µì¡íë©´ ëë ¤ì§
- ë¤ì´í°ë¸ ë·° <-> JS ë¡ì§ê° ìíµì´ ë§ì¼ë©´ ëë ¤ì§
- ë¯¸ë¬í UI ì ì´ì ëì
- ì¨ëíí° SDK íì¬ ì ì½

### React Native Components

#### View

- The most fundamental component for building a UI, View is a container that supports layout with flexbox, style, some touch handling, and accessibility controls.
- div íê·¸ì ë¹ì·

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
- ì»¨íì¸ ê° ëì³¤ì ë ì¤í¬ë¡¤ì ìì±íê³  ê°ë ¤ì§ë ë¶ë¶ì ë³´ì¬ì¤
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

## TIL â

react native ë¡ ì¤ì  ë©ì¸ íì´ì§ë¥¼ ë§ëë ììì ì§í
ê¸°ë³¸ì ì¸ ì»´í¬ëí¸ë¤ ì¬ì© ì°ìµ ë° íì¤í¸í¨ !
ë¼ì°íì ì¬ì©í´ ë¤ìí íì´ì§ ë ì´ìì êµ¬ì±ì í´ë´ì¼ í  ê² ê°ë¤.

ì°¸ê³  :
[ì¤íë¥´í ì½ë©í´ë½](https://spartacodingclub.kr/),
[React Naitve](https://reactnative.dev/),
[RN vs Native vs Flutter ë¹êµ](https://yozm.wishket.com/magazine/detail/567/)
