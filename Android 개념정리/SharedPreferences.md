# 🚩 SharedPreferences

#### 📌 영속성 데이터

+ 데이터를 생성한 **애플리케이션의 실행이 종료되지 않더라도 사라지지 않는** 데이터

+ 안드로이드에서는 여러개의 로컬저장소를 제공한다.

  대표적인 4가지 저장소

  1. Room

  2. Data Store

  3. **SharedPreferences**

     **key - value** collection을 이용해 간단한 데이터 저장이 가능한 대표적인 로컬 DB

  4. Media Store

+ 로컬저장소의 원리

  앱이 꺼져도 데이터가 유지가 되어야하기 때문에 로컬저장소를 사용하게 될 경우 **하드디스크**에 데이터를 저장하게 된다. 

<br>

#### 📌 SharedPreferences

+ 간단한 데이터를 key-value 형식으로 저장할 수 있게 해주는 로컬 저장소

+ 기본 자료형의 읽기, 쓰기만 지원
+ 애플리케이션 내부에서만 접근 가능 
+ 비교적 간단한 데이터 저장에 용이!

​	=> 보안에 좋은 편은 아님. XML 파일에 데이터를 저장하는 식으로 작동하게 되는데,  가상머신으로 XML 파일을 볼 수가 있음. 

<br>

1. 하나의 Activity에서만 사용할 때

   `val sharedPref = activity?.getPreferences(Context.MODE_PRIVATE)`

   + `getPreferences` => 

   + `MODE_PRIVATE` => 이 저장소를 앱 내부에서만 볼 수 있게 해주세요

2. 앱 전역에서 사용하고자 할 때

   ```kotlin
   val sharedPref = activity?.getSharedPreferences(
   getString(R.string.preference_file_key), Context.MODE_PRIVATE)
   ```

   + 파일 이름 지정 시 앱에서 고유하게 식별할 수 있도록

     => 파일 이름 앞에 애플리케이션 ID를 주로 붙임

   + 첫 번째 매개변수(파일명)로 식별되는 앱 전역에서 SharedPreferences를 사용하고 싶을 때는 getSharedPreferences() 메서드를 사용한다. 

     => 즉, 첫번재 매개변수로 들어가는 `R.string.preference_file_key`가 현재 앱을 나타내는 파일명이다. 이를 `getSharedPreferences()`의 인자로 넘겨줘야 하는 것. 

<br>

-----

#### 🚩 SharedPreferences 사용해보기

#### 1️⃣ 자동로그인을 위한 Selector 생성 & 배치

<img src="https://user-images.githubusercontent.com/31370590/159114887-5276da0d-d671-4b8a-b894-a27f16ab8d0a.PNG">

<img src="https://user-images.githubusercontent.com/31370590/159114898-ce633e55-c77f-4c20-a5a7-bbd8440c2fe6.PNG" width = "700" height = "500">

<br>

#### 2️⃣  SharedPreferences 생성

<img src="https://user-images.githubusercontent.com/31370590/159114937-a796b64e-1103-4350-a936-9e253fa5324e.PNG" width = "700" height = "500">

##### 코드 자세히 보자 !

```kotlin
object SOPTSharedPreferences{
    private const val STORAGE_KEY = "USER_AUTH"
    private const val AUTO_KEY = "AUTO_LOGIN"
}
```

+ SharedPreferencs의 경우 앱 전역에서 계속해서 호출되므로 object 키워드로 싱글톤으로 만들어줌

+ SharedPreferencs에서 사용하는 Key값들을 상수화

<br>

```kotlin
object SOPTSharedPreferences{
    
    fun getAutoLogin(context: Context): Boolean { // AutoLogin 상태가 설정되어있는지를 참, 거짓으로 반환하는 함수
        val preferences = context.getSharedPreferences(STORAGE_KEY, Context.MODE_PRIVATES) // 일단 getSharedPreference로 SharedPreferences에 접근
        return preferences.getBoolean(AUTO_LOGIN, false) // SharedPreferences에 접근해서 AUTO_LOGIN 키 값으로 접근해 AutoLogin 상태가 설정되어있는지를 반환
    }
    
}
```

