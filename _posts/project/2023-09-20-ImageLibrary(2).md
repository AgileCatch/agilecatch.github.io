---

layout: post
title: 전화번호부
image: /assets/img/blog/kakaobank.png
accent_image: 
  background: url('/assets/img/me/wave3.jpg') center/cover
  overlay: false
accent_color: '#fff'
theme_color: '#fff'
description: >
    coding test
invert_sidebar: true
categories :
 - project

---

# [Kotlin/개인]  Kakaobank 2023 앱 개발자 채용 기출 문제 (2)

* toc
{:toc}
---

`프로젝트 소개` :  Kakaobank 2023 상반기 안드로이드 앱 개발자 채용 기출 문제

 

## **1) Search-ViewModel**

* viewmodel을 사용하기위해 **gradle**에 **의존성** 추가

  * **Plugins**

  ```
  id ("kotlin-parcelize")
  id ("kotlin-android")
  ```

  * **dependencies**

	```
  //by viewModels를 사용하기 위한 의존성
    implementation ("androidx.activity:activity-ktx:1.7.2")
    implementation ("androidx.fragment:fragment-ktx:1.6.1")
	```



* **ViewModelFactory** 생성
  *  프래그먼트에서 뷰모델에 전달하고싶은 데이터를 직접 넣어주기 위해서 **provider**로 뷰모델을 생성하는 과정에서 **Factory** 필요함

```kotlin
class SearchViewModelFactory (private val idGenerate: AtomicLong) : ViewModelProvider.Factory{
    // ViewModelProvider.Factory 인터페이스를 구현하기 위해 create 메서드를 오버라이드
    // 이 메서드는 ViewModel 인스턴스를 생성하는 역할을 함
    override fun <T: ViewModel> create(modelClass: Class<T>): T {
        // create 메서드는 요청된 ViewModel 클래스 (modelClass)를 기반으로 ViewModel을 생성한다.

        if(modelClass.isAssignableFrom(SearchViewModel::class.java)){ // 요청된 modelClass가 SearchViewModel Class와 호환 가능한지 확인
            return SearchViewModel(idGenerate) as T //호환되는 경우 생성된 ViewModel을 T타입으로 형변환 하여 반환
        }
        throw IllegalArgumentException("Not Found ViewModel class.") // 호환되지 않는 경우 알림
    }
}
```



* **ViewModel** 생성
  * `AtomicLong`은 Long 자료형을 갖고 있는 **Wrapping** 클래스이다.
    * `Thread-safe`로 구현되어 멀티쓰레드에서 **synchronized** 없이 사용할 수 있다.
    * 또한 synchronized 보다 적은 비용으로 동시성을 보장할 수 있다.

```kotlin
class SearchViewModel (private val idGenerate: AtomicLong) : ViewModel() { //비즈니스 로직을 전부 viewModel에서 처리 -> 이후 처리한 데이터를 뷰에다 알려줌 {
    // _list : viewModel 내부적으로 control 하는 데이터
    private val _list :MutableLiveData<List<SearchModel>> = MutableLiveData()

    // viewmodel 내부에서 사용하는 읽기만 가능한 상태
    val list : LiveData<List<SearchModel>> get() = _list

    //AtomicLong을 통해 id값 부
    init {
        _list.value= arrayListOf<SearchModel>().apply {
            for (i in 0 until 3){
                add(
                    SearchModel(
                        this@SearchViewModel.idGenerate.getAndIncrement(),
                        0,
                        "Name ${i}",
                        "Date ${i}",
                    )
                )
            }
        }
    }
}
```



* **DataModel**에 id  값을 Long으로 변경 후 **@Parcelize** 선언
  * 데이터 클래스를 **인텐트 객체**로 넘기기위해서 @Parcelize를 상속해야한다.

```kotlin
@Parcelize
data class SearchModel (
    val id: Long? = null,
    val image : Int,
    val name :String,
    val date :String,
    var isBookMark : Boolean =false
) : Parcelable
```



* **SearchFragment**
  *  뷰모델 **프로바이더** 생성


```kotlin
//현업코드 by viewModels -> 의존성 추가해주어야함.'
private val viewModel: SearchViewModel by viewModels { SearchViewModelFactory(AtomicLong(1L)) }
```

