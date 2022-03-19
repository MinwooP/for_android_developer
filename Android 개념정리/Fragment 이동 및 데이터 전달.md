# 프래그먼트 간 이동 및 데이터 전달

-------

## 📌 프래그먼트 간 이동

+ Fragment는 기본적으로 액티비티 위에서 동작하기 때문에 비슷한 구조와 특징을 갖고있다. 액티비티간 이동은 시스템에서 Intent로 하듯이, Fragment는 Fragment Manager를 통해 이동한다.
  이때 Fragment는 Activity위에서 동작하기 때문에 Intent가 아닌 메소드 호출을 통해 이동하게된다.

<br>

#### Activity에서 Fragment로 전환하기

=> supportFragmentManager() 호출

```kotlin
class MainActivity : FragmentActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val fragment_main = MainFragment()
        val fragment_menu = MenuFragment()

        val button_main = findViewById<Button>(R.id.button_main)
        val button_menu = findViewById<Button>(R.id.button_menu)
        
        button_main.setOnClickListener{
                supportFragmentManager()
                .beginTransaction()
                .replace(R.id.framelayout, fragment_main)
                .commit()
            }

        
        button_menu.setOnClickListener{
                supportFragmentManager()
                .beginTransaction()
                .replace(R.id.framelayout, fragment_menu)
                .commit()
        }
    }
}
```

<br>

#### Fragment에서 Fragment로 전환하기

앞서 Activity에서 Fragment로 전환할 때와 다르게 Fragment에서 Fragment로 전환하는 것은 이동할 Fragment가 자신의 하위레벨이 아니기 때문에 직접 제어가 불가능하다. 따라서 상위 레벨인 Activity에서 제어해줘야 한다.

`MainActivity`에 하위 Fragment를 이동시켜줄 함수를 정의한다. 

```kotlin
fun changeFragment(index: Int){
    when(index){
        1 -> {
        supportFragmentManager()
        .beginTransaction()
        .replace(R.id.framelayout, fragment_main)
        .commit()
        }
        
        2 -> {
        supportFragmentManager()
        .beginTransaction()
        .replace(R.id.framelayout, fragment_menu)
        .commit()
        }
    }
}
```

=>

하위 Fragment에서는 상위 Acitivty에 정의된 메서드를 이용해 작업을 정의한다. 여기서는 Fragment의 버튼을 클릭했을 때 Fragment가 전환될 수 있도록 버튼에 listener를 달고 그 안에서 메서드를 호출해주었다. 

```kotlin
class MainFragment : Fragment() {

    fun onCreateView(inflater: LayoutInflater , container: ViewGroup? , savedInstanceState Bundle?): View? {
        val rootView = inflater.inflate(R.layout.fragment_main, container, false)
		
        val mActivity = activity as MainActivity
        val btn_change = rootView.findViewById(R.id.button_change);
        btn_change.setOnClickListener{
                activity.changeFragment(2)
	}
        return rootView
    }
}
```

<br>

-----

## 📌 프래그먼트 간 데이터 전달

주로 Bundle로 하는 듯 ? ^^



















> 참고
>
> + [Fragment간 이동](https://velog.io/@appletorch/Activity-to-Fragment-Fragment-to-Fragment)
>
> + [Fragment간 데이터 전달 방법들](https://velog.io/@appletorch/Activity-to-Fragment-Fragment-to-Fragment)