---
title: "Redux μμνκΈ° π₯"
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
- λ¦¬λμ€
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

# Redux λ¦¬λμ€

: λ¦¬μ‘νΈλ₯Ό μν μ€νμ΄νΈ λ§€λμ§λ¨ΌνΈ ν΄ (λ³΅μ‘ν μ±μμ ν¨μ¨μ , λ¨μν μ±μμ νμμμ)


## Why do we need it? μ νμνκ°?

1. Components have local state, but apps have global state.
2. Sometimes state need to be shared.
3. We need to save the shared state somewhere.
4. Redux == state container

{{< adsense >}}

## Redux is a gloabl state container

1. Ther Redux Store is like a box
2. We go and grab what we need for the container
3. For example, from <Navigation/> we only grab the username

## Stuff to remember

1. The whole state of your app is stored in an object(store)

- state κ° λ³΅μ‘νκ³  μ»€μ§ μ μμ΄μ λ¦¬λμ€λ ν΄λΉ μ€λΈμ νΈλ₯Ό μμ νλ κ²μ λ§€μ° μκ²©ν¨

2. If you wanna change the data inside of this object you need to 'dispatch' (sned) an action

- μ€λΈμ νΈμ λ°μ΄ν°λ₯Ό μμ νλ λ°©λ²μ μ‘μμ reducer λ‘ λ³΄λ΄λ©΄ κ°λ₯ν¨

3. You will send this actions to a reducer and this reducer will change the object for you.

- reducer λ μ¬μ©μλ₯Ό λμ ν΄ μ€λΈμ νΈλ₯Ό λ³κ²½ν¨

## nomad coders κ°μ μ°Έκ³ 

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcHDrNY%2FbtqBj7qvixo%2F7v1KBOdkIY4qRBjc6nfJ71%2Fimg.png)  
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcbK0Hs%2FbtqBkORASii%2FXtpfQnFr350NVbxPLROkKk%2Fimg.png)  
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcpbYf2%2FbtqBlAL5ZnQ%2FGl0EAqb3RHjVNi02JFBowk%2Fimg.png)  
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fcesk1G%2FbtqBliZbOXp%2FUcJ2YGUkU2tjOSt8qMasHk%2Fimg.png)  
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fto8YW%2FbtqBmVJcpaU%2FbEJjaAuE7eRGMSeVVrueW0%2Fimg.png)  
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FzNcAV%2FbtqBow90IEF%2F9H84txIYKAZP03Uy0m9GLk%2Fimg.png)  
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcHaK9p%2FbtqBn91wblp%2FIFC3Cy2BAolK5gWFKuMaCk%2Fimg.png)


μ°Έκ³  : 
[https://haneullee.tistory.com/4?category=689534](https://haneullee.tistory.com/4?category=689534)