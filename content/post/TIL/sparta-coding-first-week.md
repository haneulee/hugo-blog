---
title: "TIL📚 앱개발 스터디 - 1week"
date: 2021-12-11T10:46:28+09:00
categories:
  - development
tags:
  - development
  - front-end
  - react-native
  - javascript
  - til
  - sparta
  - coding
  - 스파르타코딩
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

# TIL📚 앱개발 스터디 - 1week

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/til/til.png)

## Javascript

### Object Oriented Programming

1. 상속 : 클래스개념에서 상위 클래스(부모)로 부터 하위 클래스(자식)이 유산을 물려받는것과 같이, 부모의 메소드나 변수를 사용할 수 있는 것을 말함.

2. 다형성 : 같은 함수가 있다고 칠대 그 함수가 매개변수에 따라 다른 역할을 할 수 도 있다.

3. 캡슐화 : 보통 데이터를 은닉시킨다고 표현하는데, 외부에서 쉽게 데이터를 접근할 수 없게 만들기도하고, 데이터 구조와 데이터를 다루는 방법들을 한데다 묶는것.

4. 추상화 : 공통적인 속성이나 기능을 묶어서 이름을 붙이는 것 ( a b d 이런게있다고 치면 이런건 알파벳이라고 묶을 수 있다)

**OOP와 함수형 프로그래밍의 가장 큰 차이점은 무엇인가**

객체지향은 객체 안에 상태를 저장하고, 이 상태를 이용해서 메소드를 추가하고 상태변화를 설정하고 조정하기위해 다양한 기능을 사용한다.

이에 반해 함수형 프로그래밍은 상태를 제어하는것보다 상태를 저장하지 않고 없애는데 주력한다. 예를들면, 객체 지향은 상태를 저장하는 필드와 그 필드들을 이용해 기능을 제공하는 메소드를 만들고 클래스를 만듭니다. 반면 함수형은 몇몇 자료구조(list, map, set) 등을 이용해 최적화된 동작을 만들어낸다.

### 데이터 타입

- 기본형 : 값을 그대로 할당 / 불변적 ⭕️

- Number / String / Boolean / null / undefined

- 참조형 : 값이 지정된 주소값을 할당 / 불변적 ❌

- Object / Array / Map

### 변수 선언

- var : 재선언 ⭕️ / 호이스팅

- 선언과 초기화가 한번에 일어남 (undefined 로 초기화)

- let (es6) : 재선언 ❌ / 재할당 ⭕️/ 호이스팅

- 선언과 초기화가 따로 발생 > 변수 초기화가 안된 상태에서 참조하면 에러

- const (es6) : 재선언 ❌ / 재할당 ❌

### 화살표 함수

- function과 달리 함수를 선언할 때 this에 바인딩할 객체가 정적으로 결정된다.

- 상위스코프의 this를 가리킴 (lexical this)

- this가 window객체를 가리키지 않게 조심해야함!

- call/apply/bind로 this 변경 불가능

### Array.prototype.map()

{{< alert info >}}
arr.map(callback(currentValue[, index[, array]])[, thisArg])
{{< /alert >}}

```
const array1 = [1, 4, 9, 16];

// pass a function to map
const map1 = array1.map(x => x * 2);

console.log(map1);
// expected output: Array [2, 8, 18, 32]

map은 callback 함수를 각각의 요소에 대해 한번씩 순서대로 불러 그 함수의 반환값으로 새로운 배열을 만듭니다. callback 함수는 (undefined도 포함해서) 배열 값이 들어있는 인덱스에 대해서만 호출됩니다. 즉, 값이 삭제되거나 아직 값이 할당/정의되지 않은 인덱스에 대해서는 호출되지 않습니다.

callback 함수는 호출될 때 대상 요소의 값, 그 요소의 인덱스, 그리고 map을 호출한 원본 배열 3개의 인수를 전달받습니다.

thisArg 매개변수가 map에 전달된 경우 callback 함수의 this값으로 사용됩니다. 그 외의 경우 undefined값이 this 값으로 사용됩니다. callback 함수에서 최종적으로 볼 수 있는 this 값은  함수 내 this를 정하는 일반적인 규칙에 따라 결정됩니다.



## TIL

전반적으로 자바스크립트 기초에 대한 학습이었고, 개인적으로는 skip 해도 될만한 정도의 수준이었다.
다음 react native 학습을 기대해야겠다. 👏


```

참고 :
[스파르타코딩클럽](https://spartacodingclub.kr/)
[Javascript MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Grammar_and_types)
