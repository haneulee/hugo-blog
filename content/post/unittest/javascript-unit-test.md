---
title: "Javascript 테스트"
date: 2021-05-20T11:07:12+09:00
categories:
  - development
  - unittest
tags:
  - development
  - front-end
  - unittest
  - javascript
  - testrunner
  - mocha
  - jasmine
  - karma
  - jest
  - ava
  - qunit
  - 유닛테스트
  - 테스트코드
  - 테스트프레임워크
keywords:
  - development
  - front-end
cover: ""
draft: false
thumbnailImagePosition: left
thumbnailImage: "https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/unittest/img-1.png"
# coverImage: //d1u9biwaxjngwg.cloudfront.net/cover-image-showcase/city.jpg
metaAlignment: center
coverMeta: out
---

<!--toc-->

<p>
  <br/>
</p>
<h1>1.자바스크립트 테스팅 환경</h1>
<h1>테스트 러너</h1>
<ul>
  <li class="gb gc eg ge b gf jr gh gi gj js gl gm gn jt gp gq gr ju gt gu gv jv gx gy gz jz ka kb fc" style="list-style-type: disc;">테스트 파일을 읽어들여 실행하고, 결과를 출력</li>
  <li class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc" style="list-style-type: disc;">파일이 변경된 경우 자동으로 실행해주는 watch 등의 기능 제공</li>
  <li class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc" style="list-style-type: disc;">Reporter를 지정해서 원하는 형태로 결과를 출력</li>
  <li class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc" style="list-style-type: disc;">
    <strong>Node 환경</strong>에서 실행 : <span style="color: rgb(255,0,0);">Mocha, Jest, AVA</span>
  </li>
  <li class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc" style="list-style-type: disc;">
    <strong>브라우저 환경</strong>에서 실행 : <span style="color: rgb(255,0,0);">Karma</span> → 웹서버에 연결되어 있는 브라우저 위에서 테스트를 수행</li>
</ul>
<p class="gb gc eg ge b gf gg gh gi gj gk gl gm gn go gp gq gr gs gt gu gv gw gx gy gz db fc">카르마보다 Node가 조금 더 빠르다.</p>
<h1 class="iw hk eg as ix iy iz gh ja jb jc gl jd je jf jg jh ji jj jk jl jm jn jo jp jq fc">테스트 프레임워크</h1>
<ul>
  <li class="gb gc eg ge b gf jr gh gi gj js gl gm gn jt gp gq gr ju gt gu gv jv gx gy gz jz ka kb fc" style="list-style-type: disc;">사용자가 테스트 코드를 작성할 수 있는 기반을 제공</li>
  <li class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc" style="list-style-type: disc;">프레임 워크에 의해 제공된 함수를 이용해서 테스트 코드를 작성<br/>⇒ 프레임 워크가 자동으로 테스트를 실행하고 결과를 수집해서 출력.</li>
  <li class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc" style="list-style-type: disc;">테스트 Spec 들을 그룹핑하거나 공통 사전 작업 등을 처리해 줌.</li>
  <li class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc" style="list-style-type: disc;">Mocha, Jasmine(Jest), AVA</li>
  <li class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc" style="list-style-type: disc;">예제 (Jasmine)</li>
</ul>
<pre class="hb hc hd he hf hg hh hi">
  <br/>
</pre>
<p>
  <br/>
</p>
<h1>2.브라우저 환경 vs Node.js 환경</h1>
<p class="gb gc eg ge b gf jr gh gi gj js gl gm gn jt gp gq gr ju gt gu gv jv gx gy gz db fc">
  <strong>브라우저에서 테스트 실행</strong>
</p>
<ul>
  <li class="gb gc eg ge b gf gg gh gi gj gk gl gm gn go gp gq gr gs gt gu gv gw gx gy gz jz ka kb fc" style="list-style-type: disc;">실제 브라우저 환경에서 테스트 코드를 실행</li>
  <li class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc" style="list-style-type: disc;">브라우저의 모든 API를 사용해서 테스트 가능</li>
  <li class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc" style="list-style-type: disc;">실제 브라우저를 실행해야 하기 때문에 번거로움(Headless 브라우저 사용) ⇒ Headless gui 없이 실행시키는 환경.</li>
  <li class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc" style="list-style-type: disc;">테스트 파일 별로 별도의 브라우저에서 테스트 하기가 어려움(속도 문제)</li>
  <li class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc" style="list-style-type: disc;">빈 페이지를 만들고 모든 스크립트 파일 및 CSS등을 include 해서 테스트(번들 과정 필요)</li>
  <li class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc" style="list-style-type: disc;">브라우저 호환성 테스트 가능</li>
  <li class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc" style="list-style-type: disc;">개발 시 : 빠른 피드백을 위해 Headless 브라우저를 사용</li>
  <li class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc" style="list-style-type: disc;">빌드 시 : CI 서버 및 Webdriver와 연동하여 여러 개의 브라우저에서 테스트</li>
