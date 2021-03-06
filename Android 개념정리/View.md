# View

-----

## ๐ setContentView

```kotlin
public class MainActivity extends Activity{
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
}
```

+ ํ๋ก์ ํธ๋ฅผ ์์ฑํ๋ฉด ์กํฐ๋นํฐ๋ฅผ ์์๋ฐ๋ ํด๋์ค๊ฐ default๋ก ์ ๊ณต๋ฉ๋๋ค. ๊ฐ๋ฐ์ ํธ์๋ฅผ ์ํด ์๋์ผ๋ก ์ง์๋๋ ๊ธฐ๋ฅ์ผ๋ก Activity ํด๋์ค๋ฅผ ์์๋ฐ์ผ๋ฉด **๋ฐ๋์ onCreate() ํจ์๋ฅผ ์ค๋ฒ ๋ผ์ด๋ฉ**ํฉ๋๋ค. ํด๋น ํจ์๋ **์กํฐ๋นํฐ(Activity)๊ฐ ์คํ๋  ๋ ๊ฐ์ฅ ๋จผ์  ์คํ**๋๋ ํจ์๋ก ๋ง์น ์๋ฐ์์ ํ๋ก๊ทธ๋จ ์ ๊ฐ์ฅ ๋จผ์  ์คํ๋๋ **main() ํจ์์ ๋น์ท**ํฉ๋๋ค. 

+ `setContentView()` => ์ฆ, View๋ค์ ํ๋ฉด์ ๋์ฐ๋ ๊ฒ
  setContentView() ํจ์๋ ์ฒซ ๋ฒ์งธ ์ธ์๋ก ๋๊ฒจ์ฃผ๋ **XML ๋ ์ด์์ ๋ฆฌ์์ค ID์ ํด๋นํ๋ ํ์ผ**์ **ํ์ฑ** ํ์ฌ **๋ทฐ(View)๋ฅผ ์์ฑํ๊ณ  ๋ทฐ(View)์ ์์ฑ(xmlํ์ผ์ ๊ฐ ๋ทฐ imageview, textView์ ์์ฑ) ์ ์ง์ ํ๊ณ  ๋ทฐ(View) ๊ฐ์ ์ํ๊ด๊ณ์ ๋ง์ถฐ ๋ฐฐ์น**๋ฅผ ํฉ๋๋ค. ์ด๋ฌํ ์ผ๋ จ์ ๊ณผ์ ์ **์ ๊ฐ(Inflate)**๋ผ ๋ถ๋ฆ๋๋ค. setContentView() ํจ์๋ xml ๋ฌธ์๋ฅผ ์ ๊ฐํ๊ธฐ ์ํด ๋ด๋ถ์ ์ผ๋ก LayoutInflater ํด๋์ค๋ฅผ ์ฐธ์กฐํฉ๋๋ค. 

  ์ฆ, xmlํ์ผ์ ๋ด์ฉ์ activity์ ๋์ฐ๋ ๊ฒ?
  
  ```kotlin
  setContentView(R.layout.activity_main);
  ```

  R์ res ํด๋๋ฅผ ์๋ฏธํ๊ณ , layout์ R์ ๋ด๋ถ ํด๋์ค๋ฅผ ์๋ฏธํ๋ค. ์ฆ, `R.layout.activity_main`์ activity_main.xml์ ๊ฐ๋ฆฌํค๋ ID๊ฐ ๋๋ค. 

  <br>
  
+ ์ ๊ฐ์(Inflater)

  XML๋ฌธ์๋ฅผ ์ ๊ฐ(inflate)ํ๊ธฐ ์ํด์ ์์คํ์์ผ๋ก ์ ๊ณตํ๋ ํด๋์ค๊ฐ ์์ต๋๋ค. ๋ฐ๋ก `LayoutInflater` ํด๋์ค๋ก ํด๋น ํด๋์ค์ ๊ฐ์ฒด๋ฅผ ๊ตฌํ๋ ๋ฐฉ๋ฒ์ ๋ ๊ฐ์ง๊ฐ ์์ต๋๋ค.

  1. `getSystemService()` ํจ์๋ฅผ ํตํด ๊ฐ์ ธ์ค๋ ๋ฐฉ๋ฒ

     ```kotlin
     LayoutInflater inflater1 = (LayoutInflater)getSystemService(Context.LAYOUT_INFLATER_SERVICE);
     ```

  2. ์กํฐ๋นํฐ ๋ด์์ ์ ๊ณตํ๋ `getLayoutInflater()` ํจ์๋ฅผ ํตํด ๋ฐ์์ค๋ ๋ฐฉ๋ฒ

     ```kotlin
     LayoutInflater inflater2 = getLayoutInflater();
     ```

  inflater๋ฅผ ์์ฑํ์๋ค๋ฉด `inflate()` ํจ์๋ฅผ ํตํด ์ ๊ฐ๋ ๋ทฐ ๊ฐ์ฒด๋ฅผ ๋ฐํ๋ฐ์ต๋๋ค. ์ฒซ ๋ฒ์งธ ์ธ์๋ก๋ XML ๋ ์ด์์ ๋ฆฌ์์ค ID๋ฅผ ๋๊ธฐ๊ณ  ๋ ๋ฒ์งธ๋ ๋ ์ด์์์ ์ต์์ Root ViewGruop์ผ๋ก ์ค์ ํ  ๊ฐ์ฒด๋ฅผ ๋๊น๋๋ค.

  ```kotlin
  View view  = getLayoutInflater().inflate(R.layout.activity_sub, null);
  ```

