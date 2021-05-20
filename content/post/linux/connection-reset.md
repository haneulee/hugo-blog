---
title: "connection reset by [ip] port 22"
date: 2021-05-18T12:31:38+09:00
categories: 
- development
- linux
tags: 
- development
- front-end
- connection
- server
- ssh
- 리눅스
- 서버
- 
keywords: 
- development
- front-end
cover: ""
draft: false
thumbnailImage: ""
# coverImage: //d1u9biwaxjngwg.cloudfront.net/cover-image-showcase/city.jpg
metaAlignment: center
coverMeta: out
---

리눅스에서 ssh 접속 후 아무 작업을 하지 않고 그대로 두면 Connection reset by peer 메시지와 함께 접속이 끊기는 경우가 발생한다.

  Read from remote host xxx.xxx.xxx.xxx: Connection reset by peer  
  Connection to xxx.xxx.xxx.xxx closed.

1)/etc/ssh/sshd\_config에 다음을 추가하고 재실행해주면 새로 접속하는 ssh부터는 아무런 작업을 하지 않는다고 해도 끊기지는 않을 것이다.  
  ClientAliveInterval 600  
  ClientAliveCountMax 3

ClientAliveInterval 초단위 (default 0)  
Client에서 수신한 data가 없을 경우 sshd 데몬에서 클라이언트가 살아있는지 체크하기 위한 메시지(client alive messages)를 보내게 되는데, 이 메시지를 보내는 초단위 간격을 설정한다. 0이면 보내지 않는 것이며, 600이면 600초(10분) 간격으로 클라이언트로 메시지를 보내고 응답을 확인한다. 이 메시지는 암호화된 채널을 통해 보내지므로 스푸핑을 할 수 없다. SSH protocol V2에서만 적용

ClientAliveCountMax 횟수 (default 3)  
클라이언트에서 응답이 없을 때 메시지를 보내는 횟수를 지정한다. 횟수가 3이면 600초 X 3회 = 총 30분간 응답이 없다면 접속이 끊기게 된다.

2)client쪽에서 문제를 해결하려면 ssh(client)가 서버측에 주기적 시간 간격(초 단위)으로 신호를 보내면 됩니다. /etc/ssh\_config 또는 ~/.ssh/config(cygwin solution)에 다음을 추가하고 재실행하면 끊기지는 않을 것이다.  
  Host \*  
  ServerAliveInterval 200

(vi ssh\_config 파일 readonly이면 sudo su로 root로 로그인하여 다시 시도 )