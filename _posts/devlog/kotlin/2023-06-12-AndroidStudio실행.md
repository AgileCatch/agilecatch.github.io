---
layout: post
title: 코틀린 배우기
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
 - kotlin

---

# 5 앱을 만들어 실행하기

에뮬레이터를 생성하고 연결하는 방법과 스마트폰을 연결하는 방법을 알아보아요!



* toc
{:toc}


---



## 1) 에뮬레이터 생성 및 실행하기

- 프로그램을 만든 후 매번 스마트폰에 올려 테스트하려면 꽤 귀찮다.

- 에뮬레이터는 한 시스템에서 다른 시스템을 복제해서원본 시스템을 그대로 재현해주는 것을 말한다. (일종의 가상 환경)

- 안드로이드 스튜디오에도 에뮬레이터가 있어서 스마트폰이 없어도 작성한 코드를 테스트 할 수 있다.

1. 안드로이드 스튜디오의 상단 툴바에서 아래 그림과 같이 Device Manager를 클릭해 실행한다.

![img](https://190938973-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2Fa4oGyVd5h5iQeplBqkqY%2Fuploads%2FevN8N6iE52dWHGysbLYL%2Fimage.png?alt=media&token=14290f67-9e66-4877-b635-fe398073618e)

2. Create Device를 클릭한다.

![img](https://190938973-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2Fa4oGyVd5h5iQeplBqkqY%2Fuploads%2FQYIWCIhyubdP9PNPY9Fc%2Fimage.png?alt=media&token=912d439f-41b1-4837-b01b-7060991b04d3)

3. 원하는 기기를 선택한 후 "Next"를 클릭한다. 다음 화면에서 원하는 Android 버전을 선택한다.

![img](https://190938973-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2Fa4oGyVd5h5iQeplBqkqY%2Fuploads%2FTJeRgPj5NgLyyYiLEMGw%2Fimage.png?alt=media&token=22168109-67f6-47f9-9546-e33e410ebbab)

4. 시스템 이미지를 다운로드 한다.

![img](https://190938973-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2Fa4oGyVd5h5iQeplBqkqY%2Fuploads%2FLicfQ7ZvlEJrvhxvQDuc%2Fimage.png?alt=media&token=a0636f40-3973-40db-9b2a-7d92c712670e)

5. 다운로드가 완료되면 "Next"를 클릭하고 "Finish"를 클릭한다.

![img](https://190938973-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2Fa4oGyVd5h5iQeplBqkqY%2Fuploads%2Feqp7UarjAF8tXZiIL2ig%2Fimage.png?alt=media&token=04cd54ff-69aa-48ec-b243-a0a68e99d0a0)

6. 설치가 완료되면 아래 그림과 같이 목록에 새롭게 설치한 에뮬레이터 목록이 뜬다. 여기서 "플레이" 버튼을 눌러 에뮬레이터를 실행한다.

![img](https://190938973-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2Fa4oGyVd5h5iQeplBqkqY%2Fuploads%2FW6YP8FN79xFrSSGe7Rdr%2Fimage.png?alt=media&token=0a443d81-d656-4393-9c72-8dc0f09d3848)

7. 에뮬레이터가 실행된 화면이다.

![img](https://190938973-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2Fa4oGyVd5h5iQeplBqkqY%2Fuploads%2F9CiATRmS7My45qo1DwCs%2Fimage.png?alt=media&token=d928cc4a-089d-4eaf-956d-be3dd27e52c3)



## 2) 스마트폰 설정 및 연결하기

- 스마트폰에 연결하기 위해서는 설정 화면에 있는 빌드 번호가 적힌 메뉴를 클릭하여 스마트폰의 개발자 옵션(Developer Options)을 활성화해야 한다.

- 스마트폰마다 화면 모양, 설정 메뉴의 위치 등 편차가 크기 때문에 화면으로 설명하기 보다는 메뉴의 이름으로 설명하겠다.

#### 여기서 잠깐!

- 에뮬레이터에서 개발자 모드 설정

  - 에뮬레이터에서 개발자 모드를 설정하려면 아래 1~4 스텝을 에뮬레이터에서 진행하면 된다.

- 에큘레이터에서 [빌드 번호] 위치는 보통 다음 순서대로 따라가면 찾을 수 있다.

  - [설정] - [에뮬레이트된 기기 정보] - [빌드 번호]

1. 스마트폰을 켜고 [설정(Settings)] 아이콘을 눌러 이동한다.
2. [설정] 화면에서 [휴대전화 정보]를 눌러 이동한다.
3. [휴대전화 정보]에서 아래로 내려가면 [빌드 번호]를 찾을 수 있다. 이 빌드 번호를 5회 이상 연속해서 누르면 개발자가 되었다는 메시지가 나온다.
4. 다시 [설정] 화면에서 [시스템]-[{ }개발자 옵션]을 클릭해 화면으로 이동한다.
5. 그런 다음 [USB 디버깅] 옆의 스위치 버튼을 눌러 활성화 해준다.
6. USB 케이블을 이용해 스마트폰을 컴퓨터에 연결한다.



## 3) 앱 만들어 실행하기: Say! Hello~

- 본격적으로 앱을 만들어 실행해보겠다.

- 앱을 만들어 실행하는 과정은 크게 4단계로 진행된다.

1. 프로젝트 생성하기
2. 레이아웃 편집하기
3. 소스 코드 연결하기
4. 앱 실행하기

### 1단계: 프로젝트 생성하기

- "New Project"를 클릭한다.

![img](https://190938973-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2Fa4oGyVd5h5iQeplBqkqY%2Fuploads%2FsbISGLGaCczcLM9PFyEP%2Fimage.png?alt=media&token=a81ffde1-bf45-4a90-ad79-a0631cdd8a79)

- Empty Views Activity를 클릭한다.

![img](https://190938973-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2Fa4oGyVd5h5iQeplBqkqY%2Fuploads%2FXsrz2sVXHEQYoEzDpi75%2Fimage.png?alt=media&token=b2982400-29ec-4bd8-98c8-e1535a092aa7)

- Name에는 원하는 프로젝트 이름, Package name은 소문자로, Language는 Kotlin으로 설정한다.

![img](https://190938973-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2Fa4oGyVd5h5iQeplBqkqY%2Fuploads%2FXBmdrpD6keocQxmGOtKA%2Fimage.png?alt=media&token=0d9844b7-ed93-48c5-b918-b1ca25e22ec1)

- 위 그림에서 Name은 프로젝트명이다. 이 프로젝트의 이름은 MyFirstApplication이다.

- 위 그림에서 Package name은 패키지명이다.

  - 패키지명은 애플리케이션 ID이며 나중에 변경할 수 있다.

  - 패키지명은 꼭 소문자로 입력해야 한다.

- 위 그림에서 Save location은 프로젝트를 저장할 위치이다. 각자 다를 수 있다.

- 위 그림에서 Language는 프로젝트에 사용할 언어를 선택하는 부분이며 **꼭 Kotlin으로 설정**한다.

- 위 그림에서 Minimum **SDK는 21**로 설정하였다.

여기서 잠깐!

- 패키지명(Package name)에 example을 포함할 경우 플레이 스토어에 업로드 할 수 없다.

- 반드시 com.회사명 또는 본인이름.앱이름 형태로 작성해야 한다. (위 그림에서의 패키지명은 단순히 예제 앱을 만들어보기 위함이며 스토어에 등록하는 것이 아니기에 com.example.myfirstapplication으로 작성하였다.)



- 프로젝트 생성된 화면이다.

![img](https://190938973-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2Fa4oGyVd5h5iQeplBqkqY%2Fuploads%2F3DqqE2EJi9CGUs06k63Q%2Fimage.png?alt=media&token=d7046e16-dfab-4e3e-a887-139b85d14f15)

### 2단계: 레이아웃 편집하기

- 레이아웃은 텍스트나 이미지 등을 화면에 배치할 수 있는 도구이다.

- 프로젝트가 생성되면 위 그림과 같이 기본 화면이 나타나는데 편집기 창 상단에 보이는 파일명으로 된 탭을 선택하면 레이아웃 편집기로 이동할 수 있다.

- 파일의 확장자에 따라서 .kt 파일은 코드 편집기가 열리고, .xml 파일은 레이아웃 편집기가 자동으로 선택되어 열린다.

#### 여기서 잠깐!

- 화면을 그려주는 함수 setContentView

```kotlin
super.onCreate(savedInstanceState)
setContentView(R.layout.activity_main)
```

- 코드 편집기 창을 보면 setContentView(R.layout.activity_main)라는 코드가 보인다.

- 이는 '콘텐츠를 화면에 표시하기 위해서 res/layout 디렉터리 아래에 있는 activity_main.xml 파일을 사용한다'라는 의미이다.



- 이제 activity_main.xml 탭을 클릭해서 화면을 설정할 수 있는 파일을 열어보자.

- 편집기 창이 레이아웃을 편집할 수 있는 형태로 바뀐다.

- 우측 상단에 있는 모드 버튼을 클릭하면 [Code], [Split], [Design] 모드로 변경되면서 각각의 모드에서 편집이 가능하다.

![img](https://190938973-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2Fa4oGyVd5h5iQeplBqkqY%2Fuploads%2FjgSt00krKvxSMzlXO0f7%2Fimage.png?alt=media&token=c22316b5-fe01-4ee7-a9a5-ea338cfbdd79)

[Code] 모드



![img](https://190938973-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2Fa4oGyVd5h5iQeplBqkqY%2Fuploads%2FZixE9AvNE25gJn3RnKhm%2Fimage.png?alt=media&token=c3336b08-0ecf-40fc-8618-c7b78a77143a)

[Split] 모드



![img](https://190938973-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2Fa4oGyVd5h5iQeplBqkqY%2Fuploads%2F3NyWd2DQEwsJsXv7IsXZ%2Fimage.png?alt=media&token=97bda188-a865-4691-b06b-1d434c6522ca)

[Design] 모드

- [Design] 모드를 선택면 좌측 상단의 팔레트(Palette) 영역에 있는 커먼(Common) 카테고리를 클릭한다.

- 그리고 우측에 보이는 버튼(Button)을 드래그해서 화면 중앙의 'Hello World!'라는 글자 아래에 가져다 놓는다.

![img](https://190938973-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2Fa4oGyVd5h5iQeplBqkqY%2Fuploads%2FoG18aW33fyNJ7rVJxCWr%2Fimage.png?alt=media&token=b629521d-43c2-4382-808e-77f047e6a585)

- 컨스트레인트 편집기 위쪽에 있는 + 아이콘을 클릭하면 'Hello World!'가 쓰여 있는 TextView에 버튼의 레이아웃이 연결되고, 편집 화면이 다음 우측 그림과 같이 바뀐다.

![img](https://190938973-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2Fa4oGyVd5h5iQeplBqkqY%2Fuploads%2FTVVeI8e33UTEtbqtCHNE%2Fimage.png?alt=media&token=7c7159a1-7e77-44ee-9eb4-5d217a3e0cfd)

![img](https://190938973-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2Fa4oGyVd5h5iQeplBqkqY%2Fuploads%2FWU2FLNfdyNIHieZion73%2Fimage.png?alt=media&token=558f43c0-e2b0-45e7-934a-b63847a28ad8)

#### 여기서 잠깐!

- Constraint 편집기 숫자의 의미

  - 편집기에서 클릭한 + 위의 숫자는 현재 연결된 요소와의 거리를 나타낸다.

  - 예를 들어 위 그림에서 표시된 "44"라는 숫자는 44dp(Device independence Pixel)만큼 떨어져 있다는 의미이다.



- 컨스트레인트 편집기에서 좌 우측에 있는 +를 클릭한다. 편집기 화면이 다음의 좌측 그림과 같이 연결된 형태로 바뀌고, 디자인 화면에서도 버튼의 양쪽으로 화살표가 화면 끝까지 이어진다.

  ![img](https://190938973-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2Fa4oGyVd5h5iQeplBqkqY%2Fuploads%2F6oKbEZsCuogN9FFoIZTW%2Fimage.png?alt=media&token=961cf6cf-8e8d-465f-bafd-394b5838e6b9)

  ![img](https://190938973-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2Fa4oGyVd5h5iQeplBqkqY%2Fuploads%2FEsL79hSkUjqhMCyvuDBL%2Fimage.png?alt=media&token=6696fc42-9ea2-4102-a243-123db8dead32)



- 이번에는 컨스트레인트 편집기에서 좌 우측의 값을 0으로 바꿔보도록 하겠다. 그리고 layout_width를 0dp로 바꿔준다. (버튼의 영역이 화면(가로)을 꽉 채워진 것을 확인할 수 있다.)

![img](https://190938973-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2Fa4oGyVd5h5iQeplBqkqY%2Fuploads%2FmeW2io6NIFJ1LJ7wbAed%2Fimage.png?alt=media&token=19f65e3a-3534-4440-aec0-4978e54780d6)

![img](https://190938973-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2Fa4oGyVd5h5iQeplBqkqY%2Fuploads%2FgUVLdaZ367mcBja1zREE%2Fimage.png?alt=media&token=b897e818-5566-4881-a99d-53399ea5e797)



#### 여기서 잠깐!

- 컨스트레인트의 세 가지 모드

  - Wrap Content: 위젯 안쪽의 내용물에 크기를 맞춘다.

  - Fixed: 원하는 값(위 그림에서 위쪽 컨스트레인트 값을 44로 설정)을 입력하여 가로 세로 속성 필드에 입력된 크기에 맞게 가로세로를 고정한다.

  - Match Constraint: 0dp로 설정하여 크기를 제약 조건인 Constraint 연결부에 맞춘다.

  

## 4) 코틀린 코드와 레이아웃 연결하기

- 위에서 레이아웃을 만들었는데 이렇게 만들어진 레이아웃이나 사용자에게 보이는 것들을 통칭해서 뷰(View)라고 한다.

- 이렇게 만들어진 뷰에서 버튼 같은 요소를 동작시키기 위해서는 먼저 뷰와 소스 코드를 연결해야 하는데, 안드로이드는 findViewById라는 함수를 제공하고 있으며 이를 조금 효율적으로 사용하기 위해서 코틀린에서는 코틀린 익스텐션(Kotlin Extensions)이라는 부가 기능을 제공한다.

- 하지만 코틀린 익스텐션은 다음과 같은 이유로 최신 버전의 안드로이드 스튜디오에서는 사용월 권장하지 않는다.

  - 코틀린에서만 제공하므로 자바에서는 사용할 수 없다.

  - 일부 상황에서 뷰를 찾을 수 없는 오류가 발생한다.

  - 어디서나 뷰를 호출할 수 있기 때문에 잘못된 참조로 인해 앱이 강제 종료될 수 있다. 예를 들어 activity_main.xml과 fragment_sub.xml에서 동일하게  button 아이디를 사용하면 실수로 다른 XML의 아이디를 참조하여 앱이 강제로 종료될 수도 있다.

  - 모듈화를 추천하고 있는데 코틀린 익스텐션을 사용할 경우 다른 코드에서 뷰에 대한 접근이 불가능하다.

-  뷰 바인딩 방식을 사용해서 뷰와 코드를 연결하는 방법을 공부해보겠다.

- 뷰 바인딩을 사용하는 방법을 간략하게 보고 바로 실습해보겠다.



1. build.gradle(Module: app) 파일에 viewBinding 설정을 추가한다.

![img](https://190938973-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2Fa4oGyVd5h5iQeplBqkqY%2Fuploads%2F7AybyB4kBjNrxMuKiMRu%2Fimage.png?alt=media&token=bf86ad45-177c-479a-bcee-e499bf2a8882)

2. 파일 상단에 나타나는 [Sync Now]를 클릭해서 설정을 적용한다.

![img](https://190938973-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2Fa4oGyVd5h5iQeplBqkqY%2Fuploads%2FCnQ87hiYHXmhGdJ94n5B%2Fimage.png?alt=media&token=0609fb4d-9ada-4e30-a39a-c4ca81221d0a)

3. activity_main.xml 레이아웃 파일을 작성한다.

4. viewBinding이 설정되어 있기 때문에 안드로이드가 레이아웃 파일을 바인딩으로 생성한다. 

- 자동변환 공식: 레이아웃 파일명(첫 글자와 언더바 다음 영문을 대문자로 변환) + Binding

- 예) activity_main.xml = ActivityMainBinding



- 이제 MainActivity.kt 파일을 다음과 같이 작성한다!

```kotlin
package com.example.myfirstapplication

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import com.example.myfirstapplication.databinding.ActivityMainBinding

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        val binding = ActivityMainBinding.inflate(layoutInflater)
        setContentView(binding.root)
    }
}
```

**[주요 변경사항]**

```kotlin
val binding = ActivityMainBinding.inflate(layoutInflater)
setContentView(binding.root)
```

- 바인딩 변수를 통해 뷰에 미리 작성해두었던 버튼의 id에 접근할 수 있다. 다음과 같이 버튼의 id에 리스너(Listener)를 설정한다. 리스너의 역할은 버튼을 클릭 했을 때 내부의 코드를 동작시키는 것이다.

```kotlin
binding.button.setOnClickListener { }
```

- 버튼을 클릭하였을 때 TextView의 문구를 바꿔보자! 아래 코드를 작성해주자.

```kotlin
binding.button.setOnClickListener{
    binding.textView.text = "Hello Kotlin!!!" // 버튼을 클릭하면 TextView의 문구가 변경됩니다.
}
```

```kotlin
package com.example.myfirstapplication

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import com.example.myfirstapplication.databinding.ActivityMainBinding

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        val binding = ActivityMainBinding.inflate(layoutInflater)
        setContentView(binding.root)

        binding.button.setOnClickListener {
            binding.textView.text = "Hello Kotlin!!!"
        }
    }
}
```



## 5) 앱 실행하기

![img](https://190938973-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2Fa4oGyVd5h5iQeplBqkqY%2Fuploads%2FGYTesVM731bJQwW5lP9e%2Fimage.png?alt=media&token=1db2dde0-3ddb-4742-ae78-fd13ddcb23a2)

- 이제 작성한 코드를 에뮬레이터에서 실행해보겠다. (플레이 버튼을 클릭하여 실행한다. = F5버튼도 가능)

- 앱이 실행되고, 버튼을 클릭하면 문구가 바뀌는 것을 확인할 수 있다.

![img](https://190938973-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2Fa4oGyVd5h5iQeplBqkqY%2Fuploads%2FofSEGRLsre11WRydRuf1%2F1.png?alt=media&token=5a11883f-1b51-4e78-ad1a-326801e1b7ab)

![img](https://190938973-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2Fa4oGyVd5h5iQeplBqkqY%2Fuploads%2FwKcWidUyDHXEb5lxdrRV%2F2.png?alt=media&token=fb91caab-aafe-4f2f-9fd6-f2ab56aaafa3)

- (아래 좌측: 앱 초기 실행 상태) --> (아래 우측: 앱 내 Button을 클릭한 뒤의 상태)



다음시간에서는 코틀린 사용을위한 기본문법에대해서 공부 해보겠다!
