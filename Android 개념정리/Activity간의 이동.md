# ๐ฉActivity ๊ฐ ์ด๋

####  ๐ startActivityForResult, onActivityResult => Deprecated

##### startActivityForResult

```kotlin
Intent intent = new Intent(getApplicationContext(),SubActivity.class);
startActivityForResult(intent,REQUEST_CODE);
```

+ **startActivity** : ์ ์กํฐ๋นํฐ๋ฅผ ์ด์ด์ค (**๋จ๋ฐฉํฅ**)

+ **startActivityForResult** : ์ ์กํฐ๋นํฐ๋ฅผ ์ด์ด์ค + ๊ฒฐ๊ณผ๊ฐ ์ ๋ฌ (**์๋ฐฉํฅ**)

  => **์ฆ,** **๊ฒฐ๊ณผ๊ฐ์ ์ ๋ฌํด์ฃผ๋๋ ์๋๋์ ์ฐจ์ด**๋ค. Activity์์ resultCode๋ฅผ ๋ณด๋ด์ ์ํ๋ ๊ธฐ๋ฅ์ ์ํํ  ์ ์๋ค.

<br>

##### onActivityResult

+ startActivityForResult๋ก ์๋ก์ด ์กํฐ๋นํฐ๋ก ๊ฒฐ๊ณผ๊ฐ์ ๊ฐ์ง๊ณ  ์ด๋ํ ํ์, ๋ค์ ์ด์  ์กํฐ๋นํฐ๋ก ๋์์ฌ ๋, ์๋ก์ด ์กํฐ๋นํฐ์์ ๊ฒฐ๊ณผ๊ฐ์ ๊ฐ์ง๊ณ  ๋์์ฌ ์ ์๋๋ก ํ๋ ๋ฉ์๋์ด๋ค.
+ startActivityForResult๋ก `MainActivity`์์ ์๋ก์ด ์กํฐ๋นํฐ `SubActivity`๋ฅผ ๋์ ๋ค๋ฉด, SubActivity ์ข๋ฃ ์์ ์ `setResult()` ๋ฉ์๋๋ฅผ ํตํด ๊ฒฐ๊ณผ๊ฐ์ ์ค์ ํ๋ค.
+ ๊ทธ๋ฆฌ๊ณ  `MainActivity`์์ **onActivityResult**๋ก ์ ๋ฌ๋ ๊ฒฐ๊ณผ์ ๋ฐ๋ผ ์ด์ ๋ํ ๋ฐ์์ ์์ฑํ  ์ ์๋ค. 

+ `startActivityForResult`, `onActivityResult`

```kotlin
class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        btnWrite.setOnClickListener { // ์์ฑํ๊ธฐ๋ฅผ ํด๋ฆญํ๋ฉด
            val writeIntent = Intent(this, WriteActivity::class.java) // ์ด๋ํ  ์กํฐ๋นํฐ๋ฅผ Intent์ ๋ด์
            startActivityForResult(writeIntent, 0) // ๋ค์ ์ซ์๋ requestCode (์ด ์ซ์๋ ๋ค์ ํฌ์คํ์์ ๋ฐฐ์ธ ์์ , ์ง๊ธ์ ์๋ฌด ์ซ์๋ ๋ฃ์ผ๋ฉด ๋จ)
        }
    }

    // ๋ค์ ํ์ฌ ์กํฐ๋นํฐ๋ก ๋์์์ ๋ ํ  ์์
    override fun onActivityResult(requestCode: Int, resultCode: Int, data: Intent?) {
        super.onActivityResult(requestCode, resultCode, data)

        when (resultCode) {
            Activity.RESULT_OK -> {
                Toast.makeText(this, "๋ฌธ์๋ฅผ ๋ณด๋ด๊ณ ์ผ ๋ง์์ด..!", Toast.LENGTH_SHORT).show()
            }

            Activity.RESULT_CANCELED -> {
                Toast.makeText(this, "ํ์.. ์  ๊นจ๊ณ  ๋ค์ ์ฐ๋ฝํด๋ณด์", Toast.LENGTH_SHORT).show()
            }
        }
    }
}
```

<br>

+ ํธ์ถ๋ ์กํฐ๋นํฐ์์ `setResult`

