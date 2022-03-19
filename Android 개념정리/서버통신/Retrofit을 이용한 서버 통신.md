# 🚩Retrofit을 이용한 서버 통신

-----

### 📌 서버통신 시 필요한 과정

##### POSTMAN

+ 서버개발자와 필요한 데이터 논의

  => data 뭐 필요하니 ? 어떤 method 보내줄까? 라고 서버개발자분들이 물어봄

+ 서버 API 문서 확인 후 Postman으로 테스트

<br>

##### 구현부분 ⭐

1. Retrofit 라이브러리 추가 및 AndroidManifest 설정

2. 서버 **Request, Response Data class 설계** 

   => 클라에선 request data를 보내고, 서버에서는 이에 대한 응답으로 Response 바디를 클라한테 줌. 이 두개 data 모두가 클라에 있어야 제대로 작동할 것이므로 이를 설계

3. Retrofit 인터페이스 설계 및 Retrofit 인터페이스 실제 구현체 만들기

   => POST해서 여기에 무슨 data 넣어서 서버에 보내라라고 명세가 되어있는 것이 retrofit interface이고 이를 직접 객체로 만들어주는 것이 Retrofit interface 구현체(ex) serviceCreator) 이다.

4. Callback 등록하여 통신 요청

   => 만든 객체를 통해서 통신을 한 것을 화면에 띄워주는 역할

<br>

-----

### 📌 서버통신 자세히 알아보자

#### 1️⃣ 라이브러리 추가 및 AndroidManifest 설정

<img src="https://user-images.githubusercontent.com/31370590/140907438-e93b0a78-6c75-4b18-a83b-35bd20fa02bf.PNG">

+ gson이란 ?

  java에서 **Json을 파싱하고, 생성하기 위해** 사용되는 도구

  => retrofit2는 서버 통신을 위한 라이브러리로, HTTP API를 자바 인터페이스 형태로 사용하는 라이브러리이다. 따라서 **Java <-> Json**(자바에서 JSON을 파싱할 수 있고, JSON에서 자바로 바꾸는 것도 가능. 양방향 가능)의 gson을 쓸 수 있는 것이다. 

  => retrofit2 자체에는 JSON을 해석해서 Kotlin data file이나 java data file로 변환할 수 있는 자체 컨버터를 갖고 있지 않다. 이를 대신 해줄 라이브러리가 gson이다.  

  => json을 안드로이드에 맞는 데이터 클래스로 바꿔주는 과정이 필요함 -> gson이 이를 해준다.

  => 서버 통신을 가능하게 해주는 것은 Retrofit2 이지만, json을 해석할 수 있도록 하는 것은 gson 컨버터이다. 

<img src="https://user-images.githubusercontent.com/31370590/140908339-847bad23-8533-4811-a059-d164329bd7c7.PNG">

<br><br>

#### 2️⃣ 서버 Request / Response 객체 설계

위키에서도 봤듯이 request body, response body가 있었음. 이들을 받아오기 위해 이들을 매핑해주는 data class를 만들어줘야 retrofit에서 JSON을 이 data class로 변환하면 되겠구나! 하고 변환해줌. 그래서 data class를 만들어줄 것임

`Request Body`

```json
{
    "email" : "kimwy1997@gmail.com",
    "password" : "123456"
}
```

=>

`RequestLoginData.kt`

```kotlin
package org.sopt.androidseminar

import com.google.gson.annotations.Serializename

data class RequestLoginData(
	@SerializeName("email")
	val id : String,
	val password : String
)
```

<br>

`Response Body`

```json
{
    "status": 200,
    "success": true,
    "message": "로그인 성공",
    "data": {
        "id": 1,
        "name": "김우영",
        "email": "kimwy1997@gmail.com"
    }
}
```

=>

`ResponseLoginData.kt`

