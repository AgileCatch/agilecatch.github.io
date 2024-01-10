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
 - android

---

* toc
{:toc}
---

# [Kotlin] Retrofit과 Retrofit2의 차이

오늘은 레트로핏에대해 공부해 볼 것이다.

## 1) Retrofit

 **레트로핏**은 안드로이드 앱에서 네트워크 통신을 간편하게처리할 수 있도록 도와주는 오픈소스 라이브러리다.

* 주로 **`HTTP` 기반의 `RESTful API`와 통신**하기 위해 사용되며, 서버로부터 데이터를 받아오거나 서버에 데이터를 전송하는 등의 작업을한다.
* 레트로핏을 사용하면 앱에서 서버와의 통신을 간편하게 처리할 수 있다.
*  자동으로 데이터를 매핑하고 **비동기적으로 작업**을 수행할 수 있도록 도와준다.

주로 `RESTful API`를 사용하는 앱에서 서버와통신을 단순화하고 효율적으로 구현할 수 있도록해준다.

```
💡 레트로핏은 안드로이드 앱에서 RESTful API와 통신하기 위한 도구로 사용되는 라이브러리일 뿐이며, RESTful API 자체는 웹 서비스를 설계하는 아키텍처 원칙을 나타낸다.
```



## 2) Retrofit2

*  **OkHttp**를 사용하여 네트워크 통신을 처리한다.
* 콜 어댑터를 사용하여 비동기적인 콜백 처리를 더욱 쉽게 할 수 있도록 지원한다.
* 기본적으로 null 값을 허용하도록 설계되어 있어, 서버 응답에 필드가 없는 경우 해당 필드는 null로 채워진다.



### 간단한 예제

1. **의존성 추가:** `build.gradle` 파일에 Retrofit2 및 Gson 라이브러리 의존성을 추가한다.

```
kotlinCopy code
// build.gradle 파일에 dependencies 블록에 아래의 의존성을 추가합니다.
implementation "com.squareup.retrofit2:retrofit:2.9.0"
implementation "com.squareup.retrofit2:converter-gson:2.9.0"
```

2. **데이터 클래스 생성:** 서버 응답을 매핑할 데이터 클래스를 정의한다.

```
kotlinCopy code
data class Post(
    val userId: Int,
    val id: Int,
    val title: String,
    val body: String
)
```

3. **API 서비스 정의:** Retrofit2를 사용하여 통신할 API 서비스를 정의한다.

```
kotlinCopy code
import retrofit2.Call
import retrofit2.http.GET
import retrofit2.http.Path

interface ApiService {
    @GET("posts/{id}")
    fun getPostById(@Path("id") postId: Int): Call<Post>
}
```

4. **Retrofit 객체 생성 및 API 서비스 사용:**

```
kotlinCopy code
import retrofit2.Retrofit
import retrofit2.converter.gson.GsonConverterFactory

fun main() {
    // Retrofit 객체 생성
    val retrofit = Retrofit.Builder()
        .baseUrl("https://jsonplaceholder.typicode.com/")
        .addConverterFactory(GsonConverterFactory.create())
        .build()

    // API 서비스 생성
    val apiService = retrofit.create(ApiService::class.java)

    // 비동기 처리
    val call: Call<Post> = apiService.getPostById(1)
    call.enqueue(object : retrofit2.Callback<Post> {
        override fun onResponse(call: Call<Post>, response: retrofit2.Response<Post>) {
            if (response.isSuccessful) {
                val post: Post? = response.body()
                // 서버 응답 처리
                if (post != null) {
                    println("Post Title: ${post.title}")
                    println("Post Body: ${post.body}")
                }
            } else {
                // 에러 처리
                println("Error: ${response.code()}")
            }
        }

        override fun onFailure(call: Call<Post>, t: Throwable) {
            // 통신 실패 처리
            println("Failed to execute the request: ${t.message}")
        }
    })
}
```



## 3) Retrofit과 Retrofit2의 차이점

한줄로 정리하면 

Retrofit2는 Retrofit의 업그레이드된 버전으로 

OkHttp를 기본적으로 통합하고 RxJava를 지원하여 네트워크 통신을 더욱 효율적으로 처리할 수 있게 해주는 HTTP 클라이언트 라이브러리이다.
