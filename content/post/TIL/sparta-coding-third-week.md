---
title: "TILð ì±ê°ë° ì¤í°ë - 3 week"
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

# TILð ì±ê°ë° ì¤í°ë - 3 week

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/til/til.png)

## React Navigation ð¥

{{< alert info >}}
react native ì±ì ë¤ë¹ê²ì´ì ê¸°ë¥ê³¼ íì¤í ë¦¬ë¥¼ ê°ë¨í ê´ë¦¬í  ì ìë ë¼ì´ë¸ë¬ë¦¬
{{< /alert >}}

### ì¤ì¹

```
yarn add @react-navigation/native
yarn add @react-navigation/stack

expo install react-native-gesture-handler react-native-reanimated react-native-screens react-native-safe-area-context @react-native-community/masked-view
```

### Stack Navigator ð

ì¤í ë¤ë¹ê²ì´ìì ì»´í¬ëí¸ì íì´ì§ ê¸°ë¥ì ë¶ì¬í´ì£¼ê³ 
ì»´í¬ëí¸ìì ì»´í¬ëí¸ë¡ ì´ë, ì¦ íì´ì§ ì´ëì ê°ë¥íê² í´ì¤ë¤.

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
                //í¤ëì íì¤í¸ë¥¼ ì¼ìª¾ì ëì§ ê°ì´ë°ì ëì§ë¥¼ ê²°ì 
                headerTintColor: "#fff",
                headerBackTitleVisible: false
            }}
        >

            {/* nameì í´ë¹ íë ë¶ë¶ì´ íì´ì§ì íì´íì´ ë©ëë¤.*/}
            <Stack.Screen name="MainPage" component={MainPage}/>
            <Stack.Screen name="DetailPage" component={DetailPage}/>
        </Stack.Navigator>
```

### íì´ì§ ì´ë

```
//í´ë¹ íì´ì§ì ì ëª©ì ì¤ì í  ì ìì
navigation.setOptions({
   title:'ëë§ì ê¿í'
})

//Stack.screenìì name ìì±ì¼ë¡ ì í´ì¤ ì´ë¦ì ì§ì í´ì£¼ë©´ í´ë¹ íì´ì§ë¡ ì´ëíë í¨ì
navigation.navigate("DetailPage")

//name ìì±ì ì ë¬í´ì£¼ê³ , ë ë²ì§¸ ì¸ìë¡ ëìëë¦¬ ë°ì´í°ë¥¼ ì ë¬í´ì£¼ë©´, Detail íì´ì§ìì
//ëë²ì§¸ ì¸ìë¡ ì ë¬ë ëìëë¦¬ ë°ì´í°ë¥¼ route ëìëë¦¬ë¡ ë¡ ë°ì ì ìì
navigation.navigate("DetailPage",{
  title: title
})
```

## ê³µì íê¸° (Share Contents) ð

```
import { Share } from 'react-native';

Share.share({
            message:`${tip.title} \n\n ${tip.desc} \n\n ${tip.image}`,
        });
```

## ì¸ë¶ ë§í¬ ì°ê²° (Open Link) ð

### ì¤ì¹

```
expo install expo-linking
```

### ì¬ì©

```
import * as Linking from 'expo-linking';

Linking.openURL("https://spartacodingclub.kr")
```

## ìë¨ status bar

### ì¤ì¹

```
expo install expo-status-bar
```

### ì¬ì©

```
import { StatusBar } from 'expo-status-bar';

<StatusBar style="black" />
```

## TIL â

ë¦¬ì¡í¸ ë¤ì´í°ë¸ìì íì´ì§ ì íì ì¬ì©ëë ë¦¬ì¡í¸ ë¤ë¹ê²ì´ìì íìµíë¤.
í¹í ì¤í ë¤ë¹ê²ì´í°ë¥¼ ì´ì©í´ íì´ì§ ì´ëì êµ¬ííê³ ,
ì´ ì¸ìë í­ ë¤ë¹ê²ì´í°ë ë§ì´ ì¬ì©íë¤.

expoìì ì ê³µíë ê¸°ë¥ ì¤,
ì¸ë¶ ë§í¬ ì°ê²°, ìë¨ status barë¥¼ ì»¨í¸ë¡¤í  ì ìë¤.
RNìì ì ê³µíë share ë ë§ì°¬ê°ì§!

ë³´íµ expoë¡ ê°ë°íë©´ í¸íì§ë§ ios/androidë¥¼ ë°ë¡ ì¤ì íê¸° ì´ë µê¸° ëë¬¸ì
ì»¤ì¤ííê² ì¬ì©íë ¤ë©´ react native clië¡ ì¤ì¹íë©´ ëë¤.

---

ì°¸ê³  :
[ì¤íë¥´í ì½ë©í´ë½](https://spartacodingclub.kr/),
[React Naitve](https://reactnative.dev/),
[React Navigation](https://reactnavigation.org/),
[Expo API](https://docs.expo.dev/versions/latest/?redirected),
[Expo status bar](https://docs.expo.io/versions/latest/sdk/status-bar/)