```kotlin
package org.sopt.androidseminar

data class ResponseLoginData(
	val status : Int,
	val success : Boolean,
	val message : String,
	val data : Data
) {
    data class Data(
    	val id : Int,
    	val name : String,
    	val email : String
    )
}
```

<br>

+ 이렇게 **Json 객체의 키 값과 타입을 각각 데이터 클래스의 변수명과 타입에 일치 시켜주면**

  => 서버로부터 받아오는 Response의 경우 Retrofit 구현체에 추가되는 gsonConverter가 gson 데이터를 방금 만든 ResponseData로 변환시켜 주게 되고, 반대로 RequestData의 경우 gson 데이터로 변환시켜 서버에 전달해주게 된다. 

  => 컨버터가 다 해줘서 우리가 할 일은 Request/Response 객체를 설계하는 것 말고는 딱히 없다. 

<br>

+ Serialized name

  <img src = "https://user-images.githubusercontent.com/31370590/140910967-bc07bf43-0b3e-4e43-9aef-e0ba64e03d2c.PNG">

<br>

+ 중첩 클래스 구조

  <img src="https://user-images.githubusercontent.com/31370590/140911251-c1d1bb05-948a-4421-be97-e6dd6b77f9ac.PNG">

<br><br>

#### 3️⃣ Retrofit Interface 설계

명세서 같은 역할

##### Retrofit Interface란?

=> ***서버에 어떠한 요청을 보내면 어떻게 온다*는 일종의 상호작용 방법을 정의**하는 부분 

=> 아까 봤던 http 메소드, UIR, 헤더 등등을 정의하는 부분

<br>

##### Retrofit Interface 설계

<img src="https://user-images.githubusercontent.com/31370590/140914448-d9abfcba-67f1-477f-8d16-6f0f9673a2c4.PNG">

+ 코틀린 파일을 하나 만들고, 클래스 타입은 interface, interface는 상속 받고, 구현해줘야 한다. interface type을 쓰는 이유는 retrofit에서 Service 객체를 만들어 줄 때 interface 파일을 넣어서 만들도록 method가 설계되어있다. 

+ 클라이언트와 서버와의 통신 과정이 우리 일반 세상에서의 service와 비슷하기 때문에 `~service` 라고 이름을 짓는 것이다. 

+ POST method를 사용할 것이므로 `@POST`를 써주고, `@POST( )`안에 정확히 어떤 URI에서 이를 수행하는지 적어준다. 

+ 함수 안에는 이 http 메서드를 실행시켰을 때 전달할 RequestBody 데이터와 전달받을 Response data값을 넣어준다. Body값 넣을 때도 `@Body`라고 annotation을 명시해줘야한다. 

+ POST, PUT은 Body값 가능

  GET, DELETE는 Body값 X  

+ Response에 해당하는 객체가 JSON Object일 때, `Call<ResponseLoginData>`

  Response에 해당하는 객체가 JSON Array타입일 때 `Call<List<ResponseLoginData>>`

  이렇게 해줘야 한다. 

<br><br>

#### 4️⃣ Retrofit Interface 실제 구현체(객체) 만들기

 Retrofit Interface 실제 구현체란? => Retrofit 객체다 그냥

<img src="https://user-images.githubusercontent.com/31370590/140919363-312e2582-d8c1-40a8-821a-f3329fc38653.PNG">

+ 왜 Object 타입인가 ?

  서버 호출이 필요할 때마다 Retrofit 객체를 만들어야 한다면 너무 비효율적이기 때문에 Retrofit 객체의 경우 **싱글톤(Object)**으로 제작하는 것이 바람직하다 !

  > 싱글톤이란?
  >
  > 최초 한번 생성이 되었을 때 메모리에 계속 상주하도록 하고 그 이후로는 삭제가 되지 않고 접근할 수 있도록 최초 한번만 메모리를 할당하고(Static) 그 메모리에 인스턴스를 만들어 사용하는 디자인패턴
  >
  > 쉽게 말하자면 앱 통틀어서 하나만 생성되는 객체 ! kotlin의 경우 object 키워드를 이용해 이러한 싱글톤 객체를 만들기 쉽다

