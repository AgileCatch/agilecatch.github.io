---
layout: post
title: favicon site 
description: >
  
sitemap: false
hide_last_modified: true
categories :
 - github
---


# GitHub Pages 활성화 시켜 여러 repository 웹 호스팅하기.

들어가기 전에 githubpages에 간단히 알아보자.
<h4>github pages란?</h4>
쉽게말해 github저장소의 내용을 웹페이지로 호스팅 해주는 서비스이다.
repository에 올린 소스를 직접 웹페이지를 통해서 보여주고 무료로 웹서버를 호스팅 할 수 있다.

대표적인 사례로 기술블로그로 많이 이용된다.
깃허브 페이지의 url은 다음과 같은 형식으로 생겨먹었다.
~~~
https://username.gibhub.io
~~~
와 같은 형태의 url을 본 적이 있을 것이다.
이 외 간단한 웹 프로젝트를 구현해볼 수 있으나, 저장소의 최대용량이 1G로 제한되어 있기 때문에 무거운 프로젝트는 힘들 것 같다.

<h4>github pages  구축 방법 </h4>
먼저, 공식 사이트에 가이드 라인을 잘 제공하고 있다.
* 참조 가이드 : https://pages.github.com/

가이드에서 알 수 있듯이 repository 명을 username.github.io 로 만들면 별도의 작업없이 소스만 업로드 하면 호스팅이 되고, 저장소명이 기본 도메인이 된다.  즉,
~~~
https://userName.github.io
~~~
로 접속을 하면 저장소 루트의 첫페이지.html 또는 md 내용에 웹에 출력된다.

<span style="color:red">하지만!!!</span>  깃허브에서 이런 메인 호스팅작업은 1계정당 1페이지 밖에 제공하지 않는다. 그렇다면 여러 Repository를 만들어 띄우고 싶다면 여러 계정을 파야할까?? 답은 단연 <span style="color:red">NO.</span>
repository명을 "userName.github.io" 형식이 아닌 자유형식으로 지정하되, 별도의 GitHubpages 활성화 설정을 해주면 "userName.github.io/repoName"형식으로 호스팅이 가능하다! 지금부터 별도 활성화 설정을 설명한다.

1. repositoy > settings > pages 진입
![그림](/assets/img/blog/setting.png)
2. 각 저장소의 source 에 대한 기본 설정은 None 이기 때문에 Github Pages 가 활성화 되어있지 않다. none에서 master로 변경하여 githubpages를 활성화 시켜준다.  
![그림](/assets/img/blog/nonetomaster.png)
3. 활성화가 완료되며 도메인/reponame/으로 주소를 제공한다.
~~~
ex)
https://userName.github.io/repo2/
~~~
![그림](/assets/img/blog/pagesdone.png)

주소를 눌러 시작 html페이지가 잘 뜨는지 확인해보자.
이렇게 설정을 해주면 여러 repositoy를 경로명만 다르게 해서 호스팅 할 수 있다.

> 🚫 404 에러가 발생 시,

페이지 시작 html명을 경로에 추가하여 접속해본다.
defualt인 index.html로 가정했을때
~~~
https://userName.github.io/repo2/index.html
~~~
로 시도를 해보자. 접속이 될 것이다.
