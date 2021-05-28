---
title: "XCODE TVML app"
date: 2021-05-21T10:20:38+09:00
categories: 
- development
- TVML
tags: 
- development
- front-end
- swift
- tvml
- tvos
- xcode
- 스위프트
keywords: 
- development
- front-end
cover: ""
draft: false
thumbnailImagePosition: left
thumbnailImage: "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcysiXz%2FbtqUl9XiOJr%2FOK52muaNh5GmEIVvkWHgOk%2Fimg.png"
# coverImage: //d1u9biwaxjngwg.cloudfront.net/cover-image-showcase/city.jpg
metaAlignment: center
coverMeta: out
---

xcode에서 tvml 샘플 앱을 만들어 테스트 해보기 

### STEP 1.

xcode 설치 

[developer.apple.com/xcode/downloads/](https://developer.apple.com/xcode/downloads/)


### STEP 2.

xcode 를 열고, create new project 를 통해 tvOS 탭에서 TVML App 을 선택 후 next 버튼을 누른다. 

다음 product name과 language 등을 선택한다. 

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcsN4SB%2FbtqUnJDJxcZ%2FEIZsfYW5I4TsNJMCXnh3ek%2Fimg.png)

### STEP 3.

터미널을 통해 해당 프로젝트 디렉토리로 가서 웹서버를 실행한다. 

맥은 기본적으로 python이 설치 되어 있으므로

python -m SimpleHTTPServer 9001

또는 

ruby -run -ehttpd . -p9001

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FmcRCi%2FbtqUf0fIhiI%2Fd5BoQBsVlRIjiJHZKH0dvk%2Fimg.png)

### STEP 4.

시뮬레이터를 apple tv 4k 로 선택한 후, 

상단 왼쪽의 play 버튼을 클릭하면 빌드가 실행된다. 

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FAHQpy%2FbtqUmIrxrA1%2Fg1c4J4HKr06vvSzfewpGv1%2Fimg.png)

### ERROR 

처음 실행하면 도메인 관련 오류가 발생한다. 

웹서버를 로컬로 돌려서 http 보안 오류가 발생하였기 때문에 해당 라인을 추가하고 YES 로 바꿔준다. 

다시 play 버튼을 눌러서 실행하면 완료!

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fnmeyh%2FbtqUk0fdHQE%2FGZ0NYKckk3xKe8yakfKwZk%2Fimg.png)
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcysiXz%2FbtqUl9XiOJr%2FOK52muaNh5GmEIVvkWHgOk%2Fimg.png)


{{< adsense >}}