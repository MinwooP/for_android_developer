# ๐ฉRetrofit์ ์ด์ฉํ ์๋ฒ ํต์ 

-----

### ๐ ์๋ฒํต์  ์ ํ์ํ ๊ณผ์ 

##### POSTMAN

+ ์๋ฒ๊ฐ๋ฐ์์ ํ์ํ ๋ฐ์ดํฐ ๋ผ์

  => data ๋ญ ํ์ํ๋ ? ์ด๋ค method ๋ณด๋ด์ค๊น? ๋ผ๊ณ  ์๋ฒ๊ฐ๋ฐ์๋ถ๋ค์ด ๋ฌผ์ด๋ด

+ ์๋ฒ API ๋ฌธ์ ํ์ธ ํ Postman์ผ๋ก ํ์คํธ

<br>

##### ๊ตฌํ๋ถ๋ถ โญ

1. Retrofit ๋ผ์ด๋ธ๋ฌ๋ฆฌ ์ถ๊ฐ ๋ฐ AndroidManifest ์ค์ 

2. ์๋ฒ **Request, Response Data class ์ค๊ณ** 

   => ํด๋ผ์์  request data๋ฅผ ๋ณด๋ด๊ณ , ์๋ฒ์์๋ ์ด์ ๋ํ ์๋ต์ผ๋ก Response ๋ฐ๋๋ฅผ ํด๋ผํํ ์ค. ์ด ๋๊ฐ data ๋ชจ๋๊ฐ ํด๋ผ์ ์์ด์ผ ์ ๋๋ก ์๋ํ  ๊ฒ์ด๋ฏ๋ก ์ด๋ฅผ ์ค๊ณ

3. Retrofit ์ธํฐํ์ด์ค ์ค๊ณ ๋ฐ Retrofit ์ธํฐํ์ด์ค ์ค์  ๊ตฌํ์ฒด ๋ง๋ค๊ธฐ

   => POSTํด์ ์ฌ๊ธฐ์ ๋ฌด์จ data ๋ฃ์ด์ ์๋ฒ์ ๋ณด๋ด๋ผ๋ผ๊ณ  ๋ช์ธ๊ฐ ๋์ด์๋ ๊ฒ์ด retrofit interface์ด๊ณ  ์ด๋ฅผ ์ง์  ๊ฐ์ฒด๋ก ๋ง๋ค์ด์ฃผ๋ ๊ฒ์ด Retrofit interface ๊ตฌํ์ฒด(ex) serviceCreator) ์ด๋ค.

4. Callback ๋ฑ๋กํ์ฌ ํต์  ์์ฒญ

   => ๋ง๋  ๊ฐ์ฒด๋ฅผ ํตํด์ ํต์ ์ ํ ๊ฒ์ ํ๋ฉด์ ๋์์ฃผ๋ ์ญํ 

<br>

-----

### ๐ ์๋ฒํต์  ์์ธํ ์์๋ณด์

#### 1๏ธโฃ ๋ผ์ด๋ธ๋ฌ๋ฆฌ ์ถ๊ฐ ๋ฐ AndroidManifest ์ค์ 

<img src="https://user-images.githubusercontent.com/31370590/140907438-e93b0a78-6c75-4b18-a83b-35bd20fa02bf.PNG">

