---
layout: post
title:  "스테이터스 앱 빌드 해보기 / Building Status App"
date:   2017-06-26 22:26:00 +0900
categories: 
---
친구가 전에 알려 준 Building Status 페이지가 생각이 났다.  
[스테이터스 앱 위키 / Status Wiki](https://wiki.status.im/contributing/development/building-status/)

빌드 하기 전, 설치해야 되는 요구사항과 의존성에 대한 설명이 꽤 자세히 나와있어서
iOS 시뮬레이터로 띄우기까지는 그다지 어렵지 않았다.

다음은 빌드해서 시뮬레이터로 띄워 본 화면이다. 

![Status Intro](/assets/status-1.png)
![Status Screen#1](/assets/status-screen1.png)
![Status Screen#2](/assets/status-screen2.png)
![Status Screen#3](/assets/status-screen3.png)

그 후 testrpc를 실행하고 status-dev-cli를 사용해 app 의 노드를 testrpc 로 연결했다.
#### $ status-dev-cli switch-node http://localhost:8546 --ip 192.168.1.x   
이런식으로 연결하니 
#### You've successfully switched the node.  
라는 메시지가 나오고 testrpc 에 
#### eth_syncing  
이라는 메시지가 나오며 싱크를 맞추는 듯 했는데

다음처럼 에러가 발생할 뿐 뭔가 진행이 되지 않았다.
![web3 Error](/assets/status-error.png)

(계속)
