# ScrollView







-----

## NestedScrollView

+ `NestedScrollView`는 사실 `ScrollView`이다.
  안드로이드 공식 문서에서도 "NestedScrollView is just like ScrollView" 라고 작성되어 있다.
  심지어 사용하는 방법도 `ScrollView`와 다를 것이 별로 없다.

<br>

#### ScrollView를 사용했을 때의 문제점

+ 아래는 `ScrollView`안에 `RecyclerView`를 사용했을 때, 스크롤이 되는 모습이다.

+ 이 경우에 `RecyclerView`만 스크롤 되다가 더 이상 `RecyclerView`에서 스크롤을 할 수 없을 때, `ScrollView`가 스크롤 되는 것을 알 수 있다.

  이처럼 `ScrollView`안에 `RecyclerView`를 사용하면 상당히 좋지 않은 성능을 보여주는데, 아마도 `ScrollView`와 `RecyclerView`의 스크롤 이벤트 처리에서 문제가 생겨서 이러한 문제가 발생하지 않을까 라는 생각이 든다. ~~(나중에 더 자세히 알아봐야지)~~

#### NestedScrollView를 사용하면 문제 해결!

+ `crollView`를 사용했을 때와 달리, 모든 `View`들이 함께 스크롤 되는 것을 확인할 수 있다.

<br>

#### NestedScrollView 사용법

```xml
<androidx.core.widget.NestedScrollView
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:fillViewport="true">

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="vertical">
      
      <!-- 이 부분에 RecyclerView를 비롯한 여러 View들을 배치하면 된다. -->
      <androidx.recyclerview.widget.RecyclerView
          android:id="@+id/recyclerView"
          android:layout_width="match_parent"
          android:layout_height="match_parent"
          android:layout_marginTop="10dp"
          android:nestedScrollingEnabled="false"
          android:overScrollMode="never"
          android:visibility="gone" />
      
    </LinearLayout>
</androidx.core.widget.NestedScrollView>
```

+ 여기서 한 가지 조심해야 하는 것은 `RecyclerView`의 `nestedScrollingEnabled` 값을 `false`로 설정해야 한다는 것이다. 참고로 위의 코드에서 `RecyclerView`의 `overScrollMode` 값을 `never`로 설정한 것은 `RecyclerView`의 스크롤 효과를 없애기 위해서이다.