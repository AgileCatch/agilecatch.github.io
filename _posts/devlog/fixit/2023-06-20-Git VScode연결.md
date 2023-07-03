---
layout: post
title: Git_VScode연결
accent_image: 
  background: url('/assets/img/me/wave3.jpg') center/cover
  overlay: false
accent_color: '#fff'
theme_color: '#fff'
description: >
  문제해결
invert_sidebar: true
categories :
 - devlog	
 - fixit


---

# [GitHub] 레포지토리 쉽게 연결하는 방법

자기 컴퓨터(Local) 폴더에 Github쉽게 연결하는방법



* toc
{:toc}
---



## 1. 깃허브 레포지토리 생성

내가연결하고싶은 파일이름으로 깃허브 레포지토리를 생성해준다.

### 이때주의 해야할점! 

- Public 체크!

- Add a README file 체크!

![finder1.png](../../../assets/img/blog/finder1.png)

## 2. 파일 이동하기

 git_clone(내가 클론하고싶은 파일)의 파일을 잠시 다른 경로로 옮겨준다.

-> 나는 아래의 Flutter경로에 있던 git_clone파일을 데스크탑으로 이동해주었다.

![finder2.png](../../../assets/img/blog/finder2.png)

## 3.  GitHub Desktop에들어가 연결하기

 Add > Clone Repository...>![finder3.png](../../../assets/img/blog/finder3.png)

만들었던 레포지토리를 찾아 클릭한후 동일한 이름으로 클론해준다.

![finder4.png](../../../assets/img/blog/finder4.png)

이후 기존경로에 파일이 생성되었는지 확인해보자.

![finder5.png](../../../assets/img/blog/finder5.png)

파일 내용을살펴보면 Rademe 파일이 있을것이다. 이것을 삭제해준다.

![finder6.png](../../../assets/img/blog/finder6.png)

![finder7.png](../../../assets/img/blog/finder7.png) 바탕화면에 있던 git_clone파일 내용을  Flutter파일 안에 있는 git_clone으로 옮겨주었다.

![finder8.png](../../../assets/img/blog/finder8.png)

## 4. 확인하기

파일을 옮기고 GitHub Desktop에 들어가확인해보자.

![finder9.png](../../../assets/img/blog/finder9.png)

파일이 정상적으로 클론된것을 확인되었다.

커밋을 해보자!

![finedr10.png](../../../assets/img/blog/finedr10.png)

깃허브 레포지토리를 확인해보니 정상적으로 파일이 연결된 것 을 볼 수 있었다!

