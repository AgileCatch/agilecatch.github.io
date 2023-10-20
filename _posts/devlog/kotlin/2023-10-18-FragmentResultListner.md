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

# [Kotlin] 프래그먼트 간 데이터 공유 : Fragment Result API

* toc
{:toc}
---

프로젝트 진행중 **Afragment**에서 **BFragment**를 통해 **Activity**의 값을 전달 받아야 하는 일이 생겼다.

**Afragment**에 글을 추가하는 동작을 구현하고 싶었는데 `Bottomseet`(**BFragment**)를 사용해 `Activity` 가 열리는 경우였기 때문에 복잡한 동작을 요구했다. (바텀시트를 통해 enum class type이 분리되어 들어가는데 이부분에서 `intent` 를 받아오는데 문제가 생김)

<img src="../../../assets/img/blog/fragment-a-to-b.png" alt="fragment-a-to-b.png" style="zoom:33%;" />

이러한 경우에 `viewmodel`을 사용할 수도 있었지만 `Fragment Result`를 통해 **TYPE** 을 받아오기로 하였다.

* [Developers : 프래그먼트와 통신]( https://developer.android.com/guide/fragments/communicate?hl=ko) 구글 공식 문서에서도 확인이 가능하다!
* **Fragment A - 결과 값을 받을 곳**
* **Fragment B - 결과 값을 보낼 곳**



## 1) 결과 값을 받을 Fragment A를 구현

```kotlin
setFragmentResultListener("requestKey") { requestKey, bundle ->
//결과 값을 받는곳입니다.
val result = bundle.getString("bundleKey")}
```

* **AFragment**에서 `setFragmentResultListener` 등록한다.
* **requestKey** : 동일한 `FragmentManager` 에 결과를 설정해주는 키
* **bundleKey** : 콜백을 받기위해 설정해주는 키



여기서 우리는 **requestKey**와 **bundleKey**를 잘 기억해 놓고 **FragmentB**  에서 사용해야한다.



## 2) setFragmentResultListener 동작 구현하기

```kotlin
fabAdd.setOnClickListener {
  					//FragmentB
            val teamAddCategory = TeamAddCategory()
            teamAddCategory.show(childFragmentManager, teamAddCategory.tag)

            setFragmentResultListener(FRAGMENT_REQUEST_KEY) { _, bundle ->
                Log.d("teamFragment","startActivity")
                when (bundle.getString(FRAGMENT_RETURN_TYPE)) {
                    TeamAddCategory.RETURN_TYPE_RECRUITMENT -> {
                        //결과값을 받고 동작할 내용
                        )
                        
                    }

                    TeamAddCategory.RETURN_TYPE_APPLICATION -> {
                        //결과값을 받고 동작할 내용
                        )
                      
                }
            
```

* **add button click**시 **FragmentB**(bottom seet) 올라오도록 하기 

* 본인은 FragmentB 를 바텀시트프래그먼트를 사용해서 2개의 버튼이 올라왔을때 같은 하나의 Activity에 다른 값이 들어가도록 구현 하고있다.

  

## 3) FragmentB에서 FragmentA로 Return값 설정하기

```kotlin
private fun initView() = with(binding) {
        // 여기서 Fragment Result Listener로 값을 return한다.
        btnRecruitment.setOnClickListener {
            //용병 모집
            setFragmentResult(FRAGMENT_REQUEST_KEY,bundleOf( FRAGMENT_RETURN_TYPE to RETURN_TYPE_RECRUITMENT))
            dismiss()
            Log.d("teamAddCaregory","close bottonsheet")
        }

        btnApplication.setOnClickListener {
            //용병 신청
            setFragmentResult(FRAGMENT_REQUEST_KEY,bundleOf(FRAGMENT_RETURN_TYPE to RETURN_TYPE_APPLICATION))
            dismiss()
            Log.d("teamAddCaregory","close bottonsheet")
        }
    }
```

* 바텀시트 프래그먼트에서 TeamFragment로 리턴할값을 설정하기 (본인은 타입값을 리턴해줌)
* **requestKey** : FRAGMENT_REQUEST_KEY
* **bundleKey** : FRAGMENT_RETURN_TYPE
* **Result** : RETURN_TYPE_RECRUITMENT -> 리턴할 값이다.



## 4) 콜백받은후 원하는 동작 구현해주기

```kotlin
private val addContentLauncher =
        registerForActivityResult(ActivityResultContracts.StartActivityForResult()) { result ->
            val teamModel = if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.TIRAMISU) {
                result.data?.getParcelableExtra(
                    TeamAddActivity.EXTRA_TEAM_MODEL,
                    TeamItem::class.java
                )
            } else {
                result.data?.getParcelableExtra(
                    TeamAddActivity.EXTRA_TEAM_MODEL,
                )
            }
            val teamType = result.data?.getStringExtra(TeamAddActivity.EXTRA_TEAM_ENTRY_TYPE)

            setAddContent(teamModel, teamType)
        }
...

fabAdd.setOnClickListener {
            val teamAddCategory = TeamAddCategory()
            teamAddCategory.show(childFragmentManager, teamAddCategory.tag)

            setFragmentResultListener(FRAGMENT_REQUEST_KEY) { _, bundle ->
                Log.d("teamFragment","startActivity")
                when (bundle.getString(FRAGMENT_RETURN_TYPE)) {
                    TeamAddCategory.RETURN_TYPE_RECRUITMENT -> {
                      //필요한 동작
                        val intent = TeamAddActivity.newIntentForAddRecruit(
                            requireContext(),
                            TeamAddType.RECRUIT.name
                        )
                        Log.d("teamFragment","result")
                        addContentLauncher.launch(intent)
                    }

                    TeamAddCategory.RETURN_TYPE_APPLICATION -> {
                      //필요한 동작
                        val intent = TeamAddActivity.newIntentForAddApplication(
                            requireContext(),
                            TeamAddType.APPLICATION.name
                        )
                        Log.d("teamFragment","result")
                        addContentLauncher.launch(intent)
                    }
                }

            }
           
        }
```

* 다시 **FragmentA**로 돌아와 `result= getstring` 으로 리턴값을 받은후 글을 추가해주는 액티비티 실행시켜주기(레지스터포리절트 사용)

본인은 FragmentB에서 바텀 시트가 닫힌 후 받은 **리턴 값**(Type) 으로 런쳐를 실행해 글을 추가하는 Activity가 열리도록 동작을 구현해 주었다.

하지만 액티비티가 열리지 않는 문제가 발생했다!



## 문제 해결 : 상위 및 하위 프래그먼트 간 결과 전달

```kotlin
fabAdd.setOnClickListener {
            val teamAddCategory = TeamAddCategory()
            teamAddCategory.show(childFragmentManager, teamAddCategory.tag)
            //같은 프래그먼트의 childFragmentManager를 쓰면 같은 라이프사이클을 사용 해야함
            childFragmentManager.setFragmentResultListener(FRAGMENT_REQUEST_KEY,viewLifecycleOwner) { key, bundle ->
                val result = bundle.getString(FRAGMENT_RETURN_TYPE)
```

* 문제는 childFragmentManager 이였다.
* 하위 프래그먼트의 결과를 상위 요소에 전달하려면 `setFragmentResultListener()`를 호출할 때 `getParentFragmentManager()` 대신 상위 프래그먼트의 `getChildFragmentManager()`를 사용해야한다.
* childFragmentManager를 사용하면 같은 라이프사이클을 사용해야 하기때문에 필요한 코드를 추가시켜주니 정상적으로 리턴값을 받아오는 모습이였다.