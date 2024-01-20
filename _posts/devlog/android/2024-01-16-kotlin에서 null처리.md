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

# [Kotlin] Kotlin에서 null처리 방법

* toc
{:toc}


---

## 1) **Nullable type**

```kotlin
var name: String? = null
```

* **Nullable 타입이란** 선언변수 또는 반환 타입에 `?`를 붙여 **Nullable** 타입을 선언한다. 
  * 💡 Nullable 타입은 **해당 변수 또는 표현식이 null일 수 있다**는 것을 나타낸다.
  * `?` 를 붙임으로써 null이 가능한 변수임을 명시적으로 표현한다. 
* **자바에서는 변수에 null을 할당**할 수 있고, 이로 인해 **NullPointerException**이 발생할 수 있다.
* 하지만 코틀린은 **type** 시스템을 통해 **null 안전성**을 제공하며, **변수의 타입에 null을 허용할지 여부**를 명시적으로 지정한다. 
* **nullable**이 아닌 변수에 **null**을 넣으면 컴파일 타임에 에러를 발생시킨다. (자바는 런타임에 NPE 발생)



## 2) **?. (Null safe operator)**

  ```kotlin
  val length = name?.length
  ```

* **안전 호출 연산자란** Nullable 객체의 프로퍼티나 메서드에 접근할 때, Null을 안전하게 처리하기위해 `?.` 연산자를 지원한다. 
* 이 연산자는 객체가 **null이 아닌 경우에만 접근**을 시도하고, **null인 경우에는 null을 반환**한다.




## 3) **?: (Elvis operator)**

  ```kotlin
  val length = name?.length ?: 0
  ```

- **엘비스 연산자란** Nullable 객체가 null인 경우, 엘비스 연산자를 사용하여 기본값을 지정할 수 있다. 

- 엘비스 연산자는 **Nullable 객체가 null인 경우**, **우측에 있는 기본값을 반환**한다.

- 생긴게 엘비스 프레슬리 헤어를 닮았다고 해서 붙여진 이름이란다.



## 4) **as? (Safe cast)**

  ```kotlin
  val number: Any? = "123"
  		val intValue: Int? = number as? Int
  ```

- **안전한 캐스트란 **Nullable 객체를 캐스트할 때, 안전한 캐스트를 사용하여 **캐스트가 실패할 경우 null을 반환**한다.



## 5) **Non-null**

- **Non-null이란**  단언 Nullable 객체를 Non-null 타입으로 강제로 캐스트한다. 
- 이 연산자는 객체가 null인 경우 **NullPointerException**을 발생시킬 수 있으므로 주의해야 한다.