+ gson์ด๋ ?

  java์์ **Json์ ํ์ฑํ๊ณ , ์์ฑํ๊ธฐ ์ํด** ์ฌ์ฉ๋๋ ๋๊ตฌ

  => retrofit2๋ ์๋ฒ ํต์ ์ ์ํ ๋ผ์ด๋ธ๋ฌ๋ฆฌ๋ก, HTTP API๋ฅผ ์๋ฐ ์ธํฐํ์ด์ค ํํ๋ก ์ฌ์ฉํ๋ ๋ผ์ด๋ธ๋ฌ๋ฆฌ์ด๋ค. ๋ฐ๋ผ์ **Java <-> Json**(์๋ฐ์์ JSON์ ํ์ฑํ  ์ ์๊ณ , JSON์์ ์๋ฐ๋ก ๋ฐ๊พธ๋ ๊ฒ๋ ๊ฐ๋ฅ. ์๋ฐฉํฅ ๊ฐ๋ฅ)์ gson์ ์ธ ์ ์๋ ๊ฒ์ด๋ค. 

  => retrofit2 ์์ฒด์๋ JSON์ ํด์ํด์ Kotlin data file์ด๋ java data file๋ก ๋ณํํ  ์ ์๋ ์์ฒด ์ปจ๋ฒํฐ๋ฅผ ๊ฐ๊ณ  ์์ง ์๋ค. ์ด๋ฅผ ๋์  ํด์ค ๋ผ์ด๋ธ๋ฌ๋ฆฌ๊ฐ gson์ด๋ค.  

  => json์ ์๋๋ก์ด๋์ ๋ง๋ ๋ฐ์ดํฐ ํด๋์ค๋ก ๋ฐ๊ฟ์ฃผ๋ ๊ณผ์ ์ด ํ์ํจ -> gson์ด ์ด๋ฅผ ํด์ค๋ค.

  => ์๋ฒ ํต์ ์ ๊ฐ๋ฅํ๊ฒ ํด์ฃผ๋ ๊ฒ์ Retrofit2 ์ด์ง๋ง, json์ ํด์ํ  ์ ์๋๋ก ํ๋ ๊ฒ์ gson ์ปจ๋ฒํฐ์ด๋ค. 

<img src="https://user-images.githubusercontent.com/31370590/140908339-847bad23-8533-4811-a059-d164329bd7c7.PNG">

<br><br>

#### 2๏ธโฃ ์๋ฒ Request / Response ๊ฐ์ฒด ์ค๊ณ

