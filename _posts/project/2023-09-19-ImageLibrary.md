---
layout: post
title: 전화번호부
image: /assets/img/blog/contact17.png
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

# [Kotlin/개인]  Kakaobank 2023 앱 개발자 채용 기출 문제 (1)

* toc
{:toc}
---

`프로젝트 소개` :  Kakaobank 2023 상반기 안드로이드 앱 개발자 채용 기출 문제



## **1) UI 만들기**

* **main_activity.xml**
  * 프레그먼트 사용을 위해 **TabLayout** ,**ViewPager2** 을 넣어줌

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".main.MainActivity">


    <com.google.android.material.tabs.TabLayout
        android:id="@+id/tab_layout"
        android:layout_width="0dp"
        android:layout_height="60dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent" />

    <androidx.viewpager2.widget.ViewPager2
        android:id="@+id/view_pager"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        app:layout_constraintBottom_toTopOf="@+id/tab_layout"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />


</androidx.constraintlayout.widget.ConstraintLayout>
```

---

* **Mainactivity**

  * **viewbinding** 사용하기 위해 **gradle** 추가하기

    ```
    buildFeatures{
    
      viewBinding=true
    
    }
    ```

  * **initView()** 로 초기화 블록 만들어주기

  * `= with(binding)`  선언해 바인딩해주기

  * **view pager adapter** 연결

  * **TabLayoutMediator** 사용해 `attach()` 해주기

  ```kotlin
  class MainActivity : AppCompatActivity() {
      private lateinit var binding: MainActivityBinding
  		
  		//이 단계에서는 아직 안만듬
      private val viewPagerAdapter by lazy {
          MainViewPagerAdapter(this@MainActivity)
      }
  
      override fun onCreate(savedInstanceState: Bundle?) {
          super.onCreate(savedInstanceState)
          binding = MainActivityBinding.inflate(layoutInflater)
          setContentView(binding.root)
  
          initView()
      }
  
      private fun initView() = with(binding) {
          //view pager adapter
          viewPager.adapter = viewPagerAdapter
  
          // TabLayout x ViewPager2
          TabLayoutMediator(tabLayout,viewPager) { tab, position ->
              tab.setText(viewPagerAdapter.getTitle(position))
          }.attach()
      }
  
  }
  ```

  

## **2) 프래그먼트 만들기**

```kotlin
class SearchFragment : Fragment() {
    companion object {
        //static 함수로 검색결과 fragment를 가져올 수 있는 instance 생성
        //이걸통해서 프래그먼트를 만듬
        fun newInstance() = SearchFragment()
    }

    private var _binding: SearchFragmentBinding? = null
    private val binding get() = _binding!!
    

    override fun onCreateView(
        inflater: LayoutInflater, container: ViewGroup?,
        savedInstanceState: Bundle?,
    ): View? {
        // Inflate the layout for this fragment
        _binding = SearchFragmentBinding.inflate(layoutInflater)
        return binding.root
    }