</ul>
<p class="gb gc eg ge b gf gg gh gi gj gk gl gm gn go gp gq gr gs gt gu gv gw gx gy gz db fc">
  <strong>Node.js에서 테스트 실행</strong>
</p>
<ul>
  <li class="gb gc eg ge b gf gg gh gi gj gk gl gm gn go gp gq gr gs gt gu gv gw gx gy gz jz ka kb fc" style="list-style-type: disc;">Node.js 환경에서 테스트 코드를 실행(Mocha, Jest 등)</li>
  <li class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc" style="list-style-type: disc;">브라우저에 비해서 가볍기 때문에 실행 속도가 빠름.</li>
  <li class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc" style="list-style-type: disc;">개별 테스트 파일을 별도의 프로세스에서 실행할 수 없음(병렬 실행 가능)</li>
  <li class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc" style="list-style-type: disc;">브라우저 API 대신 JSDom을 이용해서 테스트 ⇒ JSDom = 가짜 브라우저.</li>
  <li class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc" style="list-style-type: disc;">실제 렌더링을 해 주지 않으므로, 렌더링 관련 테스트 불가능</li>
  <li class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc" style="list-style-type: disc;">브라우저 호환성 테스트 불가능.</li>
</ul>
<p class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc" style="list-style-type: disc;">
  <br/>
</p>

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/unittest/img-1.png)

<!--adsense-->

<p class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc" style="list-style-type: disc;">
  <br/>
</p>
<h1 class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc" style="list-style-type: disc;">Vue 프로젝트에 주로 사용되는 테스트 방식</h1>
<p class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc">
  <br/>
</p>
<blockquote>
  <p class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc">
    <strong>Vue CLI 로 프로젝트 시작 설정에서</strong>
  </p>
  <p class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc">
    <strong>Unit Test 로 <span style="color: rgb(255,0,0);">Jest</span> 또는 <span style="color: rgb(255,0,0);">Mocha + Karma</span> 선택 가능</strong>
  </p>
</blockquote>
<p class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc">
  <br/>
</p>
<p class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc">
  <br/>
</p>
<p class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc">
  <br/>
</p>
<h1>karma</h1>
<hr/>

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/unittest/img-2.png)

<ul>
  <li>브라우저 런처를 이용하여 다양한 브라우저를 띄우고, 그 위에서 테스트 코드를 실행한다. (런처 설치 필요)</li>
  <li>웹 소켓을 통한 연결 : 카르마는 웹 소켓을 이용해 브라우저가 카르마 웹서버와 커넥션을 만든다. → 파일 변화 자동 감지</li>
  <li>Iframe 기반 테스트 : 테스트 대상 코드를 iframe에 로드하여 테스트를 수행한다. 테스트 실행마다 iframe을 다시 로드</li>
  <li>jasmine이나 mocha같은 테스트 프레임워크는 node 기반의 러너만 제공하기 때문에 브라우저 환경에서 도는 러너가 필요</li>
  <li>카르마 서버 ↔ 클라이언트 매니저 ↔ iframe ↔ 테스트 프레임워크 어댑터 ↔ 테스트 프레임워크<br/>
    <ul>
      <li>성공 실패 여부는 이벤트를 발생시킴으로써 클라이언트 페이지로 postMessage 를 통해 전달한다.</li>
      <li>클라이언트 페이지는 다시 웹 소켓을 통해 카르마 서버에 결과를 전달한다.</li>
    </ul>
  </li>
</ul>
<p class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc">
  <br/>
</p>
<p class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc">→ Mocha + Karma</p>
<p class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc">

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/unittest/img-3.png)

</p>
<p class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc">
  <br/>
</p>
<p class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc">

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/unittest/img-4.png)

</p>
<p class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc">
  <br/>
</p>
<p>
  <br/>
</p>
<h1 class="iw hk eg as ix iy ko gh ja jb kp gl jd je kq jg jh ji kr jk jl jm ks jo jp jq fc">Jasmine</h1>
<hr/>
<p class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc" style="list-style-type: disc;">
  <a href="https://jasmine.github.io/">https://jasmine.github.io/</a>
</p>
<ul>
  <li class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc" style="list-style-type: disc;">
    <span style="color: rgb(51,51,51);">BDD(Behavior Driven Development) 를 위한 API 제공</span>
  </li>
  <li class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc" style="list-style-type: disc;">
    <span style="color: rgb(51,51,51);">
      <span>비동기 코드 테스트 지원</span>
    </span>
  </li>
  <li class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc" style="list-style-type: disc;">
    <span style="color: rgb(51,51,51);">
      <span>NodeJS, 브라우저 환경 모두 지원</span>
    </span>
  </li>
  <li class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc" style="list-style-type: disc;">
    <span style="color: rgb(51,51,51);">
      <span>비교적 빠른 테스트</span>
    </span>
  </li>
  <li class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc" style="list-style-type: disc;">
    <span style="color: rgb(51,51,51);">
      <span>테스트 명세 그룹화 가능</span>
    </span>
  </li>
