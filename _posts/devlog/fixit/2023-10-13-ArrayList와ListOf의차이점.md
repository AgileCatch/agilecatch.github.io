---
layout: post
title: selector 
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

# [Android] ArrayList와 ListOf의차이점

* toc
{:toc}
---

안드로이드 스튜디오에서 Kotlin을 사용하여 어댑터를 만들고 있다면, `ArrayList`와 `listOf`의 차이점을 알아두는 것은 정말 중요하다!



## **1) ArrayList**

- `ArrayList`는 **크기가 가변적인 배열**을 나타낸다. 

  - 이는 배열의 크기를 **동적으로 조절할 수 있다**는 의미이다.

- 요소를 **추가**하거나 **제거**할 수 있다.

- 예를 들어, 다음과 같이 사용할 수 있다 

  ```
  kotlinCopy code
  val arrayList = ArrayList<String>()
  arrayList.add("사과")
  arrayList.add("바나나")
  arrayList.remove("사과")
  ```



## **2) listOf**

- `listOf`는 크기가 **고정된 불변 리스트**를 생성한다. 이는 **한 번 생성되면 크기가 변경되지 않는다**는 의미이다.

- 요소를 추가하거나 제거할 수 없다.

-  예를 들어, 다음과 같이 사용할 수 있습니다:

  ```
  kotlinCopy code
  val immutableList = listOf("사과", "바나나")
  // 아래 코드는 에러를 발생시킵니다.
  // immutableList.add("오렌지")
  ```

따라서, 어떤 것을 선택할지는 프로그램의 요구 사항에 따라 다르다.

만약 어떤 데이터를 동적으로 추가하거나 제거해야 한다면 `ArrayList`를 사용하고, 데이터가 변경되지 않아야 한다면 `listOf`를 사용하면 된다.