파일 읽기

+ **get자료형(key, defaultValue)** 형식으로 파일에서 key값에 해당하는 값을 읽을 수 있음

<br>

```kotlin
object SOPTSharedPreferences{
    
    fun setAutoLogin(context: Context): Boolean {
        val preferences = context.getSharedPreferences(STORAGE_KEY, Context.MODE_PRIVATE) // 아까 파일 읽기와 마찬가지로 일단 getSharedPreference로 SharedPreferences에 접근
        preferences.edit() // 이번엔 get~가 아닌 edit()을 호출후, put~을 호출, 끝나고 apply까지 
        	.putBoolean(AUTO_LOGIN, value)
        	.apply()
    }
    
}
```

+ 파일쓰기

  + 파일 작성을 위해 edit() 호출

  + **put자료형(key, value)** 형태로 파일에 작성할 수 있음

  + 모든 작성이 끝나면 commit() 혹은 apply() 호출 !

    > 파일의 변경사항을 저장하는 메서드 2가지 비교
    >
    > commit() 
    >
    > => 메모리내에서도 동기적으로 값을 변경, 디스크내에서도 **동기적**으로 값을 입력 
    >
    > => SharedPreferences의 작업이 파일 입출력 작업인만큼 메인 스레드에서 호출하면 ANR(앱의 강제 종료)를 일으킬 수 있음
    >
    > apply() 
    >
    > => 메모리내에서는 동기적으로 값을 변경, 디스크내에서는 **비동기적**으로 값을 입력
    >
    > => ANR을 따로 일으키지는 않음

<br>

#### 3️⃣ SharedPreferences 이용 자동 로그인 구현

<img src="https://user-images.githubusercontent.com/31370590/159130059-cff8ef2d-d17b-4fec-94ab-e518862728e6.PNG">

+ `initClickEvent()` 메서드를 통해 체크버튼을 클릭함으로서 자동로그인을 설정할 수 있도록 한다.
+ `isAutoLogin()` 메서드를 통해 자동로그인 상태를 체크해, 자동로그인 상태라면 바로 다음 Activity로 이동
+ 위 두 메서드를 `onCreate()` 안에 정의함으로써 액티비티 시작 시, 자동로그인을 체크하도록 한다. 

<br>

#### 4️⃣ 현재 자동로그인 문제점

+ 실제로 앱을 개발할 때는 서버에서 로그인 시에 클라이언트에게 사용자 Token을 주게 된다. 사용자 Token은 유저별 DB를 구분하기 위해 서버가 클라이언트에게 주게 되는 것이다. 보통 우리는 유저가 로그인 시도를 했을 때 이 토큰을 서버로부터 받아와 SharedPreferences와 같은 로컬 저장소에 저장하게 된다.  그런데 사용자 Token의 경우 만료기한이 있다. 

  이 만료기한이 지나게되면 다시 로그인을 해서 서버로부터 사용자 Token을 재발급해야 한다. 만약 지금처럼 자동로그인 로직을 짜버린다면, Token의 기한이 만료되었음에도 불구하고 자동로그인이 되버린다. 

  > 원래는 이렇게 입력되는 ID마다 다른 Token을 주지만, 우리는 id 입력 건너뛰고 특정 id에 해당하는 특정 token을 그냥 string으로 헤더에 박아버렸다. 







#### 📌 실제 SharedPreferences를 이용한 자동로그인 설정