```kotlin
class WriteActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_write)

        btnSend.setOnClickListener { // ์ ์กํ๊ธฐ๋ฅผ ํด๋ฆญํ๋ฉด
            setResult(Activity.RESULT_OK) // ๊ฒฐ๊ณผ๊ฐ ์ฑ๊ณต์ ์ด์๋ค๊ณ  ์ ์ฅํด์ค๋ค.
            finish() // ๋์๊ฐ๊ธฐ
        }
    }
}
```

<br>

#### **deprecated๋ ์ด์ **

+ **onActivityResult ์ฝ๋๊ฐ ๋๋ฌด ๊ธธ์ด์ง๋ค.**

  ํ๋ก์ ํธ๊ฐ ์ปค์ง๋ฉด์ ์กํฐ๋นํฐ์ ์๋ ๋์ด๋๊ณ  ๊ทธ์ ๋ฐ๋ผ onActivityResult ๋ฉ์๋ ์์ ๋ค์ด๊ฐ๋ ์ฝ๋์ ์๋ ๊ต์ฅํ ๋ฐฉ๋ํด์ง๋ค. 99๊ฐ์ ์กํฐ๋นํฐ๊ฐ ์์ผ๋ฉด 99๊ฐ๋ฅผ ํ ์ฝ๋ฐฑ ํจ์ ์์์ ๋ถ๊ธฐ ์ฒ๋ฆฌํด์ค์ผ ํ๋ค. ์ด๊ฑด ์ ์ง๋ณด์์ ์ฉ์ดํ๋๋ก ์ต๋ํ ์ฝ๋๋ฅผ ๋๋๊ณ  ๋๋๊ณ  ๋๋๋ ์์ฆ ํจ๋ฌ๋ค์์ ๋ง์ง๊ฐ ์๋ค.

+ **Permission ์์ฒญ์ด ๋ถํธํ๋ค.**

  ๊ธฐ์กด์๋ ํผ๋ฏธ์์์ฒญ์ ์์ ๊ฐ์ด ์ฌ์ฉํ์๋ค. ์์ ์ค๋ชํ startActivityForResult, onActivityResult์ ๋ฉ์๋ ์ด๋ฆ๊ณผ ์ญํ ์ ๋ค๋ฅด์ง๋ง ๊ทธ ๋ก์ง์ ๋๊ฐ๋ค. requestCode๋ก 0์ ์ฃผ๊ณ ... ์ฌ์ฉ์์๊ฒ ๊ถํ ์์ฒญ์ ๋ณด๋ด๋ฌ ๊ฐ๋ค๊ฐ ๋์์์ ๊ทธ ๊ฒฐ๊ณผ์ ๋ฐ๋ผ ์ฒ๋ฆฌ๋ฅผ ํ๋... ์ด ๊ธฐ์กด ๋ฐฉ๋ฒ์ ์ฌ์ฉํ์ ๋ ๋ถํธํ ์ ์ 

  requestCode์ ๋ฐ๋ผ ๋ถ๊ธฐ๋ฅผ ๋๋๊ณ  -> ํด๋น ๊ถํ์ ๊ฐ์ง๊ณ  ์๋์ง ์๋์ง์ ๋ฐ๋ผ ๋ ๋ถ๊ธฐ๋ฅผ ๋๋๋๋ฐ -> ํผ๋ฏธ์ ์์ฒญ์ ์ฌ๋ฌ ๊ฐ ํด์ผ ํ๋ค? -> ์ฝ๋๊ฐ ๋๋ฆฌ ๋ฒ์์ด ๋๊ฒ ๋๋ค.

=> Activity Result API์์๋ **์ด ๋ฌธ์ ๋ฅผ ํด๊ฒฐํ๊ธฐ ์ํด ActivityResultContracts ๊ฐ๋์ด ๋์**๋์๋ค.

<br><br>

#### ๐ ActivityResultContracts

##### 1. ์ฝ๋ฐฑ ์ ์ธ

registerForActivityResult ๋ฉ์๋๋ฅผ ํตํด ActivityLauncher๋ฅผ ๋ง๋๋ ๊ฒ์ผ๋ก ์์ํ๋ค.

```kotlin
private val filterActivityLauncher: ActivityResultLauncher<intent> = registerForActivityResult(ActivityResultContracts.StartActivityForResult()) {
        handleSelectedFilterItems(it)
    } 
```

