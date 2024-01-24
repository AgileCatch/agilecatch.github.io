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

# [Android] 코틀린의 Interface 와 자바의 Interface차이

* toc
{:toc}
인터페이스(Interface)는 객체지향 프로그래밍에서 다양한 클래스가 공통적으로 가지는 메소드의 집합을 정의하는 추상회된 형식이다. 또한 **다중 상속**을 지원하기위한 메커니즘중 하나로 사용된다. 

## **1 자바에서의 인터페이스 정의**

```java
javaCopy code
// ExampleInterface.java
public interface ExampleInterface {
    void doSomething();  // 추상 메소드
    int calculate(int x, int y);  // 추상 메소드
}
```

> 위의 예제에서 `ExampleInterface`는 두 개의 추상 메소드를 정의하고 있다.

### 1) 인터페이스를 구현하는 클래스

```java
javaCopy code
// ExampleClass.java
public class ExampleClass implements ExampleInterface {
    @Override
    public void doSomething() {
        System.out.println("Doing something!");
    }

    @Override
    public int calculate(int x, int y) {
        return x + y;
    }
}
```

>  `ExampleClass`는 `ExampleInterface` 인터페이스를 구현하고 있다. 

* 클래스에서는 반드시 **인터페이스에 정의된 모든 메소드를 구현해야 한다**. 
* 여기서 `@Override` 어노테이션은 해당 메소드가 상위 클래스나 인터페이스에서 상속받은 것임을 나타낸다.

### 2) 인터페이스 활용

```java
javaCopy code
// MainClass.java
public class MainClass {
    public static void main(String[] args) {
        ExampleClass example = new ExampleClass();
        example.doSomething();
        int result = example.calculate(3, 5);
        System.out.println("Result: " + result);
    }
}
```

>  `MainClass`에서는 `ExampleClass`를 생성하고, 인터페이스에 정의된 메소드를 호출하는 예제이다.

* 인터페이스를 사용함으로써 다형성을 구현할 수 있다. 

* 여러 클래스가 동일한 인터페이스를 구현하면, 해당 인터페이스를 사용하는 코드에서는 어떤 구현체를 사용하더라도 통일된 방식으로 메소드를 호출할 수 있다.

## **2 코틀린과 자바의 Interface차이**

### 1) 자바에서의 인터페이스

#### a. 추상 메소드와 디폴트 메소드

- **추상 메소드 (Abstract Method):** 자바 인터페이스에서는 기본적으로 모든 메소드가 추상 메소드이다. 구현이 없이 메소드 시그니처만을 가지고 있다.

  ```java
  // 자바 인터페이스 예제
  public interface ExampleInterface {
      void abstractMethod();  // 추상 메소드
  }
  ```

- **디폴트 메소드 (Default Method):** Java 8부터 도입된 디폴트 메소드는 인터페이스에 **메소드의 기본 구현을 제공할 수 있게 해준**다. **구현체에서 이를 그대로 사용하거나 재정의**할 수 있다.

  ```java
  // 자바 인터페이스에 디폴트 메소드 추가
  public interface ExampleInterface {
      void abstractMethod();  // 추상 메소드
  
      default void defaultMethod() {
          System.out.println("Default implementation");
      }
  }
  ```

### 2) 코틀린에서의 인터페이스

#### a. 추상 메소드와 디폴트 구현

- **추상 메소드 (Abstract Method):** 코틀린에서도 인터페이스는 추상 메소드를 가질 수 있다. 하지만 **인터페이스의 메소드는 항상 기본적으로 추상적**이며, 명시적으로 `abstract` 키워드를 사용하지 않는다.

  ```kotlin
  // 코틀린 인터페이스 예제
  interface ExampleInterface {
      fun abstractMethod()  // 추상 메소드
  }
  ```

- **디폴트 구현 (Default Implementation):** 코틀린에서는 디폴트 구현이나 상태를 가진 메소드를 **인터페이스에서 직접 정의**할 수 있습니다.

  ```kotlin
  // 코틀린 인터페이스에 디폴트 구현 추가
  interface ExampleInterface {
      fun abstractMethod()  // 추상 메소드
  
      fun defaultMethod() {
          println("Default implementation")
      }
  }
  ```

#### b. 속성 (Properties)

- **속성 (Properties):** 코틀린에서는 인터페이스에서 추상적인 프로퍼티(속성)을 정의할 수 있다. 이는 자바에서의 인터페이스에서는 불가능하다.

  ```kotlin
  // 코틀린 인터페이스에 프로퍼티 추가
  interface ExampleInterface {
      val property: Int  // 추상 프로퍼티
  }
  ```

이렇게 자바와 코틀린에서의 인터페이스는 몇 가지 차이점이 있다. 

코틀린은 보다 간결하고 더 많은 기능을 지원하는 특성이 있으며, 특히 **디폴트 메소드와 프로퍼티 등을 인터페이스에서 지원**하는 것이 자바보다 다양한 활용을 가능케 한다.
