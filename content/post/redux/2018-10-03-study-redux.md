---
title: "Redux 시작하기 🔥"
date: 2018-10-03 11:03:00 +0900
categories:
  - development
  - Redux
tags:
  - development
  - front-end
  - javascript
  - react
  - Redux
  - 리덕스
keywords:
  - development
  - front-end
cover: ""
draft: false
thumbnailImagePosition: left
thumbnailImage: "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcHDrNY%2FbtqBj7qvixo%2F7v1KBOdkIY4qRBjc6nfJ71%2Fimg.png"
# coverImage: //d1u9biwaxjngwg.cloudfront.net/cover-image-showcase/city.jpg
metaAlignment: center
coverMeta: out
---

<!--toc-->

# Redux 리덕스

: 리액트를 위한 스테이트 매니지먼트 툴 (복잡한 앱에서 효율적, 단순한 앱에서 필요없음)

## Why do we need it? 왜 필요한가?

1. Components have local state, but apps have global state.
2. Sometimes state need to be shared.
3. We need to save the shared state somewhere.
4. Redux == state container

<!--adsense-->

## Redux is a gloabl state container

1. Ther Redux Store is like a box
2. We go and grab what we need for the container
3. For example, from <Navigation/> we only grab the username

## Stuff to remember

1. The whole state of your app is stored in an object(store)

- state 가 복잡하고 커질 수 있어서 리덕스는 해당 오브젝트를 수정하는 것에 매우 엄격함

2. If you wanna change the data inside of this object you need to 'dispatch' (sned) an action

- 오브젝트의 데이터를 수정하는 방법은 액션을 reducer 로 보내면 가능함

3. You will send this actions to a reducer and this reducer will change the object for you.

- reducer 는 사용자를 대신해 오브젝트를 변경함

## nomad coders 강의 참고

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcHDrNY%2FbtqBj7qvixo%2F7v1KBOdkIY4qRBjc6nfJ71%2Fimg.png)  
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcbK0Hs%2FbtqBkORASii%2FXtpfQnFr350NVbxPLROkKk%2Fimg.png)  
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcpbYf2%2FbtqBlAL5ZnQ%2FGl0EAqb3RHjVNi02JFBowk%2Fimg.png)  
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fcesk1G%2FbtqBliZbOXp%2FUcJ2YGUkU2tjOSt8qMasHk%2Fimg.png)  
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fto8YW%2FbtqBmVJcpaU%2FbEJjaAuE7eRGMSeVVrueW0%2Fimg.png)  
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FzNcAV%2FbtqBow90IEF%2F9H84txIYKAZP03Uy0m9GLk%2Fimg.png)  
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcHaK9p%2FbtqBn91wblp%2FIFC3Cy2BAolK5gWFKuMaCk%2Fimg.png)

참고 :
[https://haneullee.tistory.com/4?category=689534](https://haneullee.tistory.com/4?category=689534)