* **Viewmodel**을 위한 **init Class** 생성
  * 데이터를 뿌려주기위함.
  * `viewLifecycleOwner` : 화면이 있을때만 보여질 수 있도록 해줌.

```kotlin
private fun initViewModel()= with(viewModel) {
    // viewModel 상 읽기용 list
    list.observe(viewLifecycleOwner) { // Fragment LV : observe(viewLifecycleOwner)
        listAdapter.submitList(it)
    }
}
```



* **SearchListAdapter**

  * viewmodel 추가로 사용하지 않는 함수 제거(getItem,,list 등등)
  * **onBindViewHolder** `getItem` 으로 변경해주기

  ```kotlin
  override fun onBindViewHolder(holder: ViewHolder, position: Int) {
      val item = getItem(position)
      holder.bind(item)
  }
  ```

---

## **2) Locker - ViewModel**

* ViewModel 생성

```kotlin
class LockerViewModel () : ViewModel() {

    //비즈니스 로직을 전부 viewModel에서 처리 -> 이후 처리한 데이터를 뷰에다 알려줌 {
    // _list : viewModel 내부적으로 control 하는 데이터
    private val _list :MutableLiveData<List<LockerModel>> = MutableLiveData()
    val list : LiveData<List<LockerModel>> get() = _list

    fun findIndex(lockerModel: LockerModel): Int? {
        val currentList = list.value?.toMutableList()
        val findTodoById = currentList?.find { // 수정하고자 하는 Model의 id와 currentList의 id를 비교해 같은 id 를 찾음
            it.id == lockerModel.id
        }
        return currentList?.indexOf(findTodoById)//indexOf : 찾고자 하는 Array의 index를 반환
    }

}
```

* **BookmarkViewModelFactory** 생성

  ```kotlin
  class LockerViewModelFactory : ViewModelProvider.Factory {
  
      override fun <T: ViewModel> create(modelClass: Class<T>): T {
          if(modelClass.isAssignableFrom(LockerViewModel::class.java)){
              return LockerViewModel() as T
          }
          throw IllegalArgumentException("Not Found ViewModel class.")
      }
  }
  ```

  

* 프래그먼트에 뷰모델 **프로바이더** 생성

```kotlin
private val viewModel : LockerViewModel by viewModels{LockerViewModelFactory()}
```

* Viewmodel을 위한 init class 생성
  * 데이터를 뿌려주기위함.
  * `viewLifecycleOwner` : 화면이 있을때만 보여질 수 있도록 해줌.

```kotlin
private fun initViewModel()= with(viewModel) {
    // viewModel 상 읽기용 list
    list.observe(viewLifecycleOwner) { // Fragment LV : observe(viewLifecycleOwner)
        listAdapter.submitList(it)
    }
}
```



* **LockerListAdapter**

  * viewmodel 추가로 사용하지 않는 함수 제거(getItem,,list 등등)
  * **onBindViewHolder** `getItem` 으로 변경해주기

  ```kotlin
  override fun onBindViewHolder(holder: ViewHolder, position: Int) {
          val item = getItem(position) // ListAdapter의 메소드 getItem
          holder.bind(item)
      }
  ```



* **Viewmodel**에 **test** 값 넣어 확인하기

```kotlin
init {
    _list.value= arrayListOf<LockerModel>().apply {
        for (i in 0 until 3){
            val iString = "${i}"
            val iLong = iString.toLong()
            add(
                LockerModel(
                    iLong,
                    0,
                    "Name ${i}",
                    "Date ${i}",
                )
            )
        }
    }
}
```



## **3) Main - ViewModel 만들기**

다른 프래그먼트에서 북마크를 하고 프래그먼트 연결을 하기위해 Viewmodel을 미리 생성

```kotlin
class MainViewModel : ViewModel() {
    val searchState : MutableLiveData<SearchState> = MutableLiveData()
    val lockerState : MutableLiveData<LockerState> = MutableLiveData()
}

sealed interface SearchState{
    data class AddBookmark(val bookmarkModel: LockerModel) : SearchState
    data class RemoveBookmark(val bookmarkModel: LockerModel) : SearchState
    data class ModifyBookmark(val bookmarkModel: LockerModel) : SearchState
}

sealed interface LockerState{
    data class ModifyTodo(val lockerModel: LockerModel) : LockerState
}
```

