---
layout: post
title: favicon site 
description: >
  
sitemap: false
hide_last_modified: true
categories :
 - github
---


# Git Hub Pages 활용하기

<h4> Git이란? </h4>
 SW 개발 시 여러명의 사용자들 간 개발 작업을 조율하기 위한 분산 버전 관리 시스템.

<h4> Git hub란? </h4>
깃을 좀 더 편리하게 이용하도록 만든 깃 허버 웹 호스팅 서비스.
오픈 소스 소프트웨어의 중심지(hub)역할을 하면서 오픈소스 프로젝트가 널리 퍼지는 데 크게 기여하고 있는 서비스이다.

<h4> Git hub pages란?</h4>
깃허브에서 제공하는 정적 사이트 호스팅 서비스로 일반적인 html콘텐츠를 지원하는 것 외에도 다양하고 인기있는 정적 사이트 생성기인 Jekyll을 지원한다.

1. Github 가입
<img src="https://wepplication.github.io/images/post/2018/10/github-pages/github-signup.png">

2. Git hub repository 생성
![그림](/assets/img/blog/newreop.png)


3. 로컬 저장소에 깃허브 저장소 복제하기.
~~~java
git clone git@github.com:[userName]/[repositoryName]/git
~~~
이제 해당 프로젝트 폴더에 index.html파일을 추가하여 별도의 서버 없이 포트폴리오 사이트 등 간단한 사이트를 만들 수 있다.

* 로컬 저장소를 Cloud9, 구름IDE같은 클라우드 개발툴을 이용하면 특정 pc가 아닌 어디서든 사용 가능

4. Git hub저장소 push
변경사항을 깃 저장소에 push 하기
~~~java
$ git add .
$ git commit -m "commit message"
$ git push
~~~
**깃허브 웹에 접속해서 레포지토리를 확인해 보면 push내역에 반영된 것을 확인 할 수 있을 것이다.**

# GitHub Pages 활성화 설정.
깃허브 웹의 settings에서 저장소 설정을 변경할 수 있다.

<img src = "https://wepplication.github.io/images/post/2018/10/github-pages/github-pagesetting.png"/>

github pages > source 에 None으로 된 선택창을 master branch로 변경 후 save.
로 깃 페이지 소스 설정을 하면 저장소에 올린 파일들로 정적 사이트를 생성한다.
~~~
https://[userName].github.io/[repoName]/
~~~
으로 접속하여 생성된 사이트를 확인한다.

* 파일위치에 따른 URL
+ /index.html  : https://[userName].github.io/[repoName]
+ /test/index.html : https://[userName].github.io/[repoName]/aaa
+ /test.html: https://[userName].github.io.[repoName]/test

* URL뒤 저장소 이름없이 생성하기
repository 생성 후 page를 활성화 하면 기본적으로
~~~
"https://사용자이름.github.io/저장소이름/"
~~~
으로 생성이 되는데, 저장소 이름 없이 .io 까지 바로 연결되게 하고 싶으면 저장소 생성시 repository name에 "사용자이름.github.io"로 생성을 하면 된다.
이 경우 별도로 **깃허브 페이지 활성화 설정**을 하지 않아도 사이트가 생성이 된다.

# Git 명령어
~~~java
//git 사용자 정보 설정
git config user.name "[사용자이름]"
git config user.email [이메일주소]

//현재 디렉토리에 git 저장소 생성
git init

// 수정한 모든 파일들을 스테이징 영역에 올리기
git add .

//스테이지 영역에 올라가 있는 파일들을 커밋
git commit -m "커밋 메시지"

//원격 저장소에 푸시
//-u == 원격 저장소로부터 update 받은 후, push
git push -u origin master

//강제 push (force)
git push -f

//원격 저장소를 복제하여 저장소 생성
git clone 저장소 주소

//새 원격 저장소 추가
git remote add 이름 저장소주소

//원격 저장소 제거
git remote rm 이름

//무시할 파일을 .gitignore에 추가하기 전에 git push 한 경우
//원격 저장소에 있는 .gitignore파일 제거

$ git rm -r --cached .
$ git add .
$ git commit -m "Apply .gitignore"
$ git push
~~~
