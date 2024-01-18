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

# [Kotlin] Scope functions의 정의와 사용 방법

* toc
{:toc}
---

# Scope functions이란?

**Scope functions**는 객체의 범위(scope) 내에서 코드 블록을 실행할 수 있게 하는 함수이다.

**let, run, with, apply, also** 등이 있으며, 이 함수들은 객체의 속성에 접근하거나 객체를 다르게 처리하는데 유용하다.

이 스코프는 객체의이름을 사용하지 않고 **it,this**등을 통해 객체에 접근이 가능하다.

| Function | Object reference | Return value     | Is extension function                       |
| :------- | :--------------- | :--------------- | :------------------------------------------ |
| `let`    | `it`             | Lambda result    | Yes                                         |
| `run`    | `this`           | Lambda result    | Yes                                         |
| `run`    | -                | Lambda result    | No: called without the context object       |
| `with`   | `this`           | Lambda result    | No: takes the context object as an argument |
| `apply`  | `this`           | Object reference | Yes                                         |
| `also`   | `it`             | Object reference | Yes                                         |

위 표를 살펴보면 2가지로 분류되는것을 알 수 있는데

* Object reference 가 `it` 인가  `this`인가
* 반환값이 `Object reference` 인가 `Lambda result` 인가

이 값들중 특이하게 with가 남게되는데 여러 동작들을 어떤상황에서 사용하는지 알아보자



## 1) with

`with` 은 이미 생성된 객체에 대해 일관적인 작업을처리할때 유용하다.

##### with를 사용할때

```kotlin
private fun initView() = with(binding) {
        //viewpager adapter
        viewPager.adapter = viewPagerAdapter
        //viewpager slide
        viewPager.isUserInputEnabled=false
       }
```

##### with를 사용하지 않을때

```kotlin
private fun initView() {
        //viewpager adapter
        binding.viewPager.adapter = viewPagerAdapter
        //viewpager slide
        binding.viewPager.isUserInputEnabled=false
       }
```

* 본인은 **binding**을 사용할때 `with`를 사용했었는데 xml의 Id값을불러올때 반복되는 코드를 줄이기위해 `with`로 정해줬다.

* 이값은 **this**로 참조할 수 있고 내가 사용한 방법처럼 **this**를 생략할 수도 있다.

```kotlin
val person = Person()
val result = with(person) {
    name = "John"
    age = 30
    "$name is $age years old."
}

println(result) // 출력: John is 30 years old.

```

* 위와같이 `with`를 사용했을때 반환 값이 **Lambda result** 이기때문에 마지막라인에 다른 데이터를 추가하면 이값이 반환된다.



## 2) apply

`apply`는 객체의 초기화 블록으로 사용되며, 객체 자체를 반환한다.

```kotlin
data class Car(var brand: String, var model: String, var year: Int)

val myCar = Car("Toyota", "Camry", 2022).apply {
    year = 2023
    model = "Corolla"
}

println(myCar) // 출력: Car(brand=Toyota, model=Corolla, year=2023)

```

* `with` 은 인자로 context object 를 받지만, `apply` 는 extension function 이기 때문에 객체를 생성해서 **할당하기 전**에 사용이 가능하다. 

* `apply` 코드 블록이 모두 수행된 후 인스턴스가 할당되기 때문에 `apply` 는 **객체 생성시점에서 초기화를 할 때** 유용하다.



## 3) also

`also` 는 객체를 람다에 전달하고 그 객체를 반환한다. 

주로 부수 효과를 일으키는 작업에 사용된다.

```kotlin
val numbers = mutableListOf(1, 2, 3)

numbers.also {
    it.add(4)
    println("List after adding 4: $it") // 출력: List after adding 4: [1, 2, 3, 4]
}.removeAt(1)

println("List after removing element at index 1: $numbers") // 출력: List after removing element at index 1: [1, 3, 4]

```

* `apply` 와 유사해 보이는데 차이점은 `apply` 는 Lambda function 에 인자를 넘겨주지 않기 때문에 `this`를 이용해 참조한다. 
* 그에 반해 `also`는 Lambda function 에 인자를 넘겨주기 때문에 인자를 `it` 이나 다른 이름을 부여해 참조가 가능하다.



## 4) run

`run`은 수신 객체에 람다를 실행해 결과를 반환하고 this를 사용한다.

```kotlin
val message = run {
    val greeting = "Hello"
    val name = "Kotlin"
    "$greeting, $name!"
}

println(message) // 출력: Hello, Kotlin!
```

* `with`와 유사하지만 객체를 생성해서 할당하기전에 사용이 가능하다는점이 다르다.

```kotlin
val nameDoubleLength = Person.withDefaultName()
    .run { name.length * 2 }
```

* 객체를 변수로 할당할 필요 없이 필요한값만 바로 반환받을 수 있다.

```kotlin
val nameDoubleLength = person?.run { name.length * 2 }
    ?: 0
```

* Null 회피용도로도 사용할 수 있다.



## 5) let

`let`  은 주어진 블록을 호출하고, 결과를 반환할때 주로 사용한다.

```kotlin
val length: Int? = "Hello, Kotlin".let {
    println(it) // 출력: Hello, Kotlin
    it.length
}

println("문자열 길이: $length") // 출력: 문자열 길이: 13

```

