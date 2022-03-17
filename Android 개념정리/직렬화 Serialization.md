## 직렬화 Serialization

객체를 저장하거나 메모리, 데이터베이스 혹은 파일로 옮기려면 어떻게 해야할까? 이럴 때 필요한 것이 직렬화다. 직렬화란 **객체를 바이트 스트림으로 바꾸는 것**, 즉 객체에 저장된 데이터를 스트림에 write 하기 위해 연속적인(serial) 데이터로 변환하는 것이다.

> 바이트 스트림 : 0101110010101010101010....

직렬화의 주된 목적은 객체를 상태 **그대로 저장**하고 필요할 때 다시 생성하여 사용하는 것이다.

<img src = "https://user-images.githubusercontent.com/31370590/158721415-e2f0a3fd-9988-49cf-8a8b-f6ef381d4797.PNG">

역직렬화(Deserialization)는 직렬화의 반대말로, 네트워크나 영구저장소에서 바이트 스트림을 가져와서 객체가 저장되었던 바로 그 상태로 변환하는 것이다(convert it back to the Object **with the same state**).

직렬화하면서 생긴 바이트 스트림은 플랫폼에 독립적이다(platform independent). 직렬화된 객체는 다른 플랫폼에서 역직렬화가 가능하다는 뜻이다.

=> ❓ 파일에서 직렬화 한 객체를 memory에서도 역직렬화가 가능하다는 뜻인가 ?





#### Serializable

+ 모든 클래스를 직렬화할 수는 없다. **java.io.Serializable** 인터페이스를 구현한 클래스의 객체만 직렬화될 수 있다.

  ```kotlin
  data class FollowerDao(
      @SerializedName("login")
      val name : String,
      @SerializedName("bio")
      val introduction : String?= null
  ) : Serializable
  
  ```

+ Serializable 인터페이스는 어떤 멤버변수나 메서드도 가지고 있지 않은 마커 인터페이스 **marker interface**이다. 해당 인터페이스를 구현한 클래스가 특정 능력를 가진다고 표시해두기 위해 쓰인다는 뜻이다.
+ 단, 클래스에 비밀번호와 같이 **보안상 직렬화되면 안 되는 값**이나 직렬화가 될 수 없는 객체에 대한 참조가 포함된 경우 transient라는 제어자를 이용할 수 있다. **transient가 붙은 인스턴스 변수의 값은 그 타입의 기본값으로 직렬화된다.**



> 참고
>
> + [직렬화](https://medium.com/@lunay0ung/basics-%EC%A7%81%EB%A0%AC%ED%99%94-serialization-%EB%9E%80-feat-java-2f3eb11e9a8)