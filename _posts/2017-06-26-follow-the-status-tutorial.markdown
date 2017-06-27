---
layout: post
title:  "Status 튜토리얼 따라가보기 / Follow the Status tutorial(#my-first-chatbot) "
date:   2017-06-26 22:26:00 +0900
categories: 
---

암호화폐 시장에 관심이 생겼다. 괜찮다 생각되는 ICO에는 펀딩도 했다.  
그 중 하나가 최근에 ICO가 종료 된 Status 이다.  
Status는 이더리움 네트워크 상에 올라가는 탈중앙화 메신저다. 

마침 Status App의 튜토리얼 문서가 쉽게 설명 되어 있어서 투자자의 마음으로 한 번 따라가보았다.  

Status 튜토리얼 페이지 My First Chatbot 부분까지 진행하였음.
디바이스는 iOS 시뮬레이터.

참고한 페이지는 다음과 같다.

Recently, one of my concerns is crypto currency. I also funded an ICO that looked interesting.
One of them is Status ICO, which was recently ended.
Status is a decentralized instant messenger that rides on the Ethereum network.

The tutorial in the Status App looked simple and straightforward.  
So I went through the app tutorial.

I followed up to #my-first-chatbot of the Status tutorial.  
The target device used only the iOS simulator.

The reference page is as follows.

