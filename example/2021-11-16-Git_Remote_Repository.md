---
layout: post
title: favicon site 
description: >
  
sitemap: false
hide_last_modified: true
categories :
 - github
---



# git 저장소 주소 repository 변경하기
Git에서 remote repository를 다른 주소 URL로 변경해 보자.
예를 들어 기존의 repository에서 형상관리를 하다가 새로운 repository를 생성 한 경우,새 repository로 형상관리를 하겠다라고 한다면 기존의 주소를 새로운 저장소 주소로 바꿔주어야 한다.
- 기존 주소 : https://github.com/user/repo1.git
- 새로운 주소 : https://github.com/user/repo2.git

0. 먼저 현재 연결된 주소를 확인.
~~~shell
git remote -v
~~~
~~~shell
//결과
origin  https://github.com/user/repo1.git (fetch)
origin  https://github.com/user/repo1.git (push)
~~~

1. remote set-url
set-url 로 새로운 url 을 셋팅하는 방법.
~~~shell
git remote set-url origin [새로운 repo 주소]
~~~
ex)
~~~shell
$ git remote set-url origin https://github.com/user/repo1.git
~~~

2. remote remove / add
remove로 기존 연결을 끊고 새로 추가하는 방법.

 ~~~shell
 2.1
 git remote remove origin
 ~~~

 ~~~shell
 2.2
 git remote add origin https://github.com/user/repo1.git
 ~~~

 >🚫 Remote origin already exists 에러
 기존의 repository가 연결된 상태에서 add를 하면 발생하는 에러이다.
 위의 1 또는 2번의 방법으로 해결할 수 있다.


3. git remote -v 으로 원하는 repo 주소가 잘 연결되어 있는지 확인한다.


4. 소스를 추가/커밋/푸시한다.
~~~shell
* git push 순서
0. git init    #현재 디렉토리에 깃 생성
1. git add .   #변경된 모든 소스 추가
   git add [특정파일명] #특정 소스파일 추가
2. git commit -m 'commit-message' #커밋
3. git push origin master #최종 푸시로 깃서버에 uplaod.   
~~~

5. 깃허브 웹 repository로 가서 소스가 잘 업로드 되었는지 확인한다.
