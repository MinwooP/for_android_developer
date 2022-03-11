StartActivityForResult 메서드와 onActivityResult가 Deprecated 되었기 때문에, ActivityLauncher, ActivityResultContracts 를 사용한다. 





####  startActivityForResult, onActivityResult 예제

+ `startActivityForResult`, `onActivityResult`

```kotlin
class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        btnWrite.setOnClickListener { // 작성하기를 클릭하면
            val writeIntent = Intent(this, WriteActivity::class.java) // 이동할 액티비티를 Intent에 담음
            startActivityForResult(writeIntent, 0) // 뒤에 숫자는 requestCode (이 숫자는 다음 포스팅에서 배울 예정, 지금은 아무 숫자나 넣으면 됨)
        }
    }

    // 다시 현재 액티비티로 돌아왔을 때 할 작업
    override fun onActivityResult(requestCode: Int, resultCode: Int, data: Intent?) {
        super.onActivityResult(requestCode, resultCode, data)

        when (resultCode) {
            Activity.RESULT_OK -> {
                Toast.makeText(this, "문자를 보내고야 말았어..!", Toast.LENGTH_SHORT).show()
            }

            Activity.RESULT_CANCELED -> {
                Toast.makeText(this, "하아.. 술 깨고 다시 연락해보자", Toast.LENGTH_SHORT).show()
            }
        }
    }
}
```

<br>

+ 호출된 액티비티에서 `setResult`

```kotlin
class WriteActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_write)

        btnSend.setOnClickListener { // 전송하기를 클릭하면
            setResult(Activity.RESULT_OK) // 결과가 성공적이였다고 저장해준다.
            finish() // 돌아가기
        }
    }
}
```

<br>

#### **deprecated된 이유**

+ **onActivityResult 코드가 너무 길어진다.**

  프로젝트가 커지면서 액티비티의 수도 늘어나고 그에 따라 onActivityResult 메서드 안에 들어가는 코드의 양도 굉장히 방대해진다. 99개의 액티비티가 있으면 99개를 한 콜백 함수 안에서 분기 처리해줘야 한다. 이건 유지보수에 용이하도록 최대한 코드를 나누고 나누고 나누는 요즘 패러다임에 맞지가 않다.

+ **Permission 요청이 불편하다.**

  기존에는 퍼미션요청을 위와 같이 사용했었다. 앞서 설명한 startActivityForResult, onActivityResult와 메서드 이름과 역할은 다르지만 그 로직은 똑같다. requestCode로 0을 주고... 사용자에게 권한 요청을 보내러 갔다가 돌아와서 그 결과에 따라 처리를 하는... 이 기존 방법을 사용했을 때 불편한 점은 

  requestCode에 따라 분기를 나누고 -> 해당 권한을 가지고 있는지 없는지에 따라 또 분기를 나누는데 -> 퍼미션 요청을 여러 개 해야 한다? -> 코드가 난리 법석이 나게 된다.

=> Activity Result API에서는 **이 문제를 해결하기 위해 ActivityResultContracts 개념이 도입**되었다.







#### ActivityResultContracts

##### 1. 콜백 선언

registerForActivityResult 메서드를 통해 ActivityLauncher를 만드는 것으로 시작한다.\

```kotlin
private val filterActivityLauncher: ActivityResultLauncher<intent> = registerForActivityResult(ActivityResultContracts.StartActivityForResult()) {
        handleSelectedFilterItems(it)
    } 
```

+ 액티비티의 멤버변수로 activityLauncher를 선언했다. registerForActivityResult의 파라미터로는 ActivityResultContract, ActivityResultCallback이 필요하다.

+ 해당 메서드는 ActivityResultLauncher가 반환되며, <T> 제네릭 타입은 액티비티를 띄울 때 필요한 input의 타입이다.

+ callback 람다에서는 ActivityResult 객체가 파라미터로 떨어진다. 여기에서 intent와 result code 등을 접근해서 이전에 onActivityResult에서 데이터를 가져오듯이 로직을 구성하면 된다.

<br>

##### 2. 액티비티 실행

```kotlin
private fun launchFilterActivity() {
    val intent = Intent(this, FilterActivity::class.java)
    intent.putExtra("awesome_key", "awesome_value")
    filterActivityLauncher.launch(intent) 
}
```

+ registerForActivityResult 메서드를 통해 Callback도 정의하고, ActivityResultLauncher를 만들었으면 위와같이 실행해주면 된다.
+ 실행하는 건 기존처럼 intent를 정의해주고, launch()메서드를 실행하면서 intent를 넘겨주면 끝이다.

<br>

##### ActivityResultContract Custom

+ 계약서 객체를 커스텀하는 것은 매우 간단하다.

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

+ ActivityResultContract\<I, O> 에서 I는 런처를 실행할 때의 input 타입, O는 콜백으로부터 떨어지는 인수의 타입을 적어주면 된다.

+ createIntent 메서드에서는 input으로부터 Intent 객체를 만들면 된다. 필자처럼 intent를 인풋으로 넘긴다면 그대로 input을 전달하면 된다.

+ parseResult는 intent으로부터 전달 받은 데이터를 뽑아서 리턴하면 된다. 그럼 callback 에서 해당 데이터를 원하는 타입으로 그대로 받을 수 있다.





+ 참고  : [말리빈 devlog](https://modelmaker.tistory.com/18)

  