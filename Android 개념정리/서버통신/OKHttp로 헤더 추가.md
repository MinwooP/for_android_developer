## OKHttp 

+ 안드로이드(클라이언트)와 서버 간에 Retrofit2를 사용하여 통신을 하는데 

  안드로이드 클라이언트단 쪽에서 **인터셉터**를 추가로 사용하면 안드로이드에서 서버에게 데이터 전송 및 수신받을때 인터셉터 말 그대로 중간에 매개체가 되어 어떠한 처리를 해줄 수 있다. 

<br>

#### OKHttp 사용해서 자동으로 헤더 추가하기

```kotlin
object GithubServiceCreator {
    private val BASE_URL = "https://api.github.com"
    private val retrofit: Retrofit = Retrofit.Builder()
        .baseUrl(BASE_URL)
        .client(provideOkHttpClient(AppInterceptorGit()))
        .addConverterFactory(GsonConverterFactory.create())
        .build()

    val githubService: GithubService = retrofit.create(GithubService::class.java)
}


private fun provideOkHttpClient(
    interceptor: AppInterceptorGit
): OkHttpClient = OkHttpClient.Builder()
    .run {
        addInterceptor(interceptor)
        build()
    }

class AppInterceptorGit : Interceptor {
    @Throws(IOException::class)
    override fun intercept(chain: Interceptor.Chain)
            : okhttp3.Response = with(chain) {
        val newRequest = request().newBuilder()
            .addHeader("accept", "application/vnd.github.v3+json")
            .build()
        proceed(newRequest)
    }
}
```

<br><br>

> 참고
>
> + [코틀린 Retrofit2 OkHttP interceptor 헤더 사용법](https://youngest-programming.tistory.com/200)
> + [okHttp Header 인터셉터에 조건 추가하기](https://salix97.tistory.com/238)