    //프래그먼트 뷰 생성후 해야할일 설정하는곳
    override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        super.onViewCreated(view, savedInstanceState)
        //recycler View에 대한 초기화를 해줘야함
    }

    //프래그먼트의 메모리 누수를 방지하기 위해 넣어줌 (구글 권장)
    override fun onDestroyView() {
        _binding = null
        super.onDestroyView() 
    }
}
```

* `Fragment()` 상속 받기

* **static** 함수로 검색결과 **fragment**를 가져올 수 있는 **instance** 생성

  ```kotlin
  companion object {
          //static 함수로 검색결과 fragment를 가져올 수 있는 instance 생성
          //이걸통해서 프래그먼트를 만듬
          fun newInstance() = SearchFragment()
      }
  ```

* **ViewBinding** 선언하기

  ```kotlin
  private var _binding: SearchFragmentBinding? = null
      private val binding get() = _binding!!
  ```

* **onCreateView**

  * **binding** 을  **inflate** 해주고 리턴값 선언하기

  ```kotlin
  override fun onCreateView(
          inflater: LayoutInflater, container: ViewGroup?,
          savedInstanceState: Bundle?,
      ): View? {
          // Inflate the layout for this fragment
          _binding = SearchFragmentBinding.inflate(layoutInflater)
          return binding.root
      }
  ```

* **onDestroyView**

  * 프래그먼트의 누수 방지를 위해 강제적으로 **_binding = null** 를 선언해 주도록 구글에서 권장하고 있음

    ```kotlin
    override fun onDestroyView() {
            _binding = null
            super.onDestroyView()
        }
    ```

    

## **3) 프래그먼트 레이아웃 만들기, item 만들기**

**Serch_item.xml**

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:padding="10dp">

    <ImageView
        android:id="@+id/imageView"
        android:layout_width="170dp"
        android:layout_height="170dp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        android:src="@drawable/cat6" />

    <TextView
        android:id="@+id/tv_name"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_marginTop="10dp"
        android:text="name"
        app:layout_constraintEnd_toEndOf="@+id/imageView"
        app:layout_constraintStart_toStartOf="@+id/imageView"
        app:layout_constraintTop_toBottomOf="@+id/imageView" />

    <TextView
        android:id="@+id/tv_date"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_marginTop="10dp"
        android:text="date"
        app:layout_constraintEnd_toEndOf="@+id/tv_name"
        app:layout_constraintStart_toStartOf="@+id/tv_name"
        app:layout_constraintTop_toBottomOf="@+id/tv_name" />

    <ImageView
        android:id="@+id/btn_bookmark"
        android:layout_width="40dp"
        android:layout_height="40dp"
        android:src="@drawable/heart"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.68" />
</androidx.constraintlayout.widget.ConstraintLayout>
```

* 리사이클러뷰를 사용하기위해 **item**을 만들어줌
  * **imageView**
  * **tv_name**
  * **tv_date**
  * **btn_bookmark**

---

**Search_fragment.xml**

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    xmlns:app="http://schemas.android.com/apk/res-auto">

    <androidx.recyclerview.widget.RecyclerView
        android:id="@+id/search_list"
        android:layout_width="0dp"
        android:layout_height="0dp"
        app:layoutManager="androidx.recyclerview.widget.GridLayoutManager"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintBottom_toBottomOf="parent"
        app:spanCount="2"
        />