+ 위에서는 따로 아이디나 비밀번호가 아닌 **AutoLogin상태**만을 SharedPreferences에 저장해 구현했지만, 실제로는 아이디와 비밀번호를 입력받아 이를 SharedPreferences에 저장하고

  ```kotlin
  if(autoLogin.isChecked()) {
            // 자동 로그인 데이터 저장
            SharedPreferences auto = getSharedPreferences("autoLogin", Activity.MODE_PRIVATE);
            SharedPreferences.Editor autoLoginEdit = auto.edit();
            autoLoginEdit.putString("userId", userId);
            autoLoginEdit.putString("passwordNo", passwordNo);
            autoLoginEdit.putString("userRole", loginInfo.getUserRole());
            autoLoginEdit.putString("userName", loginInfo.getUserNm());
            autoLoginEdit.commit();
  }
  ```

  나중에 로그인 할 때 자동로그인 설정이 되어있었으면, SharedPreferences에서 이를 불러와 아이디, 비밀번호 입력 창에 넣어주는 것이다.

  ```kotlin
  // 자동로그인 처리
  SharedPreferences auto = getSharedPreferences("autoLogin", Activity.MODE_PRIVATE);
  userId = auto.getString("userId", null);
  passwordNo = auto.getString("passwordNo", null);
  
  // 아이디 비밀번호
  if(userId != null && passwordNo != null){
      login(); // 불러온 id와 비밀번호를 저장해 로그인 
  }else{
      
  }
  ```



> 참고
>
> + [[Android SharedPreferences로 자동 로그인 구현하기](https://pamyferret.tistory.com/21)







❓ 우리가 세미나에서 했던 거는 자동로그인상태값을 SharedPreferences에 저장해 로그인할 때 SharedPreferences에 접근해서 이 자동로그인 상태 값이 true이면 자동으로 다음액티비티로 넘어가게 해줬는데 실제로는 자동로그인이 체크되어있으면 유저의 id와 비밀번호를 SharedPreferences에 저장해서 다음에 앱 접근할 때 이 id와 비밀번호 불러와서 이걸 서버에 보내서 자동으로 로그인되게 하는 식인건가?

=> 맞음



❓ 아이디, 비밀번호 뿐만 아니라 자동로그인을 체크했는지를 알려주는 자동로그인상태값도 true인지 false인지 따로 저장해서, 처음에 이거에 접근해서 true이면 id랑 비밀번호 불러오고, 아니면 자동로그인 x인건가 ?

=> 맞음



마져 소셜은 아이디랑 비번 저장할 필요없응께 ! 다른 프로젝트에서는 매번 로그인할때마다 엑세스, 리프레쉬 토큰을 넘겨줘야해서 얘네는 로그인할때 유저 데이터를 싱글톤 클래스에 저장해두고 계속 사용했었고, 자동로그인할때는 그냥 최초로그인 이력만 있으면 바로 엑세스, 리프레쉬 토큰발급받아서 싱글톤 클래스에 저장해두고 계속 썻어 (최초로그인 여부만 SharedPreferences에 저장햇었구!)



=> 그럼 우리는 최초로그인 여부를 SharedPreferences에 저장해놓고, 이게 true이면, 싱글톤 객체에 정의되어있는 엑세스, 리프레쉬 토큰 얻어오는 메서드를 실행시켜서, 엑세스, 리프레쉬 토큰 얻어와서 이를 싱글톤 객체에 저장하고, 앱에서 사용할 때는 이 싱글톤 객체에 접근해서 사용

=> 싱글톤 객체안에 id, refreshtoken, accessToken이 있는 거고 
서버 통신해서 id, refreshtoken, accessToken의 값을 변경해주는 loginWithKaKao 메서드도 싱글톤 객체안에 선언해주는 거구나



자동로그인이 체크되어있으면->원래는 유저가 카카오로시작하기 버튼눌러야 실행되는 로직인, 카카오서버에서 엑세스,리프레시 토큰얻어오는 메서드(이는 싱글톤 객체에 정의되어있음)을 자동로그인에서는 걍 바로 실행시켜서->얻어온 엑세스 토큰, 리프레쉬 토킅을 싱글톤 클래스에 저장하고->저장한것들을 매번 api호출에서 가져다 쓴다

어찌됐든 자동로그인이든 그냥로그인이든 액세스랑 리프레쉬 토큰은 그때마다 새로 얻어와야하는거고, 이걸 이제 실행되는 동안은 싱글톤 객체에 저장해서 쓴다는거지?