์ํค์์๋ ๋ดค๋ฏ์ด request body, response body๊ฐ ์์์. ์ด๋ค์ ๋ฐ์์ค๊ธฐ ์ํด ์ด๋ค์ ๋งคํํด์ฃผ๋ data class๋ฅผ ๋ง๋ค์ด์ค์ผ retrofit์์ JSON์ ์ด data class๋ก ๋ณํํ๋ฉด ๋๊ฒ ๊ตฌ๋! ํ๊ณ  ๋ณํํด์ค. ๊ทธ๋์ data class๋ฅผ ๋ง๋ค์ด์ค ๊ฒ์

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
    "message": "๋ก๊ทธ์ธ ์ฑ๊ณต",
    "data": {
        "id": 1,
        "name": "๊น์ฐ์",
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

+ ์ด๋ ๊ฒ **Json ๊ฐ์ฒด์ ํค ๊ฐ๊ณผ ํ์์ ๊ฐ๊ฐ ๋ฐ์ดํฐ ํด๋์ค์ ๋ณ์๋ช๊ณผ ํ์์ ์ผ์น ์์ผ์ฃผ๋ฉด**

  => ์๋ฒ๋ก๋ถํฐ ๋ฐ์์ค๋ Response์ ๊ฒฝ์ฐ Retrofit ๊ตฌํ์ฒด์ ์ถ๊ฐ๋๋ gsonConverter๊ฐ gson ๋ฐ์ดํฐ๋ฅผ ๋ฐฉ๊ธ ๋ง๋  ResponseData๋ก ๋ณํ์์ผ ์ฃผ๊ฒ ๋๊ณ , ๋ฐ๋๋ก RequestData์ ๊ฒฝ์ฐ gson ๋ฐ์ดํฐ๋ก ๋ณํ์์ผ ์๋ฒ์ ์ ๋ฌํด์ฃผ๊ฒ ๋๋ค. 

  => ์ปจ๋ฒํฐ๊ฐ ๋ค ํด์ค์ ์ฐ๋ฆฌ๊ฐ ํ  ์ผ์ Request/Response ๊ฐ์ฒด๋ฅผ ์ค๊ณํ๋ ๊ฒ ๋ง๊ณ ๋ ๋ฑํ ์๋ค. 

<br>

+ Serialized name

  <img src = "https://user-images.githubusercontent.com/31370590/140910967-bc07bf43-0b3e-4e43-9aef-e0ba64e03d2c.PNG">

<br>

+ ์ค์ฒฉ ํด๋์ค ๊ตฌ์กฐ

  <img src="https://user-images.githubusercontent.com/31370590/140911251-c1d1bb05-948a-4421-be97-e6dd6b77f9ac.PNG">

<br><br>

#### 3๏ธโฃ Retrofit Interface ์ค๊ณ

๋ช์ธ์ ๊ฐ์ ์ญํ 

##### Retrofit Interface๋?

=> ***์๋ฒ์ ์ด๋ ํ ์์ฒญ์ ๋ณด๋ด๋ฉด ์ด๋ป๊ฒ ์จ๋ค*๋ ์ผ์ข์ ์ํธ์์ฉ ๋ฐฉ๋ฒ์ ์ ์**ํ๋ ๋ถ๋ถ 

=> ์๊น ๋ดค๋ http ๋ฉ์๋, UIR, ํค๋ ๋ฑ๋ฑ์ ์ ์ํ๋ ๋ถ๋ถ

<br>

##### Retrofit Interface ์ค๊ณ

<img src="https://user-images.githubusercontent.com/31370590/140914448-d9abfcba-67f1-477f-8d16-6f0f9673a2c4.PNG">

+ ์ฝํ๋ฆฐ ํ์ผ์ ํ๋ ๋ง๋ค๊ณ , ํด๋์ค ํ์์ interface, interface๋ ์์ ๋ฐ๊ณ , ๊ตฌํํด์ค์ผ ํ๋ค. interface type์ ์ฐ๋ ์ด์ ๋ retrofit์์ Service ๊ฐ์ฒด๋ฅผ ๋ง๋ค์ด ์ค ๋ interface ํ์ผ์ ๋ฃ์ด์ ๋ง๋ค๋๋ก method๊ฐ ์ค๊ณ๋์ด์๋ค. 

+ ํด๋ผ์ด์ธํธ์ ์๋ฒ์์ ํต์  ๊ณผ์ ์ด ์ฐ๋ฆฌ ์ผ๋ฐ ์ธ์์์์ service์ ๋น์ทํ๊ธฐ ๋๋ฌธ์ `~service` ๋ผ๊ณ  ์ด๋ฆ์ ์ง๋ ๊ฒ์ด๋ค. 

+ POST method๋ฅผ ์ฌ์ฉํ  ๊ฒ์ด๋ฏ๋ก `@POST`๋ฅผ ์จ์ฃผ๊ณ , `@POST( )`์์ ์ ํํ ์ด๋ค URI์์ ์ด๋ฅผ ์ํํ๋์ง ์ ์ด์ค๋ค. 

+ ํจ์ ์์๋ ์ด http ๋ฉ์๋๋ฅผ ์คํ์์ผฐ์ ๋ ์ ๋ฌํ  RequestBody ๋ฐ์ดํฐ์ ์ ๋ฌ๋ฐ์ Response data๊ฐ์ ๋ฃ์ด์ค๋ค. Body๊ฐ ๋ฃ์ ๋๋ `@Body`๋ผ๊ณ  annotation์ ๋ช์ํด์ค์ผํ๋ค. 

+ POST, PUT์ Body๊ฐ ๊ฐ๋ฅ

  GET, DELETE๋ Body๊ฐ X  

+ Response์ ํด๋นํ๋ ๊ฐ์ฒด๊ฐ JSON Object์ผ ๋, `Call<ResponseLoginData>`

  Response์ ํด๋นํ๋ ๊ฐ์ฒด๊ฐ JSON Arrayํ์์ผ ๋ `Call<List<ResponseLoginData>>`

  ์ด๋ ๊ฒ ํด์ค์ผ ํ๋ค. 

<br><br>

#### 4๏ธโฃ Retrofit Interface ์ค์  ๊ตฌํ์ฒด(๊ฐ์ฒด) ๋ง๋ค๊ธฐ

 Retrofit Interface ์ค์  ๊ตฌํ์ฒด๋? => Retrofit ๊ฐ์ฒด๋ค ๊ทธ๋ฅ

<img src="https://user-images.githubusercontent.com/31370590/140919363-312e2582-d8c1-40a8-821a-f3329fc38653.PNG">

+ ์ Object ํ์์ธ๊ฐ ?

  ์๋ฒ ํธ์ถ์ด ํ์ํ  ๋๋ง๋ค Retrofit ๊ฐ์ฒด๋ฅผ ๋ง๋ค์ด์ผ ํ๋ค๋ฉด ๋๋ฌด ๋นํจ์จ์ ์ด๊ธฐ ๋๋ฌธ์ Retrofit ๊ฐ์ฒด์ ๊ฒฝ์ฐ **์ฑ๊ธํค(Object)**์ผ๋ก ์ ์ํ๋ ๊ฒ์ด ๋ฐ๋์งํ๋ค !

  > ์ฑ๊ธํค์ด๋?
  >
  > ์ต์ด ํ๋ฒ ์์ฑ์ด ๋์์ ๋ ๋ฉ๋ชจ๋ฆฌ์ ๊ณ์ ์์ฃผํ๋๋ก ํ๊ณ  ๊ทธ ์ดํ๋ก๋ ์ญ์ ๊ฐ ๋์ง ์๊ณ  ์ ๊ทผํ  ์ ์๋๋ก ์ต์ด ํ๋ฒ๋ง ๋ฉ๋ชจ๋ฆฌ๋ฅผ ํ ๋นํ๊ณ (Static) ๊ทธ ๋ฉ๋ชจ๋ฆฌ์ ์ธ์คํด์ค๋ฅผ ๋ง๋ค์ด ์ฌ์ฉํ๋ ๋์์ธํจํด
  >
  > ์ฝ๊ฒ ๋งํ์๋ฉด ์ฑ ํตํ์ด์ ํ๋๋ง ์์ฑ๋๋ ๊ฐ์ฒด ! kotlin์ ๊ฒฝ์ฐ object ํค์๋๋ฅผ ์ด์ฉํด ์ด๋ฌํ ์ฑ๊ธํค ๊ฐ์ฒด๋ฅผ ๋ง๋ค๊ธฐ ์ฝ๋ค

<br><br>

#### 5๏ธโฃ Callback ๋ฑ๋กํ์ฌ ํต์  ์์ฒญ

์ด๋ ๊ฒ ์๋ฒ ํต์ ์ ํ  ์ ์๋ Retrofit ๊ฐ์ฒด๊ฐ ์์ฑ์ด ๋๋๋ฐ ์ด๋ฅผ ๊ฐ์ง๊ณ  ๊ถ๊ทน์ ์ผ๋ก ํด์ผํ  ์ผ์ **data๋ฅผ ๋ฐ์์์ View์ ๋์์ฃผ๋ ์ผ**์ด๋ค. 

+ `Call<Type>` : ์๋ฒ์ ์ด `Type` ์ฃผ์ธ์ ! ํ๋ ๊ฒ

  => ๋๊ธฐ์  ๋๋ ๋น๋๊ธฐ์ ์ผ๋ก `Type`์ ๋ฐ์์ค๋ ๊ฐ์ฒด

+ `Callback<Type>` : Type ๊ฐ์ฒด๋ฅผ ๋ฐ์์์ ๋ ํ๋ก๊ทธ๋๋จธ์ ํ๋

  => Call ๊ฐ์ฒด๋ฅผ ํตํด ๋ฐํ์ ๋ฐ๊ณ  ๋๋ฉด ๊ทธ ์ดํ์ ์ด๋ค ํ๋์ ์คํ์ ์ํค๊ฒ ํ ์ง ์ ์ํ๋ ๋ถ๋ถ์ผ๋ก ์ฌ์ฉ์ ์ ์๊ฐ ๊ฐ๋ฅํจ

<br>

##### ๐ `LoginActivity.kt` ์ ์ฒด์ฝ๋ 

```kotlin
private fun initNetwork(){ // ๋คํธ์ํฌ๋ฅผ ์ด๊ธฐํํ๋ ํจ์
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

                Toast.makeText(this@MainActivity, "${data?.email}๋ ๋ฐ๊ฐ์ต๋๋ค!", Toast.LENGTH_SHORT).show()
                startActivity(Intent(this@MainActivity, SecondActivity::class,java))
            } else
                Toast.makeText(this@MainActivity, "๋ก๊ทธ์ธ์ ์คํจํ์์ต๋๋ค", Toast.LENGTH_SHORT).show()
        }

        override fun onFailure(call: Call<ResponseLoginData>, t: Throwable){
            Log.e("NetworkTest", "error:$t")
        }
    }
}
```

<br>

##### ๐ ์ ์ฒด์ฝ๋ ํ๋ํ๋์ฉ ์์ธํ ๋ณด์

```kotlin
val requestLoginData = RequestLoginData(
    email = binding.etId.text.toString(),
    password = binding.etPass.test.toString()
    )
```

+ ์ฐ์ , ํต์ ํ  ๋ ํ์ํ request ๋ฐ์ดํฐ๋ฅผ ๋ณดํต ๋ก๊ทธ์ธํ  ๋ `editText`๋ก id๋ password๋ก ์๋ ฅ๋ฐ์ผ๋ฏ๋ก **editText์ ๊ฐ์ ์ ๊ทผํด์ ์ด๋ฅผ RequestLoginData ํด๋์ค์ ์์ฑ์์ ๋งค๊ฐ๋ณ์์ ์ธ์๋ก ์ ๋ฌํด์ ๊ฐ์ฒด๋ฅผ ์์ฑ**ํจ. 

<br>

```kotlin
val call: Call<ResponseLoginData> = ServiceCreator.sampleService.postLogin(requestLoginData)
```

+ ์๊น ์๋น์ค๋ฅผ ๋ง๋ค์ด์ฃผ๋ ๊ตฌํ์ฒด๋ฅผ ๋ง๋ค๊ณ , ๊ฑฐ๊ธฐ์ ์๋น์ค ๊ฐ์ฒด๋ฅผ ๊ตฌ์ฒดํ์์ผ์คฌ๋๋ฐ ๊ทธ ์๋น์ค ๊ฐ์ฒด์์๋ `postLogin()`์ด๋ผ๋ ํจ์๋ฅผ ๋ช์ธํด์ฃผ์์. 
  ์ด์  ๊ทธ ํจ์๋ฅผ ํธ์ถํ๊ธฐ ์ํด `ServiceCreator`์์ `sampleService`์์ `postLogin()`๋ฅผ ํธ์ถํ๋๋ฐ ์ฌ๊ธฐ์ body ๊ฐ์ผ๋ก ์๊น ์์์ ์์ฑํด์ค `requestLoginData` ๋ผ๋ data class ๊ฐ์ฒด๋ฅผ ๋ฃ์ด์ค.

+ ์๊น ๊ตฌํํด์ค `postLogin()` ํจ์์ ์ง๊ธ `call` ๋ณ์์ ๋ฐํ ํ์์ด `Call<ResponseLoginData>`์ด๋ค. ์ ํต์ ํ๊ณ  ๋๋ฉด `Call<ResponseLoginData>`๊ฐ ๋ฐํ์ด ๋ ํ๋ฐ,  call์ด๋ผ๋ ๋ณ์๋ฅผ ๋ง๋ค์ด์ ์ด์์ ๋ฐํ๋ data๋ฅผ ๋ฃ์ด์ค๋ค. 

<br>

```kotlin
call.enqueue(object : Callback<ResponseLoginData> {
```

+ ์ด์  `call`์ด๋ผ๋ ๋ณ์๋ฅผ ์คํ์์ผ์ค ๋ค์, ์ฝ๋ฐฑ ๋ฉ์๋๋ก UI์ ๋์์ฃผ๋ ์์์ ํด์ค์ผ ํจ. ์๋ฒ ํต์  ๊ฐ์ ๊ฒฝ์ฐ๋ ๋น๋๊ธฐ ์ฒ๋ฆฌ๋ก ํด์ค์ผ ํจ. ๊ทธ๋์ call์ ์คํ์์ผ์ค ๋ `enqueue()`๋ผ๋ ํจ์๋ฅผ ํธ์ถํด์ฃผ๋๋ฐ ์ด๋ ๋น๋๊ธฐ ์ฒ๋ฆฌ๋ก ์์ํด์ค.(`execute()`๋ ๋๊ธฐ์ฒ๋ฆฌ) 

+ `enqueue`๋ก `call`๊ฐ์ฒด๋ฅผ ์คํ์์ผ์ค ๋ค์ `call`๊ฐ์ฒด๊ฐ ์คํ๋๊ณ  ๋ ํ ๋ฐ์์ค๋ `callback`์ผ๋ก ์ด๋ค ์์์ ํด์ค์ง ์ ์ธํด์ค๋ค. 

  => ์ฆ, `enqueque()`์์ ์๋ ๋ถ๋ถ๋ค์ด ์ฝ๋ฐฑ์ ๋ํ ๋ด์ฉ๋ค   

+ `Callback`์ ๋ฐ์์ค๊ฒ ๋๋ฉด ๋ฌด์กฐ๊ฑด override ํด์ค์ผ ํ๋ ํจ์ 2๊ฐ์ง

  + `onResponse()` : ์๋ฒ ํต์ ์ด ์ผ๋จ ์ด๋ฃจ์ด์ก๋ค๋ฉด

    => ๋ฉ์์ง์ ๋ฐ๋ผ ์ด๋ค ํ๋์ ํด์ค์ผ ํ ์ง

  + `onFailure()` : ์๋ฒ ํต์ ์ด ์ ์๋์์ ๋

    => ์๋ฌ ์ฒ๋ฆฌ๋ฅผ ํด์ฃผ๋ ์ฝ๋๋ฅผ ์์ฑํด์ค์ผํจ

<br>

```kotlin
 override fun onResponse(
            call: Call<ResponseLoginData>,
            response: Response<ResponseLoginData>
        ) {
            if(response.isSuccessful){
                val data = response.bodyy()?.data

                Toast.makeText(this@MainActivity, "${data?.email}๋ ๋ฐ๊ฐ์ต๋๋ค!", Toast.LENGTH_SHORT).show()
                startActivity(Intent(this@MainActivity, SecondActivity::class,java))
            } else
                Toast.makeText(this@MainActivity, "๋ก๊ทธ์ธ์ ์คํจํ์์ต๋๋ค", Toast.LENGTH_SHORT).show()
        }
```

+ ์๋ฒ ํต์ ์ด ์ด๋ฃจ์ด์ก๋ค๋ฉด ๋ฐ์ ๋ฉ์์ง์ ๋ฐ๋ผ ์ด๋ค ํ๋์ ํด์ค์ผ ํ ์ง  
+ ์๋ต๋ฐ์์จ ์น๊ตฌ์ ๊ฐ๋ค ์ค์๋ status ์ฝ๋๋ ์๊ฒ ์ง๋ง, ์ด ์๋ฒ ํต์ ์ ์ฑ๊ณต์ฌ๋ถ๋ฅผ ๋ํ๋ด์ฃผ๋ `isSuccessful`์ด๋ผ๋ Boolean type ๋ณ์๊ฐ ์๋ค. ์ด๋ฅผ ํตํด ์ฑ๊ณตํ์ ์ response body ์์ ์๋ data๋ฅผ ์ด์ฉํด ์ฒ๋ฆฌ ~ ์์ ~, else ์์๋ ์๋ต์ด ์ค๊ธด ์๋๋ฐ, ๋ถ์ ์ ์ธ ์๋ต์ด ์์ ๋์ ๋ํ ์์ ~

<br>

> ์ฐธ๊ณ 
>
> + SOPT 29๊ธฐ ์๋๋ก์ด๋ ํํธ ์ธ๋ฏธ๋

-----





















----

### ๐ Generic Class์ ๋ํด ํ์ฅํจ์๋ฅผ ์ถ๊ฐ => ์๋ฒ ์ฝ๋ ์ฌ์ฌ์ฉ

์๋ ์๋ฒ ํต์  ์ฝ๋

```kotlin
val call: Call<ResponseLoginData> =  ServiceCreator.sampleService.postLogin(requestLoginData)

call.enqueue(object : Callback<ResponseLoginData> {
        override fun onResponse(call: Call<ResponseLoginData>, response: Response<ResponseLoginData>) {
            if(response.isSuccessful){
                val data = response.body()?.data
                Toast.makeText(this@MainActivity, "${data?.email}๋ ๋ฐ๊ฐ์ต๋๋ค!", Toast.LENGTH_SHORT).show()
                startActivity(Intent(this@MainActivity, SecondActivity::class,java))
            } else
                Toast.makeText(this@MainActivity, "๋ก๊ทธ์ธ์ ์คํจํ์์ต๋๋ค", Toast.LENGTH_SHORT).show()
        }

        override fun onFailure(call: Call<ResponseLoginData>, t: Throwable){
            Log.e("NetworkTest", "error:$t")
        }
}
```



Generic Class์ ๋ํด ํ์ฅํจ์ ์ถ๊ฐ

=> `ResponseType`์ด๋ผ๋ ํ์์ ๋ํ Call ํด๋์ค์ ๋ํด ํ์ฅํจ์๋ฅผ ์ถ๊ฐ

=> `Call< >`์์ ์ด๋ค ๊ฐ์ฒด ํ์์ด ๋ด๊ฒจ๋, `enqueueUtil` ํจ์๋ฅผ ์ฌ์ฉํ  ์ ์๋๋ก ์ด๋ฅผ ํ์ฅํจ์๋ก ๋ง๋ค์ด ๋๋ ๊ฒ

=> **fun <E> ํด๋์ค์ด๋ฆ<E>.ํจ์์ด๋ฆ(์ธ์ํ์): ๋ฆฌํดํ์ {๊ตฌํ๋ถ}** ๋ก ์ ์๊ฐ๋ฅ

<img src="https://user-images.githubusercontent.com/31370590/159102693-3e06c633-9a61-4a26-b00d-68ea759147d9.PNG">

ํ์ฅํจ์๋ฅผ ์ด์ฉํ ์ฝ๋

```kotlin
call.enqueueUtil ( 
	onSuccess = { data ->  // ์ฌ๊ธฐ์ data๋ onResonse์ response.body ์ด๋ฏ๋ก data์ ์ ๊ทผํ๋ ค๋ฉด data.data~ ๋ก ์ ๊ทผํด์ผํ๋ค. 
                shortToast("${data.data.name}๋ ๋ฐ๊ฐ์ต๋๋ค")
                }
)
```



