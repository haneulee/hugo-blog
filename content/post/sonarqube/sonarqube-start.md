---
title: "Frontend SonarQube 적용"
date: 2021-05-20T10:46:41+09:00
categories: 
- development
- sonarqube
tags: 
- development
- front-end
- sonarqube
- 소나큐브
- 프론트엔드
- 테스트코드
- 정적분석
- 테스트
- sonarlint
- sonarscanner
keywords: 
- development
- front-end
cover: ""
draft: false
thumbnailImagePosition: left
thumbnailImage: "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F0ULxl%2FbtqS3aaXFqL%2Fgr6OAyBjbKpIbwlaVjtPU0%2Fimg.png"
# coverImage: //d1u9biwaxjngwg.cloudfront.net/cover-image-showcase/city.jpg
metaAlignment: center
coverMeta: out
---
<!--toc-->

이번에 회사에서 개발 코드 정적 분석 툴인 

소나큐브 (sonarqube)를 도입하기로 해서 사전 검토에 들어갔다. 

먼저 현재 개발중인 SKB G2 웹앱 코드를 소나큐브로 돌려보기로 했다. 

해당 웹앱 코드는 vue 프레임워크를 사용중

-----------------------

### 1\. 소나큐브 서버 띄우기


소나큐브는 아래 사이트에서 다운로드 받고, 

소나스캐너는 맥을 이용중이므로 간단하게 brew로 설치해준다. 

```
brew install sonar-scanner
```