+ ์กํฐ๋นํฐ์ ๋ฉค๋ฒ๋ณ์๋ก ActivityLauncher๋ฅผ ์ ์ธํ๋ค. registerForActivityResult์ ํ๋ผ๋ฏธํฐ๋ก๋ ActivityResultContract, ActivityResultCallback ์ด๋ ๊ฒ 2๊ฐ๊ฐ ํ์ํ๋ค.

+ ํด๋น ๋ฉ์๋๋ ActivityResultLauncher๊ฐ ๋ฐํ๋๋ฉฐ, <T> ์ ๋ค๋ฆญ ํ์์ ์ก**ํฐ๋นํฐ๋ฅผ ๋์ธ ๋ ํ์ํ input์ ํ์**์ด๋ค.

+ callback ๋๋ค์์๋ ActivityResult ๊ฐ์ฒด๊ฐ ํ๋ผ๋ฏธํฐ๋ก ๋จ์ด์ง๋ค. ์ฌ๊ธฐ์์ intent์ result code ๋ฑ์ ์ ๊ทผํด์ ์ด์ ์ onActivityResult์์ ๋ฐ์ดํฐ๋ฅผ ๊ฐ์ ธ์ค๋ฏ์ด ๋ก์ง์ ๊ตฌ์ฑํ๋ฉด ๋๋ค.

<br>

##### 2. ์กํฐ๋นํฐ ์คํ

```kotlin
private fun launchFilterActivity() {
    val intent = Intent(this, FilterActivity::class.java)
    intent.putExtra("awesome_key", "awesome_value")
    filterActivityLauncher.launch(intent) 
}
```

+ registerForActivityResult ๋ฉ์๋๋ฅผ ํตํด Callback๋ ์ ์ํ๊ณ , ActivityResultLauncher๋ฅผ ๋ง๋ค์์ผ๋ฉด ์์๊ฐ์ด ์คํํด์ฃผ๋ฉด ๋๋ค.
+ ์คํํ๋ ๊ฑด ๊ธฐ์กด์ฒ๋ผ intent๋ฅผ ์ ์ํด์ฃผ๊ณ , launch()๋ฉ์๋๋ฅผ ์คํํ๋ฉด์ intent๋ฅผ ๋๊ฒจ์ฃผ๋ฉด ๋์ด๋ค.

<br>

##### ActivityResultContract Custom

+ ๊ณ์ฝ์ ๊ฐ์ฒด๋ฅผ ์ปค์คํํ๋ ๊ฒ์ ๋งค์ฐ ๊ฐ๋จํ๋ค.

```kotlin
class CustomContract : ActivityResultContract<Intent, Long>() {
    override fun createIntent(context: Context, input: Intent): Intent {
        return input
    }

    override fun parseResult(resultCode: Int, intent: Intent?): Long {
        return intent?.getLongExtra("awesome_key", -1) ?: -1
    }
}
```

+ ActivityResultContract\<I, O> ์์ I๋ ๋ฐ์ฒ๋ฅผ ์คํํ  ๋์ input ํ์, O๋ ์ฝ๋ฐฑ์ผ๋ก๋ถํฐ ๋จ์ด์ง๋ ์ธ์์ ํ์์ ์ ์ด์ฃผ๋ฉด ๋๋ค.

+ createIntent ๋ฉ์๋์์๋ input์ผ๋ก๋ถํฐ Intent ๊ฐ์ฒด๋ฅผ ๋ง๋ค๋ฉด ๋๋ค. ํ์์ฒ๋ผ intent๋ฅผ ์ธํ์ผ๋ก ๋๊ธด๋ค๋ฉด ๊ทธ๋๋ก input์ ์ ๋ฌํ๋ฉด ๋๋ค.

+ parseResult๋ intent์ผ๋ก๋ถํฐ ์ ๋ฌ ๋ฐ์ ๋ฐ์ดํฐ๋ฅผ ๋ฝ์์ ๋ฆฌํดํ๋ฉด ๋๋ค. ๊ทธ๋ผ callback ์์ ํด๋น ๋ฐ์ดํฐ๋ฅผ ์ํ๋ ํ์์ผ๋ก ๊ทธ๋๋ก ๋ฐ์ ์ ์๋ค.





> ์ฐธ๊ณ   
>
> + [๋ง๋ฆฌ๋น devlog](https://modelmaker.tistory.com/18)
>
> + [ActivityResultLauncher ๋ ์์ธํ](https://onlyfor-me-blog.tistory.com/342)