</ul>
<p class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc" style="list-style-type: disc;">
  <br/>
</p>
<h2 class="iw hk eg as ix iy ko gh ja jb kp gl jd je kq jg jh ji kr jk jl jm ks jo jp jq fc">1. <span style="letter-spacing: -0.008em;">HTML 페이지 방식 : </span>
  <span style="letter-spacing: -0.008em;">Jasmine </span>
</h2>
<p class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc" style="list-style-type: disc;">index.js → jasmine.css 와 jasmine.js 링크</p>
<p class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc" style="list-style-type: disc;">

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/unittest/img-5.png)

</p>
<p class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc" style="list-style-type: disc;">
  <br/>
</p>
<p class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc" style="list-style-type: disc;">test.vue → 테스트 코드 </p>
<p class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc" style="list-style-type: disc;">

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/unittest/img-6.png)

</p>
<p class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc" style="list-style-type: disc;">
  <br/>
</p>
<p class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc" style="list-style-type: disc;">테스트 화면 → '/test' 페이지 이동하여 테스트 코드 실행</p>
<p class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc" style="list-style-type: disc;">

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/unittest/img-7.png)

</p>
<p class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc" style="list-style-type: disc;">
  <br/>
</p>
<h2 class="iw hk eg as ix iy ko gh ja jb kp gl jd je kq jg jh ji kr jk jl jm ks jo jp jq fc">2. 테스트 러너 방식 : Jasmine + Karma</h2>
<p>→ </p>
<p>
  <br/>
</p>
<h1 class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc" style="list-style-type: disc;">
  <span style="font-size: 24.0px;letter-spacing: -0.01em;">Qunit</span>
</h1>
<hr/>
<p>
  <a href="https://qunitjs.com/" style="letter-spacing: 0.0px;">https://qunitjs.com/</a>
</p>
<p>
  <br/>
</p>
<ul>
  <li>강력하고 사용하기 쉬운 Javascript 단위 테스트 프레임워크</li>
  <li>가장 오래됨</li>
  <li>진입장벽 낮음</li>
  <li>
    <span style="letter-spacing: 0.0px;">jQuery, jQuery UI, jQuery Mobile 에서도 사용 가능</span>
  </li>
</ul>
<p>
  <br/>
</p>
<p>index.js → qunit.css 와 qunit.js 링크</p>
<p>

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/unittest/img-8.png)

</p>
<p>
  <br/>
</p>
<p>test.vue → 테스트 코드 </p>
<p>

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/unittest/img-9.png)

</p>
<p>
  <br/>
</p>
<p>홈화면</p>
<p>

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/unittest/img-10.png)

</p>
<p>테스트 화면 → '/test' 페이지 이동하여 테스트 코드 실행</p>
<p>

![](https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/unittest/img-11.png)

</p>
<p>
  <br/>
</p>
<p>
  <br/>
</p>
<p>
  <br/>
</p>
<h3>
  <a href="https://sungjk.github.io/2017/03/03/testing-react-application.html">→ Jest VS Mocha 비교 참고 사이트</a>
</h3>
<h1>Mocha</h1>
<hr/>
<ul>
  <li>Node.js 환경, 브라우저 환경 모두 지원</li>
  <li>TDD, BDD, QUnit, export 스타일 모두 적용</li>
  <li>Karma 테스트 러너와 함께 사용되기도 함</li>
  <li>assertion 은 Chai 와 함께 사용<span style="color: rgb(93,104,111);">
      <br/>
    </span>
  </li>
</ul>
<p class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc" style="list-style-type: disc;">
  <br/>
</p>
<h1>Jest</h1>
<hr/>
<ul>
  <li>jasmine 기반</li>
  <li>React에서 공식적으로 지원</li>
  <li>Auto Mocking 지원</li>
  <li>비동기 코드 테스트 지원</li>
  <li>스냅샷 테스트 지원</li>
</ul>
<p>
  <br/>
</p>
<h1 class="iw hk eg as ix iy ko gh ja jb kp gl jd je kq jg jh ji kr jk jl jm ks jo jp jq fc">Vue Test Utils</h1>
<hr/>
<p>
  <br/>
</p>
<ul>
  <li>vue 프레임워크에 한정적</li>
  <li>다른 프레임워크 변경 시, 테스트 코드도 새롭게 변경해야 함</li>
</ul>
<p class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc" style="list-style-type: disc;">
  <br/>
</p>
<p class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc" style="list-style-type: disc;">
  <br/>
</p>
<p class="gb gc eg ge b gf kc gh gi gj kd gl gm gn ke gp gq gr kf gt gu gv kg gx gy gz jz ka kb fc" style="list-style-type: disc;">
  <br/>
</p>