<br><br>

#### 5️⃣ Callback 등록하여 통신 요청

이렇게 서버 통신을 할 수 있는 Retrofit 객체가 완성이 됐는데 이를 가지고 궁극적으로 해야할 일은 **data를 받아와서 View에 띄워주는 일**이다. 

+ `Call<Type>` : 서버에 이 `Type` 주세요 ! 하는 것

  => 동기적 또는 비동기적으로 `Type`을 받아오는 객체

+ `Callback<Type>` : Type 객체를 받아왔을 때 프로그래머의 행동

  => Call 객체를 통해 반환을 받고 나면 그 이후에 어떤 행동을 실행을 시키게 할지 정의하는 부분으로 사용자 정의가 가능함

<br>

##### 📌 `LoginActivity.kt` 전체코드 

```kotlin
private fun initNetwork(){ // 네트워크를 초기화하는 함수
    val requestLoginData = RequestLoginData(
        email = binding.etId.text.toString(),
        password = binding.etPass.test.toString()
    )

    val call: Call<ResponseLoginDat> =  ServiceCreator.sampleService.postLogin(requestLoginData)

    call.enqueue(object : Callback<ResponseLoginData> {
        override fun onResponse(
            call: Call<ResponseLoginData>,
            response: Response<ResponseLoginData>
        ) {
            if(response.isSuccessful){
                val data = response.bodyy()?.data

                Toast.makeText(this@MainActivity, "${data?.email}님 반갑습니다!", Toast.LENGTH_SHORT).show()
                startActivity(Intent(this@MainActivity, SecondActivity::class,java))
            } else
                Toast.makeText(this@MainActivity, "로그인에 실패하였습니다", Toast.LENGTH_SHORT).show()
        }

        override fun onFailure(call: Call<ResponseLoginData>, t: Throwable){
            Log.e("NetworkTest", "error:$t")
        }
    }
}
```

<br>

##### 📌 전체코드 하나하나씩 자세히 보자

```kotlin
val requestLoginData = RequestLoginData(
    email = binding.etId.text.toString(),
    password = binding.etPass.test.toString()
    )
```

+ 우선, 통신할 때 필요한 request 데이터를 보통 로그인할 때 `editText`로 id나 password로 입력받으므로 **editText의 값에 접근해서 이를 RequestLoginData 클래스의 생성자의 매개변수의 인자로 전달해서 객체를 생성**함. 

<br>

```kotlin
val call: Call<ResponseLoginData> = ServiceCreator.sampleService.postLogin(requestLoginData)
```

+ 아까 서비스를 만들어주는 구현체를 만들고, 거기서 서비스 객체를 구체화시켜줬는데 그 서비스 객체안에는 `postLogin()`이라는 함수를 명세해주었음. 
  이제 그 함수를 호출하기 위해 `ServiceCreator`안의 `sampleService`안의 `postLogin()`를 호출하는데 여기서 body 값으로 아까 위에서 생성해준 `requestLoginData` 라는 data class 객체를 넣어줌.

+ 아까 구현해준 `postLogin()` 함수와 지금 `call` 변수의 반환 타입이 `Call<ResponseLoginData>`이다. 잘 통신하고 나면 `Call<ResponseLoginData>`가 반환이 될텐데,  call이라는 변수를 만들어서 이안에 반환된 data를 넣어준다. 

<br>

```kotlin
call.enqueue(object : Callback<ResponseLoginData> {
```

+ 이제 `call`이라는 변수를 실행시켜준 다음, 콜백 메서드로 UI에 띄워주는 작업을 해줘야 함. 서버 통신 같은 경우는 비동기 처리로 해줘야 함. 그래서 call을 실행시켜줄 때 `enqueue()`라는 함수를 호출해주는데 이는 비동기 처리로 작업해줌.(`execute()`는 동기처리) 

