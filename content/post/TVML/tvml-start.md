---
title: "TVML for Apple TV"
date: 2021-05-20T10:52:18+09:00
categories: 
- development
- TVML
tags: 
- development
- front-end
- TVML
- appletv
- 애플티비
- swift
- ios
- tvos
keywords: 
- development
- front-end
cover: ""
draft: false
thumbnailImagePosition: left
thumbnailImage: ""
# coverImage: //d1u9biwaxjngwg.cloudfront.net/cover-image-showcase/city.jpg
metaAlignment: center
coverMeta: out
---

# TVML (Television Markup Language)

앱의 뷰를 정의한 XML의 형태, TV용 클라이언트-서버 랩의 인터페이스를 만듬

자바스크립트 API를 통해 전체 클라이언트와 서버를 만들수 있는 TVJS와 함께 결합한다.

기본적으로 애플TV 앱은 iOS와 유사하게 개발할 수 있다. 더불어 클라이언트-서버 앱을 개발하도록 했다. 개발자는 자바스크립트, DOM, HTTPS, XMLHTTPRequst 같은 웹 기술을 사용할 수 있다.



- TVMLJS :  TVML 페이지를 읽을 때 사용되는 자바스크립트 API

- TVMLKit : 앱에서 자바스크립트와 TVML 요소를 통합하는 수단 (네이티브와 자바스크립트/TVML 코드를 연결)

- TVServices : 사용자의 앱 아이콘 선택 시 상세정보를 노출하도록 만드는 프레임워크



## 장점 :

TVML 애플리케이션은 공통 기능 / 사용자 인터페이스를 사용하여 표준 애플리케이션을 보다 쉽고 빠르게 구축 할 수 있다.

TVML 템플릿은 Netflix TV 앱이나 HBO GO 또는 iTunes에서 사용하고 설계 시간이 크게 줄어 든다.

JavaScript 경험이 거의 없어도 템플릿을 구현하기가 매우 쉽다. 자동 레이아웃 처리가 되고 lazy image loading이 자동으로 되며 화면에서 모든 UI 요소의 동작은 이미 Apple에서 처리한다.

템플릿은 구조화되었지만 customize 할 수 있다. 템플릿은 플러그 앤 플레이 이지만 UI 부분적 요소를 customize 할 수 있다.

웹 서버에서 TVML / TVJS 파일을 호스팅 할 수 있어 앱이 업데이트되면 사용자가 다운로드하지 않고도 앱을 변경할 수 있다.

TVML을 customize된 UIKit과 사용할 수 있다. (How To Mix UIKit and TVML Within One App)



JavaScript 및 TVML을 사용하는 클라이언트-서버 앱은 기존 앱과 약간 다르다.

Xcode에서 생성 한 프로젝트의 주요 기능은 메인 JavaScript 파일에 액세스하여 TVML 파일에서 생성 된 페이지를 화면에 표시한다.



기본적으로 애플TV 앱은 iOS와 유사하게 개발할 수 있다.

더불어 클라이언트-서버 앱을 개발하도록 했다.

개발자는 자바스크립트, DOM, HTTPS, XMLHTTPRequst 같은 웹 기술을 사용할 수 있다.

애플은 TV용 클라이언트-서버 랩의 인터페이스를 만드는 TVML(Television Markup Language)이란 표시언어를 제공한다.

TVML 문서는 자바스크립트를 사용한다.

TVML킷 프레임워크는 네이티브 코드와 자바스크립트 및 TVML 코드 사이의 가교를 제공한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FwnAC2%2FbtqTjDSw0yM%2FwMuRK6MZPjPJ9V9ZqdYlM0%2Fimg.jpg)

**TVOS 클라이언트-서버 앱 모델**

iOS의 패럴랙스 이미지 기능도 활용할 수 있다. UIKit을 사용해 패럴랙스 효과 적용을 일정부분 자동화할 수 있다.

TVOS 프레임워크는 iOS에 없는 새 프레임워크를 갖고 있다. 일단 TVMLJS로 TVML 페이지를 읽을 때 사용되는 자바스크립트 API다. TVMLKit은 앱에서 자바스크립트와 TVML 요소를 통합하는 수단이다. TVServices는 사용자의 앱 아이콘 선택 시 상세정보를 노출하도록 만드는 프레임워크다.


참고 
[www.raywenderlich.com/1579-beginning-tvos-development-with-tvml-tutorial](https://www.raywenderlich.com/1579-beginning-tvos-development-with-tvml-tutorial)


# TVos App 개발 시, native language와 tvml 비교


1. 인터페이스
   1. 버튼 하나만 눌러 화면을 보는 대신 인터페이스를 자주 사용하는 앱을 만들려면 native 가 더 괜찮다. 그러나 앱에서 비디오 콘텐츠를 스트리밍하려는 경우 TVML만 있으면 된다.
2. 개발언어
   1. native language가 익숙한 ios 개발자면 swift나 object-c로 개발하면 되나 이를 모르면 tvml로 개발하면 된다.
3. 개발기간
   1. 스트리밍 비디오 앱을 만들려는 경우 TVML로 개발할 경우 시간을 절약 할 수 있다
4. customizing
   1. 복잡하게 구성된 UI 의 경우 customize 하는 데 있어 native language가 더 나을 수 있다.


## 고려해야 할 사항


1. 리모컨 컨트롤 이벤트 트리거
2. 애플 tv의 앱 사이즈 제한
   1. 200 Mb 이하
3. 외부 저장소
   1. 새로운 OS 용으로 개발된 앱에는 외부 저장소가 없어서 자체 데이터베이스 시스템 또는 iCloud Kit를 사용해야 한다.
4. 웹뷰가 없음


{{< alert info >}}
기본 iOS 및 TVML 애플리케이션 모두 뛰어난 장단점이 없다. 주요 차이점은 프로그래밍에 대한 특정 접근 방식이 응용 프로그램의 특성에 따라 다소 적합 할 수 있다는 것이다. 사용자 인터페이스와 적극적으로 상호 작용해야하는 경우 native 앱을 선택해야 한다. TVML 앱은 사용자가 인터페이스를 조금만 사용하려는 경우 (예 : 영화 및 TV 프로그램 시청)에 더 적합하다. 
{{< /alert >}}

