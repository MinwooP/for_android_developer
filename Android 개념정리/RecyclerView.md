## ๐ฉ RecyclerView

### RecyclerView๋?

+ ์ฑ์์์ List๋ฅผ ํํํ  ๋ ์ฌ์ฉํ๋ ๋ทฐ
+ ๊ฐ๋ก/์ธ๋ก/๊ฒฉ์ ๋ฐฉํฅ์ ์ง์
+ ItemDecoration์ ์ด์ฉํด ์ ๋๋ฉ์ด์์ ๋ฃ์ ์ ์์
+ ์ด๋ฆ ๊ทธ๋๋ View๋ฅผ ์ฌ์ฌ์ฉํ๊ธฐ ๋๋ฌธ์ ํจ์จ์ ์
+ ListView๋ณด๋ค ์ ์ฐ -> ์ปค์คํ์ด ํธํจ
+ ViewHolder ํจํด์ ๊ฐ์  

<br>

#### RecyclerView VS ListView

<img src = "https://user-images.githubusercontent.com/31370590/138226738-a37effa7-08fd-451c-a7ce-bf73b9b8ff60.PNG">

<br>

### ๋๋ ๋น์ ๋ก RecyclerView ์ดํดํ๊ธฐ

+ ๋ง์ด ๋ค๋ฅธ **๋๋**์ ๋ฌถ์ด์ ํ๋งคํ๊ณ  ์ถ๋ค. **ํฌ์ฅ์ง**๋ฅผ ๋ง๋ค๊ณ  ์ด ํฌ์ฅ์ง๋ฅผ ๊ฐ์ง๊ณ  **์์ฒด**๊ฐ ๋๋์ ํฌ์ฅํด์ค. ๊ทธ๋ฌ๋ฉด **๋๋ ๋ฌถ์**์ด ์์ฑ๋๋ค. 

  <img src = "https://user-images.githubusercontent.com/31370590/138227600-3e1ad23c-3ef1-4046-abc1-5e3e7ac24848.PNG">

  + ๋๋ - data
  + ํฌ์ฅ์ง - Viewholder
  + ์์ฒด - Adapter
  + ๋๋ ๋ฌถ์ - RecyclerView

<br>

### RecyclerView ์์ ์์

+ ๋ฆฌ์คํธ์ ๋ฐ๋ณต์ ์ผ๋ก ๋ณด์ฌ์ง **์์ดํ์ Layout(xml) ๋ง๋ค๊ธฐ**
+ ์์ดํ์ **data class** ๋ง๋ค๊ธฐ
+ ์์ดํ ๋ทฐ์ UI์์๋ฅผ ๊ฐ์ง๊ณ  ์๋ **ViewHolder** ๋ง๋ค๊ธฐ
+ ViewHolder๋ฅผ ์์ฑํ๊ณ  ViewHolder์ ๋ฐ์ดํฐ๋ฅผ ์ ๋ฌํ๋ **Adapter**๋ง๋ค๊ธฐ
+ **RecyclerView** ๋ฐฐ์นํ๊ธฐ
+ RecyclerView ์์ดํ์ **๋ฐฐ์น๋ฐฉํฅ(๊ฐ๋ก/์ธ๋ก/๊ฒฉ์)** ํ์ธํ๊ธฐ(LayoutManager)
+ RecyclerView์ **Adapter** ์ฐ๊ฒฐํ๊ธฐ
+ Adapter์ **๋ฐ์ดํฐ ๊ฐฑ์ **ํ๊ธฐ



<br>

##### 1. ์์ดํ ๋ ์ด์์ ๋ง๋ค๊ธฐ

+ `layout > new > Layout Resource File`์ ํด๋ฆญ ํด `item_sample_list`๋ก ์ด๋ฆ์ ์ง์ด ์๋ก์ด item layout์ ๋ง๋ ๋ค.

