---
layout: post
title: subcategory - test2
image: /assets/img/me/coding.png
accent_image: 
  background: url('/assets/img/me/keepgoing.png') center/cover
  overlay: false
accent_color: '#ccc'
theme_color: '#ccc'
description: >
  Version 9.1 provides minor design changes, new features, and closes multiple issues.
invert_sidebar: true
categories :
 - subcategory
 - test2
---

# sub-cat-post2 



* toc
{:toc}


## 1)예외처리하기

Try-catch문은 예외를 처리하기 위한 구문이다. 

try-catch문의 기본 구조 
~~~java
try { //예외발생할 가능성이 있는 문장 
}catch(Exception1 e1) { //Exception1이 발생했을 경우, 이를 처리하지 위한 문장적는다. //보통 이곳에 예외메세지를 출력하고 로그로 남김. 
}catch(Exception2 e2) { //Exception2이 발생했을 경우, 이를 처리하지 위한 문장적는다. 
}catch(ExceptionN eN) { //ExceptionN이 발생했을 경우, 이를 처리하지 위한 문장적는다. 
}finally{ //예외발생여부에 관계없이 상항 수행되어야 하는 문장적는다. }
~~~

try 문에서 Exception 예외가 발생할 경우 catch (Exception e) 로 빠져서 그 안의 실행문을 실행한다.

마지막의 finally블럭은 try-catch문과 함께 예외발생 여부과 관계없이 "항상. 무조건" 실행되어야할 코드를 적는다.

필수는 아니며 마지막에 선택적으로 덧붙여 사용한다.

예외 발생시 try->catch->finally 순으로,  발생 하지 않은 경우 try->finally 순으로 실행된다.  

 

*finally 블록은 어떤 경우에 사용할까?

 보통은 자원이나 DB에 커넥션 한 경우, 파일 닫기, 연결 닫기(close) 등과 같은 "정리"코드를 넣는 데 사용된다.



## try-catch문 플로우 
- 예외가 try 블럭에서 발생한 경우

 발생한 예외와 일치하는 catch 문이 있는지 확인. 
 일치하는 catch 문이 있다면 catch 블럭 내의 문장을 모두 실행하고 try catch 문을 빠져나가서 그다음 문장을 수행.
 일치하는 catch 문이 없다면 예외는 처리되지 못하고 에러 발생.
- 예외가 try 블럭 안에서 발생하지 않은 경우

  1. catch블럭을 거치지 않고 전체 try-catch문을 빠져나가서 수행을 계속한다. 

 

- 예외가 try 블럭 밖에서 발생한 경우

 예외는 아무 처리되지 못한 채 에러 발생.
Try-catch블럭에서 예외 발생시, 예외가 발생한 위치 이후에 있는 try블럭의 문장들은 수행되지 않으므로, try블럭에 포함시킬 코드의 범위를 잘 선택해야한다. 

## catch 블럭 
)와 블럭{} 두부분으로 나눠져있는데, 괄호에는 처리하고자하는 예외타입(Exception), 참조변수(e)를 선언한다.

예외발생시 발생예외에 해당하는 클래스의 인스턴스가 만들어진다.

예를 들어 AuthException이 발생한다고 하면 AuthException인스턴스가 생성된다. 

try블럭내에서 이 예외가 발생했다면, 이를 처리할 수 있는 catch 블럭이 있는지 찾는다. 

예시 catch블럭 )
~~~java 
catch (AuthException e) { e.printStackTrace(); //예외정보 출력 
log.error("AuthException ERROR: {} ", e.getMassage()); //로그남김 
throw e; //예외 던지기 
} catch (Exception e ) { 
  e.printStackTrace(); 
  log.error("Exception ERROR: {} ", e.getMassage()); 
  throw e; 
  }
~~~

 이때, AuthException 을 처리하는 catch블럭이 없다면, 예외가 처리되지 못하고 에러를 발생시키기 때문에
 모든 예외클래스는 Exception클래스의 자손이므로, catch블럭 괄호에 Exception e 를 선언해 놓으면 
 어떤 종류의 예외가 발생하더라도 이 catch블럭에 의해서 처리가 된다. 마치 if-else 문의 else 부분이라고 볼 수 있다.
 그래서 보통 마지막 catch블럭에 Exception e를 선언한다. 
 예시같은 경우에는 두번째 catch블럭에서 AuthException을 제외한 모든 예외가 처리되는 것이다.


## 2)예외 던지기
* throw e

: 예외 던지기 (발생시키기)

throw 키워드를  사용하여 프로그래머가 고의로 예외를 발생시킬수 있다.

 

예외던지기 플로우 

1. try안에서 연산자 new를 이용해서 발생시키려는 예외클래스의 객체생성.

2. 키워드 throw를 사용해서 생성한 예외를 catch로 던진다. 

3. catch 에서 던진 예외를 잡아서 확인 또는 처리한다. 


examle)
```java 
public static void main (String[] args) {
   try { 
     Exception e = new Exception("고의발생"); // 1. 예외 생성 
       throw e; // 2. 예외 던지기 
     } catch (Exception e) { 
       System.out.println("에러메세지:" + e.getMessage()); e.printStackTrace(); //예외정보 출력 
       } System.out.println("프로그램 정상 종료."); }
```
result) 
```c
에러메세지: 고의발생 java.lang.Exception: 고의발생 at ExceptionEx9.main(ExceptionEx9.java:4) 프로그램 정상 종료.

```