</androidx.constraintlayout.widget.ConstraintLayout>
```

* **RecyclerView** id 값 넣어주기

* **GridLayoutManager** 를 사용해 그리드뷰로 만들어 줄 것임

  * `spanCount` 를 2로 설정하면 **GridView 2줄**로 만들 수 있음

  

## **4) 데이터모델 만들기**

```kotlin
data class SearchModel (
 		val id: Int,
    val image : Int,
    val name :String,
    val date :String,
    var isBookMark : Boolean =false
)
```

* item의 내용대로 Data Class 생성해주기



## **5) 메인 어댑터 만들기**

* 프래그먼트를 관리하기위한 **DataClass** 생성하기

```kotlin
data class MainTabs(
    val fragment: Fragment,
    val titleRes: Int
)
```

```kotlin
class MainViewPagerAdapter(
    fragmentActivity: FragmentActivity
) : FragmentStateAdapter(fragmentActivity) {

    private val fragments = ArrayList<MainTabs>()

    //페이지 생성 관리
    init {
        fragments.add(
            MainTabs(SearchFragment.newInstance(), R.string.main_tab_search_title)
        )
        fragments.add(
            MainTabs(LockerFragment.newInstance(), R.string.main_tab_locker_title),
        )
    }

    fun getTitle(position: Int): Int {
        return fragments[position].titleRes
    }

    //화면의 갯수
    override fun getItemCount(): Int {
        return fragments.size
    }
    
    override fun createFragment(position: Int): Fragment {
        return fragments[position].fragment
    }
}
```

* **FragmentStateAdapter** 를 사용하여 액티비티를 넘겨줄 수 있도록함
* **init**으로 페이지 생성 관리하기

---

* **Mainactivity**  어댑터를 **지연초기화 함수로 선언**하기
  * 함수를 사용할때만 초기화가 될수 있도록 설정할 수 있다.


```kotlin
private val viewPagerAdapter by lazy {
    MainViewPagerAdapter(this@MainActivity)
}
```

* **initView()** 에 어댑터 연결

```kotlin
private fun initView() = with(binding) {
    //view pager adapter
    viewPager.adapter = viewPagerAdapter

    // TabLayout x ViewPager2
    TabLayoutMediator(tabLayout,viewPager) { tab, position ->
        tab.setText(viewPagerAdapter.getTitle(position))
    }.attach()
}
```



## **6) 리스트뷰 어댑터 만들기**

```kotlin
class SearchListAdapter : ListAdapter<SearchModel, SearchListAdapter.ViewHolder>(
    object : DiffUtil.ItemCallback<SearchModel>() {
        override fun areItemsTheSame(
            oldItem: SearchModel, newItem: SearchModel
        ): Boolean {
            return oldItem.id == newItem.id
        }

        override fun areContentsTheSame(
            oldItem: SearchModel,
            newItem: SearchModel
        ): Boolean {
            return oldItem == newItem
        }
    }
) {
    class ViewHolder(
        private val binding: LockerItemBinding
    ) : RecyclerView.ViewHolder(binding.root) {

    }

    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): ViewHolder {
        TODO("Not yet implemented")
    }

    override fun onBindViewHolder(holder: ViewHolder, position: Int) {
        TODO("Not yet implemented")
    }

}
```

- **ViewHolder** 먼저 작성해주기

  ```kotlin
      class ViewHolder(
          private val binding: LockerItemBinding
      ) : RecyclerView.ViewHolder(binding.root) {
          fun bind(item: SearchModel)= with(binding){
  //이미지, 추가해야함
              binding.tvDate.text=item.date
              binding.tvName.text=item.name
          }
  
      }
  ```

* **DataModel** 선언하기

  ```kotlin
  private val list = ArrayList<SearchModel>()
  ```

* **onCreateViewHolder**

  * retrun값 넣어주기

  ```kotlin
  override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): ViewHolder {
          return SearchListAdapter.ViewHolder(
              LockerItemBinding.inflate(
                  LayoutInflater.from(parent.context)
              )
          )
      }
  ```

* **onBindViewHolder**

  * list로 넘길 수 있도록 bind 해주기

  ```kotlin
  override fun onBindViewHolder(holder: ViewHolder, position: Int) {
          val item = list[position] 
          holder.bind(item)
      }
  ```

* **addItems** 을 위한 함수 추가

```kotlin
fun addItems(items: List<SearchModel>) {
        list.addAll(items)
        notifyDataSetChanged()
    }

    override fun getItemCount(): Int {
        return list.size
    }
```



## **7) 프래그먼트에 어댑터 연결해주기**

* **지연초기화 함수로** 어댑터 선언하기

```
private val listAdapter by lazy {
    SearchListAdapter()
}
```

* 함수 초기화를 위해 **initView()** 생성
  * 함수 **binding**해주기
  * 어댑터 연결 하기

```
override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
    super.onViewCreated(view, savedInstanceState)
    //recycler View에 대한 초기화를 해줘야함
    initView()
}

private fun initView() =with(binding) {
    //어댑터 연결
        searchList.adapter=listAdapter
}
```

* **onCreatedView()** test data 추가하기

```
// for test
val testList = arrayListOf<SearchModel>()
for (i in 0 until 100) {
    testList.add(
        SearchModel(
            id = i,
            0,
            "Locker Name $i",
            "Locker Date $i"
        )
    )
}
listAdapter.addItems(testList)
```