+ ๊ทธ๋ฆฌ๊ณ  ๊ฑฐ๊ธฐ์ ์ํ๋ ๋ทฐ๋ฅผ ๋ฐฐ์นํ๋ค.

  ex) textView, textView, imageView

<br>

##### 2. ์์ดํ์ data class ๋ง๋ค๊ธฐ

+ ์ฐ๋ฆฌ๊ฐ ๋ง๋  item layout์ ๋ฃ์ด์ค data๋ฅผ ๋ด๋ ํด๋์ค

+ `java > com.example.~ > new > Kotlin Class/File `

```kotlin
data class UserData{
    val name : String, // ์ด๋ฆ
    val introduction : String // ์๊ฐ 
}
```

+ ์ด์  ์ด data๋ค์ **ViewHolder**๊ฐ ๊ฐ์ง๊ณ  ์๋ View(Item layout)์ ๋ฃ์ด์ฃผ๋ฉด ๋๊ฒ ๊ตฌ๋

<br>

##### 3, 4. ViewHolder, Adapter ๋ง๋ค๊ธฐ

##### ViewHolder๋?

+ RecyclerView์ ์ฌํ์ฉ ๋๋ Item Layout(View)๋ฅผ ๋ถ์ก๊ณ  ๊ด๋ฆฌํ๋ ์ญํ 
+ **Adapter์์ ์ ๋ฌ๋ฐ์ ๋ฐ์ดํฐ๋ฅผ Item Layout์ Bind** ์์ผ์ฃผ๋ ์ญํ 

+ VIewHolder๋ ๊ณ์ํด์ ์ฌํ์ฉ ๋จ

<br>

##### Adapter๋?

+ ํฌ์ฅ์ง(ViewHolder)๋ฅผ ๋ง๋ค๊ณ  ์ด ํฌ์ฅ์ง๋ฅผ ๊ฐ์ง๊ณ  ๋๋(data)์ ํฌ์ฅ(bind)ํด์ฃผ๋ ์์ฒด

+ ViewHolder๋ฅผ ์์ฑํ๊ณ  ItemLayout์ ViewHolder์ ๋๊ฒจ์ค๋ค.
+ ๋ฆฌ์คํธ๋ก ๋ณด์ฌ์ค Data๋ฅผ ๊ฐ ViewHolder์ ์ ๋ฌํด์ค๋ค. 

<br>

=> ViewHolder๋ Adapter๋ก๋ถํฐ Item Layout(view)๋ ๋ฐ๊ณ , ๊ทธ view์ ๋์ธ data๋ ๋ฐ๋๋ค. ๋ฐ์์ data๋ฅผ Item Layout์ Bind ์์ผ์ค๋ค. 

<br>

`Adapter class` code

<img src = "https://user-images.githubusercontent.com/31370590/138236424-349cd932-6df9-4135-afe5-0ed410422e43.PNG">

`ViewHolder` ์ฝ๋ ๋ถ์

+ Binding ๊ฐ์ฒด๋ฅผ ์์ฑ์๋ก ๊ฐ์ง๋ ViewHolder ํด๋์ค ์์ฑ

  `ItemSampleListBinding`