<br>

<br>


-----

## ๐ findViewById

+ activity_main.xml์์ ์ค์ ํ ๋ทฐ๋ค์ ์ด๊ธฐ ์ค์ ๋ง ํด๋์์ ์ด๋ฒคํธ๋ฅผ ๋ฐ๊ฑฐ๋ ํ  ์ ์์ต๋๋ค. ๊ทธ๋์, ์ด๋ฒคํธ๋ฅผ ๋ฐ๊ฑฐ๋ ๋ทฐ์ ์ํฅ์ ์ฃผ๋ ค๋ฉด MainActivity.kt์์ ์์ ์ ํด์ค์ผ ํ๋ค. ๊ทธ๋์ **activity_main.xml ๋ ์ด์์์ ์ค์ ๋ ๋ทฐ๋ค์ ๊ฐ์ ธ์ค๋** ๋ฉ์๋๊ฐ `findViewById`์ด๋ค.

  ```kotlin
  class MainActivity : AppConpatActivity() {
      override fun onCreate(savedInstanceState: Bundle?){
          super.onCreate(savedInstanceState);
          setContentView(R.layout.activity_main)
              
          val myText : TextView = findViewById(R.id.myTextView)
          myText.text = "Hi~"
      }
  }
  ```

  <br>

+ ์ด๋ ๊ฒ findViewById๋ฅผ ์ด์ฉํ๋ฉด, activity_main.xml ์์ ์ ์ฉ ์์ผฐ๋ ๊ธ์๋ฅผ ๋ฃ๊ฑฐ๋, ๊ธ์์์ ๋ณ๊ฒฝํ๊ฑฐ๋ ๋ฑ์ ์์์ ํ  ์ ์๋ ๋ฉ์๋๋ฅผ ์ง์ํ๊ฒ ๋๋ค. ํนํ, ๊ฐ์ฅ ์ค์ํ ์ด๋ฒคํธ ์ฒ๋ฆฌ๊ฐ ๊ฐ๋ฅํ ๋ฉ์๋๋ ์ง์์ ํ๊ฒ ๋๋ค. 

<br>

<br>

-----

## ๐ View Binding

+ ๋ชจ๋  UI ์์์ ์ก์ธ์คํ์ฌ ์ฌ์ฉ์์ ์๋ ฅ์ ์ฝ์ด์ผ ํ๋ค. ์ฝ๋๊ฐ `View`์์ ๋ฉ์๋๋ฅผ ํธ์ถํ๊ฑฐ๋ ์์ฑ(ex) myButton.text)์ ์ก์ธ์คํ๊ธฐ ์ ์ ๋จผ์  `Button` ๋๋ `TextView`์ ๊ฐ์ `View`์ ๋ํ ์ฐธ์กฐ๋ฅผ ์ฐพ์์ผ ํ๋ค. `findViewById()` ๋ฉ์๋๋ฅผ ํตํด **`View`์ ID๊ฐ ์ฃผ์ด์ง๋ฉด ์ด ๋ทฐ์ ๋ํ ์ฐธ์กฐ๋ฅผ ๋ฐํ**ํ๋ ์์์ ์คํํ์ง๋ง, ์ด๋ ์ฑ์ ๋ทฐ๊ฐ ๋ ๋ง์์ง๊ณ  UI๊ฐ ๋ณต์กํด์ง์ ๋ฐ๋ผ ๋ฒ๊ฑฐ๋ก์์ง ์ ์๋ค.

<br>

