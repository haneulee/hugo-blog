---
title: "리액트 useState 훅 사용하기"
date: 2021-05-18T12:30:09+09:00
categories: 
- development
- react
tags: 
- development
- front-end
keywords: 
- development
- front-end
- react
- 리액트
- useState
- hook
- 훅
cover: ""
draft: false
thumbnailImage: ""
# coverImage: //d1u9biwaxjngwg.cloudfront.net/cover-image-showcase/city.jpg
metaAlignment: center
coverMeta: out
---

## 배열 state 

#### 1\. 추가

```
const [language, setLanguage] = useState([]);

setLanguage([...language, newLanguage]);
// or

setLanguage(language.concat(newLanguage));
```

#### 2\. 삭제

```
const [language, setLanguage] = useState([]);

setLanguage(language.filter(item => item.id !== id));
```

#### 3\. 수정

```
const [language, setLanguage] = useState([]);

setLanguage(
      language.map(item =>
        item.id === id ? { ...item, active: !item.active } : item
      )
    );
```