+ RecyclerView.ViewHolder ํด๋์ค ์์

  ์ด ๋, RecyclerView.ViewHolder ํด๋์ค๋ ์์ฑ์๋ก View๋ฅผ ์๊ตฌํ๋ฏ๋ก, **binding.root(root๋ทฐ)**๋ฅผ ๋๊ฒจ์ค๋ค. 

  (์ด๋ ๋๊ฒจ์ฃผ๋ View๋ ์ฌํ์ฉ๋๋ ItemLayout(`item_sample_list.xml`์ root ๋ทฐ์ด๋ค.)

+ `onBind()`ํจ์

  ViewHolder๊ฐ ๊ฐ์ง View์ Adapter๋ก๋ถํฐ ์ ๋ฌ๋ฐ์ data๋ฅผ ๋ถ์ฌ์ฃผ๋ ํจ์

  (Adapter์์ **onBindViewHolder()** ํธ์ถ ์ ์คํ๋๋ค.)

<br>

`Adapter` ์ฝ๋ ๋ถ์

+ RecyclerView.Adapter()๋ฅผ ์์ ๋ฐ๋๋ค.

  <>์์ ํด๋น Adapter๊ฐ ๋ฐ์ดํฐ๋ฅผ ์ ๋ฌํ  ViewHolder ํด๋์ค ์์ฑ

###### override ํด์ผํ๋ ํจ์ 3๊ฐ์ง

1. `getItemCount()`

   + RecyclerView๋ก ๋ณด์ฌ์ค ์ ์ฒด ๋ฐ์ดํฐ์ ๊ฐ์ ๋ฐํ

2. `onCreateViewHolder()`

   + ViewHolder๋ฅผ ์์ฑํ๊ณ  ItemLayout์ Binding ๊ฐ์ฒด๋ฅผ ๋ง๋ค์ด ViewHolder์ ์์ฑ์๋ก ๋๊ฒจ์ฃผ๋ ํจ์

     => ์ด ๋, View(Item Layout)์ ViewHolder์๊ฒ ๋๊ฒจ์ค๋ค !

   + Binding ๊ฐ์ฒด๋ฅผ ์์ฑํ  ๋, **LayoutInflater.from**์ ํตํด **LayoutInflater(๋ทฐ๋ฅผ ๋ง๋ค ๋ ์ฌ์ฉ)๋ฅผ ์์ฑ**ํ๋ค. ์ด๋, LayoutInflater.from์ context์ธ์๋ก๋ parent(ViewGroup)์ context๋ฅผ ๋๊ธด๋ค. 

3. `onBindViewHolder()`

   + ์ฌํ์ฉ ๋๋ ๋ทฐ(ViewHolder์ ๋ทฐ)๊ฐ ํธ์ถํ์ฌ ์คํ๋๋ ํจ์
   + **ViewHolder์ position์ ๋ฐ์ดํฐ๋ฅผ ๊ฒฐํฉ**์ํค๋ ์ญํ ์ ํ๋ค.

<br>

##### 5. RecyclerView ๋ฐฐ์นํ๊ธฐ

<img src = "https://user-images.githubusercontent.com/31370590/138240550-29060a20-86cd-46ad-a975-a649d1f46ab5.PNG" width = "900" height = "350">

+ itemCount
+ listitem 

<br>

##### 6. RecyclerView ์์ดํ์ **๋ฐฐ์น๋ฐฉํฅ(๊ฐ๋ก/์ธ๋ก/๊ฒฉ์)** ํ์ธํ๊ธฐ(LayoutManager)

`app:layoutManager = "andriodx.recyclerview.widget.LinearManager"`

<br>

##### 7, 8. RecyclerView์ **Adapter** ์ฐ๊ฒฐํ๊ธฐ, Adapter์ data ๊ฐฑ์ ํ๊ธฐ

`MainActivity` code

<img src = "https://user-images.githubusercontent.com/31370590/138242205-82aef629-3662-44b5-b639-848842cc126a.PNG">







๋งค๋ฒ ์ฌ์ฉ์๊ฐ ์๋๋ก ์คํฌ๋กค ํ  ๋ ๋ง๋ค ๋งจ ์์ ์์นํ ๋ทฐ ๊ฐ์ฒด๊ฐ ์๋ก ์ญ์ ๋๊ณ , ์๋ซ ๋ถ๋ถ์์ ์๋ก ๋ํ๋  ์ฑํ๋ฐฉ ๋ทฐ ๊ฐ์ฒด๋ฅผ ์๋ก ์์ฑํ๋ฉด ๊ฒฐ๊ตญ 100๊ฐ์ ๋ทฐ ๊ฐ์ฒด๊ฐ ์ญ์ ๋๊ณ  ์์ฑ๋๋ ๊ฒ์ผ ๋ฟ๋ง ์๋๋ผ, ์คํฌ๋กค์ ์์๋๋ก ์๋ค ๊ฐ๋ค ํ๋ฉด ์ ๋ฐฑ๊ฐ์ ๋ทฐ ๊ฐ์ฒด๊ฐ ์๋ก ์์ฑ๋๊ณ  ์ญ์ ๋จ์ ๋ฐ๋ณตํ๋ค.

๋ฆฌ์ฌ์ดํด๋ฌ ๋ทฐ๋ ์ฌ์ฉ์๊ฐ ์๋๋ก ์คํฌ๋กค ํ๋ค๊ณ  ๊ฐ์ ํ์ ๋, **๋งจ ์์ ์กด์ฌํด์ ์ด์  ๊ณง ์ฌ๋ผ์ง ๋ทฐ ๊ฐ์ฒด๋ฅผ ์ญ์  ํ์ง์๊ณ  ์๋ซ์ชฝ์์ ์๋ก ๋ํ๋๋  ํ๋์ ๋ทฐ ์์น๋ก ๊ฐ์ฒด๋ฅผ ์ด๋์ํจ๋ค.** ์ฆ ๋ทฐ ๊ฐ์ฒด ์์ฒด๋ฅผ ์ฌ์ฌ์ฉ ํ๋ ๊ฒ์ธ๋ฐ, **์ค์ํ ์ ์ ๋ทฐ ๊ฐ์ฒด๋ฅผ ์ฌ์ฌ์ฉ ํ  ๋ฟ์ด์ง ๋ทฐ ๊ฐ์ฒด๊ฐ ๋ด๊ณ  ์๋ ๋ฐ์ดํฐ(์ฑํ๋ฐฉ ์ด๋ฆ)๋ ์๋ก ๊ฐฑ์ ๋๋ค๋ ๊ฒ**์ด๋ค. ์ด์จ๊ฑฐ๋ ๋ทฐ ๊ฐ์ฒด๋ฅผ ์๋ก ์์ฑํ์ง๋ ์์ผ๋ฏ๋ก ํจ์จ์ ์ธ ๊ฒ์ด๋ค.

***๊ฒฐ๊ณผ์ ์ผ๋ก ๋ณด์๋ฉด, ๋งจ ์ฒ์ ํ๋ฉด์ ๋ณด์ฌ์ง 10๊ฐ ์ ๋์ ๋ทฐ ๊ฐ์ฒด๋ง์ ๋ง๋ค๊ณ , ์ค์  ๋ฐ์ดํฐ๊ฐ 100๊ฐ๋  1000๊ฐ๋  ์๋ ๋ง๋ค์ด ๋์ 10๊ฐ์ ๊ฐ์ฒด๋ง ๊ณ์ ํด์ ์ฌ์ฌ์ฉ ํ๋ ๊ฒ์ด๋ค.***

๋ฐ๋ผ์ ๋งจ ์ฒ์ 10๊ฐ์ ๋ทฐ๊ฐ์ฒด๋ฅผ ๊ธฐ์ตํ๊ณ  ์์(ํ๋ฉ) ๊ฐ์ฒด๊ฐ ํ์ํ๋ฐ ์ด ๊ฒ์ด ViewHolder์ด๋ค. ๋์ค์ ์ ์ฒด ์ฝ๋๋ฅผ ๋ณด๊ฒ ์ง๋ง, ViewHolder ์ฝ๋ ๋ถ๋ถ๋ง ๋ณด์๋ฉด ์๋์ ๊ฐ๋ค.

```kotlin
class MyViewHolder(view: View): RecyclerView.ViewHolder(view) {
    var textField = view.chat_title
}
```

```kotlin
// MainActivity
override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    setContentView(R.layout.activity_recycler_view)

    val datas = Array(100) {
        "chat $it"
    }

    recycler_view.adapter = MyApdater(datas)
    recycler_view.layoutManager = LinearLayoutManager(this)
    // ์ฝ๋๋จ์์ layoutmanager ์ค์ ํ๊ธฐ
}
```



์ฐธ๊ณ 

+ [๋ฆฌ์ฌ์ดํด๋ฌ๋ทฐ์ ์๋ฆฌ์ ์ฌ์ฉ๋ฒ](https://wooooooak.github.io/android/2019/03/28/recycler_view/)
+ [๋ฉํฐ๋ทฐ ํ์ ๋ฆฌ์ฌ์ดํด๋ฌ๋ทฐ ๋ง๋ค๊ธฐ](https://wooooooak.github.io/android/2019/04/13/RecyclerView_mutiType/)





### ๐ฉ DiffUtil๊ณผ ListAdapter ์ดํดํ๊ณ  RecyclerView์ ์ ์ฉํ๊ธฐ

+ Recyclerview์ ๋ฐ์ดํฐ๊ฐ ๋ณํ๋ฉด Recyclerview Adapter๊ฐ ์ ๊ณตํ๋ `notifyItem`๋ฉ์๋๋ฅผ ์ฌ์ฉํด์ ViewHolder ๋ด์ฉ์ ๊ฐฑ์ ํ  ์ ์์ต๋๋ค.
+ ๊ทธ๋ฐ๋ฐ ๋ฐ์ดํฐ๊ฐ ๋ณ๊ฒฝ๋๋ ๋ฐฉ์์ ํ์ธํ๊ณ  ๊ทธ๋๋ง๋ค ์ด๋ ๊ฒ notify๋ฅผ ์ผ์ผ์ด ํด ์ฃผ๋๊ฒ์ ๋ฒ๊ฑฐ๋กญ๊ธฐ๋ ํ๊ณ , ๋ ์ฌ์ฉํ๊ธฐ์ ๋ฐ๋ผ์๋ ๊ฐฑ์ ์ด ํ์์๋ ViewHolder๋ฅผ ๊ฐ์ด ๊ฐฑ์ ํ๋ ๋ถํ์ํ ์์์ด ์๊ธธ์๋ ์์ต๋๋ค.

#### DiffUtil

+ DiffUtil์ **๋ ๋ฐ์ดํฐ์์ ๋ฐ์์ ๊ทธ ์ฐจ์ด๋ฅผ ๊ณ์ฐํด์ฃผ๋ ํด๋์ค**์๋๋ค. DiffUtil์ ์ฌ์ฉํ๋ฉด ๋ ๋ฐ์ดํฐ ์์ ๋น๊ตํ ๋ค ๊ทธ์ค ๋ณํ๋ถ๋ถ๋ง์ ํ์ํ์ฌ Recyclerview์ ๋ฐ์ํ  ์ ์์ต๋๋ค.

+ DiffUtil์ ์ฌ์ฉํ๊ธฐ ์ํด์๋ `DiffUtil.Callback()`์ ์์๋ฐ์ `areItemsTheSame`์ผ๋ก ๋น๊ต๋์์ธ ๋ ๊ฐ์ฒด๊ฐ ๋์ผํ์ง ํ์ธํ๊ณ , `areContentsTheSame`์ผ๋ก ๋ ์์ดํ์ด ๋์ผํ ๋ฐ์ดํฐ๋ฅผ ๊ฐ์ง๋์ง ํ์ธํ๋ฉด ๋ฉ๋๋ค.



### ์ฐธ๊ณ 

+ [RecyclerView ์ด๋ํฐ์ ๋ฐ์ดํฐ ๋น ๋ฅด๊ฒ ๋ฐ๊พธ๊ธฐ - ListAdapter์ DiffUtil ์ฌ์ฉํ๊ธฐ](https://velog.io/@l2hyunwoo/Android-RecyclerView-DiffUtil-ListAdapter)