+ `enqueue`로 `call`객체를 실행시켜준 다음 `call`객체가 실행되고 난 후 받아오는 `callback`으로 어떤 작업을 해줄지 선언해준다. 

  => 즉, `enqueque()`안에 있는 부분들이 콜백에 대한 내용들   

+ `Callback`을 받아오게 되면 무조건 override 해줘야 하는 함수 2가지

  + `onResponse()` : 서버 통신이 일단 이루어졌다면

    => 메시지에 따라 어떤 행동을 해줘야 할지

  + `onFailure()` : 서버 통신이 잘 안되었을 때

    => 에러 처리를 해주는 코드를 작성해줘야함

<br>

```kotlin
 override fun onResponse(
            call: Call<ResponseLoginData>,
            response: Response<ResponseLoginData>
        ) {
            if(response.isSuccessful){
                val data = response.bodyy()?.data

                Toast.makeText(this@MainActivity, "${data?.email}님 반갑습니다!", Toast.LENGTH_SHORT).show()
                startActivity(Intent(this@MainActivity, SecondActivity::class,java))
            } else
                Toast.makeText(this@MainActivity, "로그인에 실패하였습니다", Toast.LENGTH_SHORT).show()
        }
```

+ 서버 통신이 이루어졌다면 받은 메시지에 따라 어떤 행동을 해줘야 할지  
+ 응답받아온 친구의 값들 중에는 status 코드도 있겠지만, 이 서버 통신의 성공여부를 나타내주는 `isSuccessful`이라는 Boolean type 변수가 있다. 이를 통해 성공했을 시 response body 안에 있는 data를 이용해 처리 ~ 작업 ~, else 에서는 응답이 오긴 왔는데, 부정적인 응답이 왔을 때에 대한 작업 ~

<br>

> 참고
>
> + SOPT 29기 안드로이드 파트 세미나

-----





















----

### 🌟 Generic Class에 대해 확장함수를 추가 => 서버 코드 재사용

원래 서버 통신 코드

```kotlin
val call: Call<ResponseLoginData> =  ServiceCreator.sampleService.postLogin(requestLoginData)

call.enqueue(object : Callback<ResponseLoginData> {
        override fun onResponse(call: Call<ResponseLoginData>, response: Response<ResponseLoginData>) {
            if(response.isSuccessful){
                val data = response.body()?.data
                Toast.makeText(this@MainActivity, "${data?.email}님 반갑습니다!", Toast.LENGTH_SHORT).show()
                startActivity(Intent(this@MainActivity, SecondActivity::class,java))
            } else
                Toast.makeText(this@MainActivity, "로그인에 실패하였습니다", Toast.LENGTH_SHORT).show()
        }

        override fun onFailure(call: Call<ResponseLoginData>, t: Throwable){
            Log.e("NetworkTest", "error:$t")
        }
}
```



Generic Class에 대해 확장함수 추가

=> `ResponseType`이라는 타입에 대한 Call 클래스에 대해 확장함수를 추가

=> `Call< >`안에 어떤 객체 타입이 담겨도, `enqueueUtil` 함수를 사용할 수 있도록 이를 확장함수로 만들어 놓는 것

=> **fun <E> 클래스이름<E>.함수이름(인자타입): 리턴타입 {구현부}** 로 정의가능

<img src="https://user-images.githubusercontent.com/31370590/159102693-3e06c633-9a61-4a26-b00d-68ea759147d9.PNG">

확장함수를 이용한 코드

```kotlin
call.enqueueUtil ( 
	onSuccess = { data ->  // 여기서 data는 onResonse의 response.body 이므로 data에 접근하려면 data.data~ 로 접근해야한다. 
                shortToast("${data.data.name}님 반갑습니다")
                }
)
```



