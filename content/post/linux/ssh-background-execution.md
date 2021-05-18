---
title: "ssh 백그라운드 실행 방법"
date: 2021-05-18T12:33:46+09:00
categories: 
- development
- linux
tags: 
- development
- front-end
- linux
- 리눅스
- ssh
- 백그라운드
- 서버
- npm
- nohup
- node
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

터미널에서 또는 명령창에서 

ssh 로 접속하여 서버를 실행 후, 

터미널을 종료하거나 다른 프로세스를 실행하면 이전 실행이 중단된다. 

해당 서버에서 계속 서버를 띄어놓기 위해 

백그라운드로 실행하는 방법이 있다. 

### nohup

nohup node server.js > /dev/null 2>&1 &

(.out 파일 없이 실행하기)

**<실행 방법>**

1\. 백그라운드에서 돌리기 위한 실행파일을 준비한다. (나의 실행파일 이름은 main.js)

2\. 명령어 입력하면 끝

\# nohup node /절대 경로/main.js &

\*구체적으로 노드를 nohup으로 구동하는 명령어

1) 일반 실행

\[root@localhost myWebRtc\]# node server.js

Socket IO server has been started

\- 내 ssh 프로세스가 node server.js 프로세스에 묶여버려 다른작업을 아무것도 하지 못한다.

2) Background 실행

\[root@localhost myWebRtc\]#**nohub node server.js &**(단, 현재 디렉토리에 파일이 있다는 가정)

\[1\] 31498

\- Background Process로 실행되어 

내가 실행하려고 했던 node.js 웹서버가 돌아가는 도중에도 동시에 다른 리눅스 명령어를 칠 수 있다.

3\. 잘 돌아가는지 확인

# ps -aux | grep main.js

**<중지하는 방법>**

ps 명령어로 PID 값을 찾은 후, kill 명령어로 프로세스를 종료시킨다.

\# ps -ef | grep a.out

\# kill -9 PID번호

※참고

nohup 명령어를 사용하면 명령어를 사용한 디렉토리에 nohup.out 이라는 파일이 자동 생성된다.(예를 들어, /dev/project/priceOnEachMarketWebVersion 에서 nohup를 실행시켰다면, 그 디렉토리 직하에 nohup.out이라는 파일이 생선된다.)

이 파일에는 nohup으로 실행하는 명령의 출력이 기록되어진다.

이 파일을 생성하고 싶지 않다면 /dev/null에 출력하도록 하면 된다.

\# nohup echo hello > /dev/null

[https://blog.dork94.com/3](https://blog.dork94.com/3)

[https://mytory.net/archives/2340](https://mytory.net/archives/2340)

[https://tyson.tistory.com/88](https://tyson.tistory.com/88)
