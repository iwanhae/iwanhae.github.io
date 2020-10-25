---
title: "ShellinaBox 웹에서 즐기는 터미널"
description: 구 블로그에서 가져옴
date: 2017-10-01
slug: shellinabox
image: 1315785_orig.png
draft: false
categories:
    - Server
---
## 서론
지금 필자는 군인이다.
군대에 있다.

다행이도 보직을 그런쪽으로 받아서 그런지 컴퓨터를 사용할 기회가 많으며 여가시간을 이용해 군대내 인트라넷이 아닌 외부 인터넷에 접속할 기회도 많다.

단지 문제가 있는건...... 열려있는 포트가 80이랑 443밖에 없다..... 

아시는분은 이미 알고있겠지만 이 두 포트는 일반적인 http 통신포트와 https통신포트로 즉, 웹서핑 이외에는 할수있는게 거의 없다.

일반적인 유저라면 이는 별 문제가 되지 않겠지만...... 필자에게 한가지 문제가 있는데 SSH가 안된다.... (이놈은 22번 포트사용)

이런 상황에서 웹에서 터미널을 이용할 방법을 찾으며 여러가지 삽질을 하다가 찾아낸게 ShellInABox이다.

(이거 세팅하기까지는 Cloud9에서 제공하는 터미널 기능 썼다.)

## 본론
설치는 쉽다. 

`apt install shellinabox`

끗.

설정도 쉽다.

`/etc/default/shellinabox`
(사용하는 포트, 기본적인 Black/White list 설정가능)

서비스확인은

`service shellinabox start/stop/status`

그 외 기타 명령어는

`shellinaboxd`

등으로 끝이다.


## 결론
~~음핫핫핫핫~~

~~군대에서 SSH로 서버에 접속만 가능하면 난 무적이다!!!~~

는 농담이고 빨리 전역하고 싶습니다.... 
( https://goon.iwanhae.ga )