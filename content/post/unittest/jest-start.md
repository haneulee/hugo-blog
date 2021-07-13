---
title: "Jest 유닛 테스트 - 소개"
date: 2021-07-09T11:06:17+09:00
categories:
  - development
tags:
  - development
  - front-end
  - unittest
  - jest
  - javascript
  - facebook
  - react
  - nextjs
  - 테스트주도개발
  - 제스트
  - TDD
  - 페이스북
  - 단위테스트
keywords:
  - development
  - front-end
cover: ""
thumbnailImagePosition: left
thumbnailImage: https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/unittest/img-jest.png
# coverImage: //https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/hugo/github-site.png
metaAlignment: center
coverMeta: out
draft: false
---

<!--toc-->

# Jest

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/unittest/img-jest.png)

## Jest 란 ? 🤔

{{< hl-text yellow >}}
Jest는 Facebook에서 개발한 JavaScript 테스팅 프레임워크이다.
Babel , TypeScript , Node , React , Angular , Vue 등을 사용하는 프로젝트에서 사용할 수 있다.
Test runner와 Test Mathcher, Test Mock 프레임워크까지 제공하여 다른 유닛 테스트 프레임워크보다 편하다.
{{< /hl-text >}}

## 테스트 주도 개발 (TDD)

- 짧은 개발 사이클을 반복하는 소프트웨어 개발 프로세스 중 하나
- 새로운 함수를 정의하는 자동화된 테스트 케이스를 작성한다.
- 그 케이스를 통과하기 위한 최소한의 코드를 생성한다.
- 새 코드를 표준에 맞도록 리팩토링한다.

### 장점

1. 객체지향적인 코드 개발
2. 설계 수정 시간의 단축
3. 디버깅 시간 단축
4. 유지보수 용이성
5. 테스트 문서 대체 가능

## Jest 설치

```
yarn add --dev jest
npm install --save-dev jest
```

{{< adsense >}}

## Jest 설정

> 설정
> moduleNameMapper - 경로 설정 가능
> coveragePathIgnorePatterns - 테스트를 제외할 파일 명시

```json
> package.json

"jest": {
    "moduleFileExtensions": [
      "js",
      "json",
      "ts"
    ],
    "moduleNameMapper": {
      "^src/(.*)$": "<rootDir>/$1"
    },
    "rootDir": "src",
    "testRegex": ".*\\.spec\\.ts$",
    "transform": {
      "^.+\\.(t|j)s$": "ts-jest"
    },
    "collectCoverageFrom": [
      "**/*.service.ts"
    ],
    "coverageDirectory": "../coverage",
    "testEnvironment": "node",
    "coveragePathIgnorePatterns": [
      "node_modules",
      ".entity.ts",
      ".constants.ts"
    ]
  },
```

## Jest 사용 방법

### mocking

mocking은 단위 테스트를 작성할 때, 해당 코드가 의존하는 부분을 가짜(mock)로 대체하는 기법

### mock function

#### jest.fn()

- Returns a new, unused mock function. Optionally takes a mock implementation.

```js
const mockFn = jest.fn();
mockFn();
expect(mockFn).toHaveBeenCalled();

// With a mock implementation:
const returnsTrue = jest.fn(() => true);
console.log(returnsTrue()); // true;
```

#### jest.spyOn()

- Creates a mock function similar to jest.fn but also tracks calls to object[methodName]. Returns a Jest mock function.

Note: By default, jest.spyOn also calls the spied method. This is different behavior from most other test libraries. If you want to overwrite the original function, you can use jest.spyOn(object, methodName).mockImplementation(() => customImplementation) or object[methodName] = jest.fn(() => customImplementation);

```js
const video = require("./video");

test("plays video", () => {
  const spy = jest.spyOn(video, "play");
  const isPlaying = video.play();

  expect(spy).toHaveBeenCalled();
  expect(isPlaying).toBe(true);

  spy.mockRestore();
});
```

---

참고 :
[jset 공식문서](https://jestjs.io/docs/api),
[jset mocking](https://www.daleseo.com/jest-fn-spy-on/),
