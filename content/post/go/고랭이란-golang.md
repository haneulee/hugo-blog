---
title: "고랭이란 Golang "
date: 2022-10-05T21:36:47+02:00
categories:
  - development
tags:
  - development
  - front-end
  - 고랭이란 Golang
  - golang
  - google
  - concurrency
  - back-end
  - goroutine
keywords:
  - development
  - front-end
cover: ""
thumbnailImagePosition: left
thumbnailImage: "https://go.dev/images/go_google_case_study_carousel.png"
# coverImage: //https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/hugo/github-site.png
metaAlignment: center
coverMeta: out
draft: false
---

<!--toc-->

![](https://go.dev/images/go_google_case_study_carousel.png)

# 고랭이란? What is Golang?

{{< alert info >}}
2009 년 구글에서 발표한 프로그래밍 언어.  
로버트 그리즈머, 롭 파이크, 케네스 톰슨이 C++의 복잡함이 싫어서 Go를 만들었다.  
Go 언어 사용자들을 Gopher 라고 함  
{{< /alert >}}

<!--adsense-->

## 특징

- 정적 타입 : 자료형에 형이 정해져 있음
- 강타입 : 자료형 변환(타입캐스팅)이 항상 명시되어야 함
- 안전성 : 타입 안전성과 메모리 안전성
- 병행성 : 스레드를 한 단계 더 추상화한 '고루틴'이라는 개념 사용
- 가비지 컬렉션 : 결과물에 go runtime이 내장되는데 go run time이 메모리를 핸들링
- 컴파일 언어 : 인터프리터 언어가 아니지만 근접한 수준의 빠른 컴파일
  포인터는 존재, 하지만 포인터 연산은 없음

## 장점 & 단점

### 장점

1. 진입장벽이 낮다.
2. 다양한 라이브러리 사용 가능
3. 이동 효율성 - 명령 컴파일 및 실행 속도가 빠르다
4. 고루틴은 매우 가벼움
5. 백엔드와 통합이 쉽다.
6. 동시성 (concurrency) - 다중 스레딩 기능

### 단점

1. 에러처리가 힘들다
2. 제네릭이 없었으나 현재 지원함
3. 생산성이 약함
4. 바이트코드를 생성하는 언어가 아니므로 바이너리만 배포할 경우 각각 컴파일 해야함
5. 현대 프로그래밍 언어의 성과를 무시한 언어설계?.. 라는 말도 있다.

## 동시성 concurrency

프로그램을 여러 독립된 작은 단위로 나누고 주어진 자원을 사용해 빠르게 동시다발적으로 수행

## 고루틴 goroutine

비동기 메커니즘으로 각각의 고루틴은 병렬로 동작하며 메시지 채널을 통해 값을 주고 받는다.  
고루틴을 사용하면 이벤트 처리, 병렬 프로그래밍이 간단해짐  
멀티스레드이지만 스케줄러에 의해 관리되는 경량 스레드여서 CPU 코어수와 무관하게 아무리 많은 고루틴을 작성해도 성능에 문제가 없다.

## Go 설치

[https://golang.org/dl/](https://golang.org/dl/) 에서 Go 다운로드

```
go version // 고 버전 확인
```

## Go 코드

- [Go 플레이그라운드](https://go.dev/play/)

```
package main

import "fmt"

func main() {
	fmt.Println("Hello, 世界")
}

go run . //고 실행

```

---

참고 :
[https://go.dev/](https://go.dev/),  
[https://namu.wiki/w/Go(%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%20%EC%96%B8%EC%96%B4)](<https://namu.wiki/w/Go(%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%20%EC%96%B8%EC%96%B4)>),
[Go Online Editor](https://replit.com/languages/go)
