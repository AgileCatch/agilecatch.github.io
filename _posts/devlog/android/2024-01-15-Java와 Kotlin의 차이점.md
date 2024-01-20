---
layout: post
image: /assets/img/blog/kotlin.png
accent_image: 
  background: url('/assets/img/me/wave3.jpg') center/cover
  overlay: false
accent_color: '#fff'
theme_color: '#fff'
description: >
  kotlin start!
invert_sidebar: true
categories :
 - devlog	
 - android

---

# [Kotlin] Java와 Kotlin의 차이점

* toc
{:toc}
---

왜 코틀린언어가 주목받고있고 현재 안드로이드 시장에서 많이 사용되는가? 생각해보자

## 간결성, 생산성

* 코틀린은 보다 **간결하고 표현력이 높은 문법**을 가지고 있다. 
* 변수 선언과 초기화, 함수 선언, 컬렉션 조작 등이 간단하고 명확하게 작성할 수 있다.
* 코틀린은 자바보다 더 간결하고 직관적이라, **쓰고 읽는 데 시간이 덜 걸린다**.
* 자바에 존재하는 여러 가지 번로운 준비 코드(생성자, 게터, 세터 등)들을 코틀린은 묵시적으로 제공하기 때문에 그런 준비코드 없이 더 깔끔하다.
* 기능이 다양한 표준 라이브러리를 제공하기 때문에 **반복되는 코드**를 줄일 수 있다.



## 안정성

* 실행 시점에 오류를 발생시키는 대신 **컴파일 시점 검사를 통해 오류를 더 많이 방지**해준다.

* 코틀린은 **null이 될 수 없는 값을 추적**하며, **실행 시점에 NullPointException이 발생할 수 있는 연산을 사용하는 코드를 금지**한다.
* 자바에서 객체의 null을 다루는데 사용되는 많은 코드라인을 생략할 수 있다.



## nullalbe type

* **자바에서는 변수에 null을 할당**할 수 있고, 이로 인해 **NullPointerException**이 발생할 수 있다.

*  하지만 코틀린은 **type** 시스템을 통해 **null 안전성**을 제공하며, **변수의 타입에 null**을 허용할지 여부를 명시적으로 지정한다. 또한 널 포인터 예외를 방지하기 위해 특별한 문법과 기능을 제공한다.

* nullable이 아닌 변수에 null을 넣으면 컴파일 타임에 에러를 발생시킨다. (자바는 런타임에 NPE 발생)



## null 체크

* java에서는 NPE(Null Point Exception)를 방지하기 위해 Optional이나 catch를 이용해 짰던 방어로직을 아래와 같은 연산자로 대체할 수 있다.

```
💡 null safe operator (?.) : null 아님을 확인 후에 안전하게 호출함
💡 elvis operator (?:) : null에 대한 직접적인 처리
```



## 상호 운용성

* **Java와 100% 호환**되며, 기존 라이브러리를 활용할 수 있어서 기존의 자바 코드를 가능하면 최대한 활용할 수 있다.

* java 클래스를 kotlin 클래스에서, kotlin 클래스를 java 클래스에서 사용할 수 있다.
* 라이브러리가 어떤 api를 제공하던 간에 코틀린에서 그 api를 활용할 수 있다.



## 도구 친화

* Kotlin은 개발 도구인 ItelliJ IDE를 개발한 JetBrains가 설계한 언어라, 사용하고 있는 IDE intellij가 Kotlin을 더 잘 지원한다.
* intellij 15부터 코틀린 플러그인이 기본적으로 포함되어 있다.