[www.sonarqube.org/downloads/](https://www.sonarqube.org/downloads/)


사이트에서 무료버전인 community 버전을 다운로드 받고,  zip파일 압축을 풀어준다.

터미널을 통해 sonarqube 폴더 위치를 확인하고, 아래 명령어를 실행한다.

```
/usr/sonarqube-8.6.0.39681/bin/macosx-universal-64/sonar.sh console
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FzdbiF%2FbtqSQ6hlHpH%2FoUod8lJky0Ahs20mfkWbf1%2Fimg.png)

sonarqube is up이 뜬다면 성공! 

sonarqube server를 띄워주는데 default url은 http://localhost:9000 이다. 

브라우저에 해당 주소를 입력하면 로그인 창이 나온다. 

초기 id, password는 모두 admin 이다. 

로그인을 하면 sonarqube 대시보드 창으로 넘어간다. 

프로젝트 탭을 눌러 메뉴로 들어가면 

새로운 프로젝트를 생성한다. 

프로젝트 키를 입력하고, 

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FBSDC6%2FbtqSZyi71Ry%2FSCTQQganWJbqNVdPv5sfuk%2Fimg.png)

토큰 이름을 입력하고 (간단하게 나는 token 으로) generate 버튼을 누르면 토큰 키가 생성된다. 

키는 저장할 필요없다. 다음 단계에서 copy하도록 되어 있음

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbkksq1%2FbtqS3J5eTr3%2FgT9naJVeXcAPpFy6Y0dZPk%2Fimg.png)

아래처럼 프로젝트에 해당하는 것을 선택한다.

여기서 소나스캐너는 brew로 설치해주었으므로 다운로드 받을 필요가 없다.

맨 아래에 있는 소나 스캐너 명령어만 copy 해준다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fmy1O7%2FbtqSXkMuhBx%2F4oo8oRSuvqwjQeLAQXRPPk%2Fimg.png)

-------------------
### 2\. 소나스캐너로 코드 검사 하기

위에서 복사했던 소나스캐너 명령어를 검사할 프로젝트 root 위치에서 실행해준다. 

여기서 나는 git scm 에러가 발생했다. 

그래서 '\-Dsonar.scm.provider=git' 을 명령어 뒤에 추가해줬다. 

```
sonar-scanner \
  -Dsonar.projectKey=test_automation \
  -Dsonar.sources=. \
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.login={토큰 키} \
  -Dsonar.scm.provider=git
```

해당 명령어를 실행하면 아래와 같이 모든 코드가 정적분석 검사되고, 

SUCCESS 가 뜨는지 확인!!

```
INFO: Scanner configuration file: /usr/local/Cellar/sonar-scanner/4.5.0.2216/libexec/conf/sonar-scanner.properties
INFO: Project root configuration file: NONE
INFO: SonarScanner 4.5.0.2216
INFO: Java 13.0.1 Oracle Corporation (64-bit)
INFO: Mac OS X 10.15.5 x86_64
INFO: User cache: /Users/1004599/.sonar/cache
INFO: Scanner configuration file: /usr/local/Cellar/sonar-scanner/4.5.0.2216/libexec/conf/sonar-scanner.properties
INFO: Project root configuration file: NONE
INFO: Analyzing on SonarQube server 8.6.0
INFO: Default locale: "ko_KR", source code encoding: "UTF-8" (analysis is platform dependent)
INFO: Load global settings
INFO: Load global settings (done) | time=78ms
INFO: Server id: BF41A1F2-AXbgYkdem1niIyF4KTtH
INFO: User cache: /Users/1004599/.sonar/cache
INFO: Load/download plugins
INFO: Load plugins index
INFO: Load plugins index (done) | time=37ms
INFO: Load/download plugins (done) | time=95ms
INFO: Process project properties
INFO: Process project properties (done) | time=6ms
INFO: Execute project builders
INFO: Execute project builders (done) | time=1ms
INFO: Project key: test_automation
INFO: Base dir: /Users/1004599/Documents/workspace/testautoreact
INFO: Working dir: /Users/1004599/Documents/workspace/testautoreact/.scannerwork
INFO: Load project settings for component key: 'test_automation'
INFO: Load project settings for component key: 'test_automation' (done) | time=11ms
INFO: Load quality profiles
INFO: Load quality profiles (done) | time=60ms
INFO: Load active rules
INFO: Load active rules (done) | time=835ms
INFO: Indexing files...
INFO: Project configuration:
INFO: Load project repositories
INFO: Load project repositories (done) | time=33ms
INFO: 440 files indexed
INFO: 83692 files ignored because of scm ignore settings
INFO: Quality profile for css: Sonar way
INFO: Quality profile for js: Sonar way
INFO: Quality profile for web: Sonar way
INFO: Quality profile for xml: Sonar way
INFO: ------------- Run sensors on module test_automation
INFO: Load metrics repository
INFO: Load metrics repository (done) | time=23ms
INFO: Sensor CSS Metrics [cssfamily]
INFO: Sensor CSS Metrics [cssfamily] (done) | time=306ms
INFO: Sensor CSS Rules [cssfamily]
INFO: 5 source files to be analyzed
INFO: 5/5 source files have been analyzed
INFO: Sensor CSS Rules [cssfamily] (done) | time=3573ms
INFO: Sensor JaCoCo XML Report Importer [jacoco]
INFO: 'sonar.coverage.jacoco.xmlReportPaths' is not defined. Using default locations: target/site/jacoco/jacoco.xml,target/site/jacoco-it/jacoco.xml,build/reports/jacoco/test/jacocoTestReport.xml
INFO: No report imported, no coverage information will be imported by JaCoCo XML Report Importer
INFO: Sensor JaCoCo XML Report Importer [jacoco] (done) | time=4ms
INFO: Sensor JavaScript analysis [javascript]
INFO: 297 source files to be analyzed
INFO: Version of TypeScript used during analysis: 3.8.3
INFO: 118/297 files analyzed, current file: client/src/components/table/SortTable.js
INFO: 297/297 source files have been analyzed
INFO: Sensor JavaScript analysis [javascript] (done) | time=22167ms
INFO: Sensor C# Properties [csharp]
INFO: Sensor C# Properties [csharp] (done) | time=1ms
INFO: Sensor JavaXmlSensor [java]
INFO: 6 source files to be analyzed
INFO: Sensor JavaXmlSensor [java] (done) | time=344ms
INFO: Sensor HTML [web]
INFO: 6/6 source files have been analyzed
INFO: Sensor HTML [web] (done) | time=44ms
INFO: Sensor XML Sensor [xml]
INFO: 6 source files to be analyzed
INFO: Sensor XML Sensor [xml] (done) | time=301ms
INFO: Sensor VB.NET Properties [vbnet]
INFO: 6/6 source files have been analyzed
INFO: Sensor VB.NET Properties [vbnet] (done) | time=1ms
INFO: ------------- Run sensors on project
INFO: Sensor Zero Coverage Sensor
INFO: Sensor Zero Coverage Sensor (done) | time=118ms
INFO: SCM Publisher SCM provider for this project is: git
INFO: SCM Publisher 307 source files to be analyzed
INFO: 265/307 source files have been analyzed
INFO: SCM Publisher 307/307 source files have been analyzed (done) | time=11905ms
INFO: CPD Executor 10 files had no CPD blocks
INFO: CPD Executor Calculating CPD for 288 files
INFO: CPD Executor CPD calculation finished (done) | time=196ms
INFO: Analysis report generated in 304ms, dir size=3 MB
INFO: Analysis report compressed in 1147ms, zip size=1 MB
INFO: Analysis report uploaded in 42ms
INFO: ANALYSIS SUCCESSFUL, you can browse http://localhost:9000/dashboard?id=test_automation
INFO: Note that you will be able to access the updated dashboard once the server has processed the submitted analysis report
INFO: More about the report processing at http://localhost:9000/api/ce/task?id=AXbgx7Srm1niIyF4KYkI
INFO: Analysis total time: 59.869 s
INFO: ------------------------------------------------------------------------
INFO: EXECUTION SUCCESS
INFO: ------------------------------------------------------------------------
INFO: Total time: 1:00.770s
INFO: Final Memory: 13M/57M
INFO: ------------------------------------------------------------------------
```

검사가 다 완료된 후에는 

**'http://localhost:9000/dashboard?id=test\_automation'** 에 접속하여 분석 결과를 확인하면 된다. 


![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F0ULxl%2FbtqS3aaXFqL%2Fgr6OAyBjbKpIbwlaVjtPU0%2Fimg.png)

프론트엔드 코드는 보통 eslint + prettier 조합으로 코드 컨벤션 및 문법 체크 등을 한다. 

여기에 husky + lint-staged 조합을 사용하면 내가 수정한 코드를 git에 커밋하기 전에 체크하고, 통과 안되면 커밋이 불가능하게 된다. 

소나큐브에서는 보안, 코드 중복, 코드 스멜 등을 검사할 수 있으니 추가적으로 검사하는 것도 좋을 듯 하다. 

만약에 정적분석 검사를 자동화하고 싶으면 젠킨스와 같이 사용하여 빌드 배포시 마다 소나큐브를 돌리게 할 수도 있다. 

테스트 코드를 작성하거나 typescript를 사용하는 것도 도움이 될 것 같다. 

여유가 되면 나중에 하는 것으로 ㅜ

소나큐브 삽질기 끝!!


{{< adsense >}}