+ View Binding ์ฌ์ฉ

  1. ๋ทฐ ๊ฒฐํฉ ์ฌ์ฉ ์ค์ 

     + `build.gradle`์ ํ์ ์ฝ๋ ์ถ๊ฐ => Sync Now

     ```kotlin
     buildFeatures {
         viewBinding = true
     }  
     ```

     ๋ชจ๋ Gradle ํ์ผ์์ ๋ทฐ ๋ฐ์ธ๋ฉ์ ํ์ฑํํ๋ฉด, ๋ ์ด์์ ํ์ผ๋ง๋ค ๋ฐ์ธ๋ฉ ํด๋์ค๊ฐ ์์ฑ๋ฉ๋๋ค.

     <br>

  2. ๊ฒฐํฉ ๊ฐ์ฒด ์ด๊ธฐํ 

     +  โ	

       <img src = "https://user-images.githubusercontent.com/31370590/125413956-9674fa02-f7ac-4de5-a4f0-bdcd9435ece9.PNG " width = "560" height = "400">

       <br>

     + `MainActivity.kt`

       ```kotlin
       class MainActivity : AppCompatActivity() {
       
           lateinit var binding: ActivityMainBinding
       
           override fun onCreate(savedInstanceState: Bundle?) {
               super.onCreate(savedInstanceState)
               binding = ActivityMainBinding.inflate(layoutInflater)
               setContentView(binding.root)
           }
       }
       ```

       + `lateinit var binding: ActivityMainBinding`

         `lateinit` ํค์๋๋ ์๋ก์ด ํค์๋๋ก, **์ฝ๋๊ฐ ๋ณ์๋ฅผ ์ฌ์ฉํ๊ธฐ ์ ์ ๋จผ์  ์ด๊ธฐํํ  ๊ฒ์์ ํ์ธ**ํด ์ค๋๋ค. ํ๋กํผํฐ ์ด๊ธฐํ๋ฅผ ๋ฏธ๋ฃจ๋ ๊ฒ. ๋ณ์๋ฅผ ์ด๊ธฐํํ์ง ์์ผ๋ฉด ์ฑ์ด ๋น์ ์ ์ข๋ฃ๋ฉ๋๋ค.

       <br>

       + `binding = ActivityMainBinding.inflate(layoutInflater)`

         `activity_main.xml` ๋ ์ด์์์์ `Views`์ ์ก์ธ์คํ๋ ๋ฐ ์ฌ์ฉํ  `binding` ๊ฐ์ฒด๋ฅผ ์ด๊ธฐํํฉ๋๋ค.

       <br>

       + `setContentView(binding.root)`

         activity์ ์ฝํ์ธ  ๋ทฐ๋ฅผ ์ค์ ํฉ๋๋ค(๋ ์ด์์ ์ ๊ฐ?). ๋ ์ด์์์ ๋ฆฌ์์ค ID์ธ `R.layout.activity_main`์ ์ ๋ฌํ๋ ๋์ , ์ฑ์ ๋ทฐ ๊ณ์ธต ๊ตฌ์กฐ ๋ฃจํธ์ธ `binding.root`๋ฅผ ์ง์ ํฉ๋๋ค. 

         <span style="color:red">๊ทธ๋ฌ๋ฉด, `binding.root`๊ฐ `R.layout.activity_main`์ ๊ฐ๋ฆฌํค๋ ๊ฒ?</span>

     <br>

  3. binding ์ฌ์ฉ

     + `binding` ๊ฐ์ฒด๋ **ID๊ฐ ์๋ ์ฑ์ ๋ชจ๋  `View`๋ฅผ ์ํ ์ฐธ์กฐ๋ฅผ ์๋์ผ๋ก ์ ์**ํฉ๋๋ค. ๋ทฐ ๊ฒฐํฉ์ ์ฌ์ฉํ๋ ๊ฒ์ด ํจ์ฌ ๋ ๊ฐ๊ฒฐํด์ `View`๋ฅผ ์ํ ์ฐธ์กฐ๋ฅผ ์ ์งํ  ๋ณ์๋ฅผ ๋ง๋ค ํ์์กฐ์ฐจ ์์ผ๋ฉฐ ๊ฒฐํฉ ๊ฐ์ฒด์์ ์ง์  ๋ทฐ ์ฐธ์กฐ๋ฅผ ์ฌ์ฉํ๊ธฐ๋ง ํ๋ฉด ๋ฉ๋๋ค.

       ```kotlin
       // Old way with findViewById()
       val myButton: Button = findViewById(R.id.my_button)
       myButton.text = "A button"
       
       // Better way with view binding
       val myButton: Button = binding.myButton
       myButton.text = "A button"
       
       // Best way with view binding and no extra variable
       binding.myButton.text = "A button"
       ```

       > ๊ฒฐํฉ ํด๋์ค์ ์ด๋ฆ์ XML ํ์ผ์ ์ด๋ฆ์ ์นด๋ฉ ํ๊ธฐ๋ฒ์ผ๋ก ๋ณํํ๊ณ  ์ด๋ฆ ๋์ 'Binding'์ ์ถ๊ฐํ์ฌ ์์ฑ๋ฉ๋๋ค. ๋ง์ฐฌ๊ฐ์ง๋ก ๊ฐ ๋ทฐ๋ฅผ ์ํ ์ฐธ์กฐ๋ ๋ฐ์ค์ ์ญ์ ํ๊ณ  ๋ทฐ ์ด๋ฆ์ ์นด๋ฉ ํ๊ธฐ๋ฒ์ผ๋ก ๋ณํํ์ฌ ์์ฑ๋ฉ๋๋ค. ์๋ฅผ ๋ค์ด `activity_main.xml`์ `ActivityMainBinding`์ด ๋๊ณ  `binding.textView`๋ก `@id/text_view`์ ์ก์ธ์คํ  ์ ์์ต๋๋ค.