[스테이터스 앱 위키 / Status Wiki](https://wiki.status.im/contributing/development/building-status/)  
[Status Documentation#my-first-dapp](http://docs.status.im/#my-first-dapp)  
[Status 개발 환경설정과 Hello Status만들기(1)](http://www.chaintalk.io/archive/lecture/758)  
  
빌드하기 위해 설치해야 되는 요구사항과 의존성에 대한 설명은 [스테이터스 앱 위키 / Status Wiki](https://wiki.status.im/contributing/development/building-status/)에 잘 나와있다.  
A description of the requirements and dependencies that need to be installed to build is outlined in [스테이터스 앱 위키 / Status Wiki](https://wiki.status.im/contributing/development/building-status/).  

해당 위키에 나온 순서대로 의존모듈들을 내려받고 다음처럼 react-native 앱을 실행하면 된다. 
Download the dependent modules in the order listed on the wiki and run the react-native app as follows.

#### # Run (iOS)
    $ react-native run-ios

#### # Intro
![Status Intro](/assets/status-1.png){:width="50%"}  
접근 권한을 설정해야 한다.  
You need to set access permissions.  
![Status Access Setting](/assets/status-access.png){:width="50%"}

#### # Sign In
![Status Sign In](/assets/status-login.png){:width="50%"}

#### # Console  
여기서 /debug On 해준다.  
![Status Screen#1](/assets/status-debug-on.png){:width="50%"}
  
#### # Contacts
![Status Screen#2](/assets/status-screen2.png){:width="50%"}

#### # Wallet
![Status Screen#3](/assets/status-screen3.png){:width="50%"}


#### # FirstBlood 
![Status Screen#4](/assets/status-fb.png){:width="50%"}   
FirstBlood Chatbot에게 1000 ETH를 Request 해 봤다.  
몰론 오지 않았다.  

I asked FirstBlood Chatbot for 1000 ETH.  
Of course. did not come.  

다음은 testrpc를 실행하고 status-dev-cli를 사용해 app 의 노드를 testrpc 로 연결한다.
Next, run testrpc and connect the node of your app to testrpc using status-dev-cli.

#### # Install testrpc 
    $ npm install -g ethereumjs-testrpc

#### # Run testrpc 
    $ testrpc -p 8546

#### # status device scan
    $ status-dev-cli scan
    Searching for connected devices...
    Status iOS (xxxx::xxx:xxxx:xxxx:xxx, 192.168.1.x)

#### # Node Switching
    $ status-dev-cli switch-node http://localhost:8546 --ip 192.168.1.x   
    You've successfully switched the node.  

#### # testrpc terminal
    ...
    shh_post
    shh_post
    eth_syncing
    shh_post
    eth_syncing  
    ...

어떤 메시지가 나오며 테스트 노드와 동기화를 하는 것 같았지만, web3 관련 경고만 발생할 뿐 진행이 되지 않았다. 
Some messages appeared to be synchronizing with the test node, but only web3 related warnings occurred, not progress.    
![web3 warn](/assets/status-error-full.png){:width="50%"}

다음 링크에서 web3 response 가 정상적으로 동작하지 않는 이유를 알 수 있었다.  
이 링크에 따르면 현재 Status App은 다른 테스트넷 또는 사설 테스트넷에 연결하는 환경은 아직 제공하지 않는단다.   
[Status 개발 환경설정과 Hello Status만들기(1)](http://www.chaintalk.io/archive/lecture/758) 

In the next link, we can see why the web3 response does not work normally.  
According to this link, the Status App does not currently provide an environment for connecting to other test or private test nets.  
[Status 개발 환경설정과 Hello Status만들기(1)](http://www.chaintalk.io/archive/lecture/758) 




다음으로 Truffle을 설치 후 truffle-status-box 를 띄워 올려보겠다.   
여기서부터는 [Status Documentation#my-first-dapp](http://docs.status.im/#my-first-dapp)를 따라했다.   


Next, after installing Truffle, and display the truffle-status-box.  
From here, I followed [Status Documentation # my-first-dapp](http://docs.status.im/#my-first-dapp).

#### # Install truffle(Version 3.0.5+ required)
    $ npm install -g truffle 

#### # Install truffle-box-status & Compile
    $ git clone https://github.com/status-im/truffle-box-status.git
    $ cd truffle-box-status && npm install
    $ truffle compoile
    $ truffle migrate #testrpc 가 실행되고 있어야 한다.

#### # Run truffle-box-status
    truffle-box-status를 실행한다.
    $ npm run start

#### # adding truffle-box-status
    truffle-box-status라는 이름의 dApp 이 실행되고 있는지 확인한다.
    $ status-dev-cli list --ip 192.168.1.x (Device IP)

    다음과 같이 표시 될 것이다.

    dapp-0x74727566666c652d626f782d737461747573 (Name: "truffle-box-status", DApp URL: "http://localhost:3000")


#### # truffle-box-status 
Contacts와 Chats에 truffle-status-box dApp이 추가 되었다.  
![Truffle-Status-Box](/assets/status-truffle-box-status-1.png){:width="50%"}  

![Truffle-Status-Box](/assets/status-truffle-box-status-2.png){:width="50%"}  


#### # Chatbot
    truffle-box-status/public/bot 디렉토리를 만들고 
    bot.js 파일을 만든다.

    $ cd ~/truffle-box-status/public/ && mkdir bot/
    $ touch bot/bot.js
    $ nano bot/bot.js

    이후 status-dev-cli 로 watch를 걸어 놓으면 watch가 동작하여 변경 된 정보가 바로 dApp 으로 반영이 된다. 명령어는  
    status-dev-cli watch $PWD "<whisper-identity>" –ip 192.168.1.x

#### # 이제 bot.js 파일을 수정한다.
    status.command({
        name: "hello",
        title: "HelloBot",
        description: "Helps you say hello",
        color: "#CCCCCC",
        preview: function (params) {
                var text = status.components.text(
                     {
                         style: {
                             marginTop: 5,
                            marginHorizontal: 0,
                            fontSize: 14,
                            fontFamily: "font",
                            color: "black"
                        }
                    }, "Hello from the other side!");
                return {markup: status.components.view({}, [text])};
            }
        });

#### # Hello Status
![Hello Status](/assets/status-hello.png){:width="50%"}



#### # 끝맺음 Conclusion

Status 튜토리얼 페이지가 너무나 잘 되어있어서 큰 막힘 없이 #my-first-chatbot 예제까지 따라할 수 있었다.  
그리고 Status와 truffle-status-box가 많은 부분 React로 만들어져 있어서, 웹/앱 개발에 관심이 있는 사람은 소스를 분석하는 것도 재미있을 것 같다.  

Status 백서에 나온 예시들이 실제 구현되기까지는 적지 않은 시간이 걸릴 것 같지만,  
어떠한 아웃풋도 없고 추상적인 내용만 가득 찬(내가 이해 못했을 수도만있지만) ICO가 넘쳐나는 요즘에
일반 사용자도 직접 만져볼 수 있는 아웃풋을 제공하는 Status 팀의 노고에 박수를 쳐 주고싶다.


The tutorial page was so good that I was able to follow the # my-first-chatbot example without much clogging.
And Status and truffle-status-box are mostly made up of React, so anyone interested in web / app development might be interested in analyzing the source.

I think the Status will take some time before the examples in the white paper are actually implemented.
But it's a much better project than some ICOs that invest in a white paper filled with abstract content without a single line of source code.
I would like to applaud the Status team's efforts to provide output that can be touched by the general public.

