# π₯ Unit 2 : Layouts

## Pathway 2 : Get user input in an app Part 2

## π Track 1 : change the app theme

### λμμΈ λ° μμ

+ λ¨Έν°λ¦¬μΌ λμμΈμ λ¬Όμ²΄κ° λΉμ λ°μ¬νκ³  κ·Έλ¦Όμλ₯Ό λλ¦¬μ°λ λ°©μμ ν¬ν¨νμ¬ μ€μ  μΈκ³μ μ§κ°μμ μκ°μ λ°μμ΅λλ€. μ½κΈ° μ½κ³  λ§€λ ₯μ μ΄λ©° μΌκ΄λ λ°©μμΌλ‘ μ± UIλ₯Ό λΉλνλ λ°©λ²μ κ΄ν κ°μ΄λλΌμΈμ μ μν©λλ€

<img src = "https://user-images.githubusercontent.com/31370590/125562774-35b060d6-1025-4ee6-9c51-d8093ab0525f.PNG" width = "400" height = "200">

+ **μμ**μ μμ λΉ¨κ°μ, λΉμ, νλμ(RGB) κ΅¬μ±μμλ₯Ό λνλ΄λ 3κ°μ 16μ§μ μ«μ(#00~#FF(0~255))λ‘ ννν  μ μμ΅λλ€. μ«μκ° ν΄μλ‘ κ΅¬μ±μμμ μμ΄ λ λ§μ΄ ν¬ν¨λ©λλ€. λν, μμμ ν¬λͺλλ₯Ό λνλ΄λ μν κ°(#00~#FF)μ ν¬ν¨νμ¬ μ μν  μ μμ΅λλ€(#00=0%=μμ  ν¬λͺ, #FF=100%=μμ  λΆν¬λͺ)



### νλ§

+ **νλ§**λ κ°λ³ `View`λΏ μλλΌ μ±, νλ λλ λ·° κ³μΈ΅ κ΅¬μ‘° μ μ²΄μ μ μ©λλ μ€νμΌμ λͺ¨μμλλ€. μ±, νλ, λ·° λλ λ·° κ·Έλ£Ήμ νλ§λ₯Ό μ μ©νλ©΄ μμμ νμ μμ μ μ²΄μ λμΌν νλ§κ° μ μ©λ©λλ€. λν, νλ§λ₯Ό μ¬μ©νμ¬ λ·°κ° μλ μμ(μν νμμ€ λ° μ°½ λ°°κ²½)μλ μ€νμΌμ μ μ©ν  μ μμ΅λλ€.



## π Track 2 : change the app icon

### λ°μ² μμ΄μ½

+ λͺ©νλ **κΈ°κΈ° λͺ¨λΈμ΄λ νλ©΄ λ°λμ μκ΄μμ΄ λ°μ² μμ΄μ½μ λͺ¨μμ λ©μ§κ²(μ λͺνκ³  λͺν)** λ§λλ κ²μλλ€. νΉν **νλ©΄ ν½μ λ°λ**λ **νλ©΄μ μΈμΉλΉ ν½μ μ**(λλ dpi, μΈμΉλΉ λνΈ μ)λ₯Ό λνλλλ€. μ€λ°λ κΈ°κΈ°(mdpi)μ κ²½μ° νλ©΄μ μΈμΉλΉ λνΈ μκ° 160μ΄μ§λ§ μ΄μ΄μ΄κ³ λ°λ κΈ°κΈ°(xxxhdpi)λ νλ©΄μ μΈμΉλΉ λνΈ μκ° 640μλλ€.

+ μμ€ λλ ν°λ¦¬(**app > src > main > res**)μ `mipmap` ν΄λ : Andriod μ±μ λ°μ² μμ΄μ½ μμμ λ°°μΉν΄μΌ νλ μμΉμ΄λ€. 

  ex) mimmap-hdpi

  

+ Androidμ λ°λ νμ μ(density qualifier)

  + `mdpi` - μ€λ°λ νλ©΄μ λ¦¬μμ€(~160dpi)
  + `hdpi` - κ³ λ°λ νλ©΄μ λ¦¬μμ€ (~240dpi)
  + `xhdpi` - μ΄κ³ λ°λ νλ©΄μ λ¦¬μμ€(~320dpi)
  + `xxhdpi` - μ΄μ΄κ³ λ°λ νλ©΄μ λ¦¬μμ€(~480dpi)
  + `xxxhdpi` - μ΄μ΄μ΄κ³ λ°λ νλ©΄μ λ¦¬μμ€(~640dpi)
  + `nodpi` - νλ©΄μ ν½μ λ°λμ κ΄κ³μμ΄ μ‘°μ ν  μ μλ λ¦¬μμ€
  + `anydpi` - μ΄λ€ λ°λλ‘λ μ‘°μ  κ°λ₯ν λ¦¬μμ€



### μ μν μμ΄μ½(adaptive icon)

+ μ΄λ **μ΄λ€ κΈ°κΈ°λ λ°λμμλ  νμΌνλ μμ΄μ½ μ€νμΌμ κ°μ§ μ μλλ‘** ν΄μ£Όλ μμ΄μ½ μ€νμΌμ΄λ€. κ°λ¨νκ² λ§νμλ©΄ λ§μ€νΉ μ²λ¦¬ν΄μ μμ΄μ½μ λ³΄μ¬μ£Όλ ννμλλ€. λ°°κ²½ λ μ΄μ΄(Background-Layer)μ ν¬κ·ΈλΌμ΄λ λ μ΄μ΄(Foreground-Layer)λ₯Ό ν©ν λ μ΄μ΄λ₯Ό λ§μ€ν¬ λ μ΄μ΄(Mask-Layer)λ₯Ό μ μ©ν΄μ λ³΄μ¬μ£Όλ λ°©μμΌλ‘ κ΅¬νλμ΄ μμ΅λλ€. 

+ Foreground and bachground layer

  κ°λ°μλ μ± μμ΄μ½μ λ λ μ΄μ΄, μ¦ **ν¬κ·ΈλΌμ΄λ λ μ΄μ΄**μ **λ°±κ·ΈλΌμ΄λ λ μ΄μ΄**λ‘ κ΅¬μ±ν  μ μμ΅λλ€. μ μμμ ν°μ Android μμ΄μ½μ ν¬κ·ΈλΌμ΄λ λ μ΄μ΄μ μμ§λ§ νλμκ³Ό ν°μ κ·Έλ¦¬λλ λ°±κ·ΈλΌμ΄λ λ μ΄μ΄μ μμ΅λλ€. ν¬κ·ΈλΌμ΄λ λ μ΄μ΄λ λ°±κ·ΈλΌμ΄λ λ μ΄μ΄ μμ μμλλ€. κ·Έλ° λ€μ λ§μ€ν¬(μ΄ κ²½μ°μλ μν λ§μ€ν¬)κ° λ§¨ μμ μ μ©λμ΄ μν λͺ¨μμ μ± μμ΄μ½μ΄ μμ±λ©λλ€.

+ **vector drawble**(res->drawable->ic_launcher_background)κ³Ό **bitmap image**(res->mipmap-~dpi->ic_launcher)λ λͺ¨λ κ·Έλν½μ μ€λͺνμ§λ§ μ€μν μ°¨μ΄μ μ΄ μμ΅λλ€.

  **λΉνΈλ§΅ μ΄λ―Έμ§**λ κ° ν½μμ μμ μ λ³΄λ₯Ό μ μΈνκ³  λ³΄μ ν μ΄λ―Έμ§μ κ΄ν΄ μ μμ§ λͺ»ν©λλ€. λ°λ©΄μ λ²‘ν° κ·Έλν½μ μ΄λ―Έμ§λ₯Ό μ μνλ λͺ¨μμ κ·Έλ¦¬λ λ°©λ²μ μκ³  μμ΅λλ€. μ΄λ¬ν μ§μΉ¨μ μμ μ λ³΄μ ν¨κ» μΌλ ¨μ μ κ³Ό μ , κ³‘μ μΌλ‘ κ΅¬μ±λ©λλ€. λ²‘ν° κ·Έλν½μ **νμ§ μ ν μμ΄ λͺ¨λ  νλ©΄ λ°λμ μ΄λ€ μΊλ²μ€ ν¬κΈ°λ‘λ μ‘°μ ν  μ μλ€**λ κ²μ΄ μ₯μ μλλ€.

  **λ²‘ν° λλ‘μ΄λΈ**μ Androidμ λ²‘ν° κ·Έλν½ κ΅¬νμΌλ‘, ν΄λκΈ°κΈ°μμ μΆ©λΆν μ μ°νλλ‘ λ§λ€μ΄μ‘μ΅λλ€. μ΄λ¬ν κ°λ₯ν μμλ₯Ό μ¬μ©νμ¬ **XMLλ‘ μ μ**ν  μ μμ΅λλ€. λͺ¨λ  λ°λ λ²ν·μ λΉνΈλ§΅ μ μ λ²μ μ μ κ³΅νλ λμ  μ΄λ―Έμ§λ₯Ό ν λ²λ§ μ μνλ©΄ λ©λλ€. λ°λΌμ μ±μ ν¬κΈ°κ° μ€μ΄ μ μ§νκΈ°κ° μ¬μμ§λλ€.
  
+ μ΄λν°λΈ μμ΄μ½μ μ¬μ©νλ λ°±κ·ΈλΌμ΄λ λ μ΄μ΄μ ν¬κ·ΈλΌμ΄λ λ μ΄μ΄λ λͺ¨λ **108x108dp**λ‘ μ€μ ν΄μΌνλ©°, λ§μ€νΉ λλ νλ©΄ μμ­μ μ΅λ **72x72dp**, μ΅μ **66x66dp**λ‘ μ€μ ν©λλ€ 

+ μ΄μ  μ μν μμ΄μ½μ΄ μ μλνλ―λ‘ λͺ¨λ  μ± μμ΄μ½ λΉνΈλ§΅ μ΄λ―Έμ§λ₯Ό μ κ±°ν  μ μλ μ΄μ κ° κΆκΈν  μ μμ΅λλ€. μ΄μ  λ²μ μ Androidμμ μ± μμ΄μ½μ΄ κ³ νμ§λ‘ νμλκΈ° μν΄(μ΄μ  λ²μ κ³Όμ νΈνμ±μ΄λΌκ³  ν¨) μ΄λ¬ν νμΌμ΄ μ¬μ ν νμν©λλ€.



Q)

+ drawable->**ic_launcher_background.xml**κ³Ό  **drawable-v24->ic_launcher_foreground.xml** λͺ¨λ **vector drawble file**μλλ€. ν½μ λ¨μμ κ³ μ λ ν¬κΈ°λ μλ€. μ½λλ₯Ό λ³΄λ©΄ `<vector>`μμλ₯Ό μ¬μ©ν΄ λ²‘ν° λλ‘μ΄λΈμ XMLμ μΈμ νμΈν  μ μλ€. 

+ μ΄ λκ°μ λ²‘ν° λλ‘μ΄λΈ νμΌμ μ΄μ©ν΄ res > mipmap-anydpi-v26->**ic_launcher.xml** κ°μ **μ μν μμ΄μ½**μ λ§λλ κ²

+ res->mipmap-~dpi->ic_launcher.**png**λ λΉνΈλ§΅ μ΄λ―Έμ§ νμΌ(μ¬μ§ κ°μ κ²μ μΌλ ¨μ λͺ¨μμΌλ‘ μ€λͺνκΈ° μ΄λ ΅κΈ° λλ¬Έμ λ²‘ν° λλ‘μ΄λΈλ³΄λ€ λΉνΈλ© μμμ μ¬μ©νλ κ²μ΄ λ ν¨μ¨μ μ΄λ€.)

  > **μ°Έκ³ **: μ μν μμ΄μ½μ νλ«νΌμ API μμ€ 26μμ μΆκ°λμμΌλ―λ‘ `-v26` λ¦¬μμ€ νμ μκ° μλ `mipmap` λ¦¬μμ€ λλ ν°λ¦¬μμ μ μν μμ΄μ½μ μ μΈν΄μΌ ν©λλ€. μ¦, μ΄ λλ ν°λ¦¬μ λ¦¬μμ€λ API 26(Android 8.0) μ΄μμ μ€ννλ κΈ°κΈ°μλ§ μ μ©λ©λλ€. μ΄ λλ ν°λ¦¬μ λ¦¬μμ€ νμΌμ μ΄μ  λ²μ μ νλ«νΌμ μ€ννλ κΈ°κΈ°μμλ λ¬΄μλ©λλ€.



## π Track 3 : Create a more polished user experience

### material component

+ λ¨Έν°λ¦¬μΌ κ΅¬μ±μμλ μ±μμ λ¨Έν°λ¦¬μΌ μ€νμΌμ λ μ½κ² κ΅¬νν  μ μλ μΌλ°μ μΈ UI μμ ―μλλ€. λ¨Έν°λ¦¬μΌ κ΅¬μ±μμλ₯Ό μ¬μ©νλ©΄ μ±μ΄ μ¬μ©μ κΈ°κΈ°μ μλ λ€λ₯Έ μ±κ³Ό ν¨κ» λ μΌκ΄λ λ°©μμΌλ‘ μλν©λλ€. μ΄λ κ² νλ©΄ ν μ±μμ νμ΅λ UI ν¨ν΄μ΄ λ€μ μ±μ μ΄μ λ  μ μμ΅λλ€. λ°λΌμ μ¬μ©μλ μ±μ μ¬μ©νλ λ°©λ²μ ν¨μ¬ λ λΉ λ₯΄κ² λ°°μΈ μ μμ΅λλ€. κ°λ₯νλ©΄ ν­μ (λΉ λ¨Έν°λ¦¬μΌ μμ ―μ΄ μλ) λ¨Έν°λ¦¬μΌ κ΅¬μ±μμλ₯Ό μ¬μ©νλ κ²μ΄ μ’μ΅λλ€λν λ¨Έν°λ¦¬μΌ κ΅¬μ±μμλ μ μ°μ±κ³Ό λ§μΆ€μ€μ  κ°λ₯μ±μ΄ λ λμ΅λλ€

+ νμ¬ ν κ³μ°κΈ° μ±μ λ μ΄μμ μλ¨μλ μλΉμ€ λΉμ©μ μν `EditText` νλκ° μμ΅λλ€. μ΄ `EditText` νλλ μλνμ§λ§ νμ€νΈ νλμ λͺ¨μκ³Ό λμ λ°©μμ κ΄ν μ΅κ·Ό λ¨Έν°λ¦¬μΌ λμμΈ κ°μ΄λλΌμΈμ λ°λ₯΄μ§λ μμ΅λλ€. μλΉμ€ λΉμ© `EditText`λ₯Ό λ¨Έν°λ¦¬μΌ νμ€νΈ νλ(`TextInputLayout`μ `TextInputEditText`λ‘ κ΅¬μ±λ¨)λ‘ λ°κΏλλ€. 

  ```kotlin
  <com.google.android.material.textfield.TextInputLayout
    android:id="@+id/cost_of_service"
     android:layout_width="160dp"
     android:layout_height="wrap_content"
     android:hint="@string/cost_of_service"
     app:layout_constraintStart_toStartOf="parent"
     app:layout_constraintTop_toTopOf="parent">
  
    <com.google.android.material.textfield.TextInputEditText
         android:id="@+id/cost_of_service_edit_text"
         android:layout_width="match_parent"
         android:layout_height="wrap_content"
         android:inputType="numberDecimal" />
      />
  
  </com.google.android.material.textfield.TextInputLayout>
  ```

+  `TextInputEditText` μμμμ λ¦¬μμ€ IDκ° `cost_of_service_edit_text`μΈ μ¬μ©μ μλ ₯μ κ°μ Έμ΅λλ€. `MainActivity`μμ `binding.costOfServiceEditText`λ₯Ό μ¬μ©νμ¬ μ μ₯λ νμ€νΈ λ¬Έμμ΄μ μ‘μΈμ€ν©λλ€. 

  ```kotlin
  private fun calculateTip() {
      // Get the decimal value from the cost of service text field
      val stringInTextField = binding.costOfServiceEditText.text.toString()
      val cost = stringInTextField.toDoubleOrNull()
  
      ...
  }

+ Android νλ«νΌμ `Switch` λμ  MDC λΌμ΄λΈλ¬λ¦¬μ `SwitchMaterial`μ μ¬μ©ν  λ μ΄μ μ λΌμ΄λΈλ¬λ¦¬μ `SwitchMaterial` κ΅¬νμ΄ μλ°μ΄νΈλλ©΄(μ: λ¨Έν°λ¦¬μΌ λμμΈ κ°μ΄λλΌμΈ λ³κ²½) μ§μ  λ³κ²½νμ§ μκ³ λ λ¬΄λ£λ‘ μμ ―μ΄ μλ°μ΄νΈλλ€λ μ μλλ€. λλΆμ λ―Έλμ λλΉν μ±μ λ§λ ¨ν  μ μμ΅λλ€.





### μμ΄μ½

+ μ±μ μμ΄μ½μ κ²½μ° λ€μν νλ©΄ λ°λμ λ§λ μ¬λ¬ λ²μ μ λΉνΈλ§΅ μ΄λ―Έμ§λ₯Ό μ κ³΅νλ λμ  **λ²‘ν° λλ‘μ΄λΈ**μ μ¬μ©νλ κ²μ΄ μ’μ΅λλ€. λ²‘ν° λλ‘μ΄λΈμ μ΄λ―Έμ§λ₯Ό κ΅¬μ±νλ μ€μ  ν½μμ μ μ₯νλ λμ  ***μ΄λ―Έμ§λ₯Ό λ§λλ λ°©λ²μ κ΄ν μ§μΉ¨μ μ μ₯νλ XML νμΌ***λ‘ ννλ©λλ€. λ²‘ν° λλ‘μ΄λΈμ μκ°μ  νμ§ μμ€μ΄λ νμΌ ν¬κΈ° μ¦κ° μμ΄ νμ₯νκ±°λ μΆμν  μ μμ΅λλ€. 



+ μ΄μ  μλλ‘μ΄λ λ²μ  μ§μνκΈ°

  μ±μ λ²‘ν° λλ‘μ΄λΈμ μΆκ°νμ§λ§, Android νλ«νΌμ λ²‘ν° λλ‘μ΄λΈ μ§μμ Android 5.0(API μμ€ 21) μ μλ μΆκ°λμ§ μμμ΅λλ€. μ±μ΄ μ΄λ¬ν μ΄μ  λ²μ μ Androidμμ μλ(μ΄μ  λ²μ κ³Όμ νΈνμ±)νκ² νλ €λ©΄ `vectorDrawables` μμλ₯Ό μ±μ `build.gradle` νμΌμ μΆκ°νμΈμ. κ·Έλ¬λ©΄ API 21 λ―Έλ§μ νλ«νΌ λ²μ μμ λ²‘ν° λλ‘μ΄λΈμ μ¬μ©ν  μ μμ΅λλ€. 

  `app/build.gradle`

  ```kotlin
  android {
    defaultConfig {
      ...
      vectorDrawables.useSupportLibrary = true
     }
     ...
  }



### μμ΄μ½ μΆκ°νκΈ°

1. vector drawble asset μΆκ°νκΈ°
   + **Resource Manager** > + > **Vector Asset**
   + **Clip Art:** μμ μλ λ²νΌμ ν΄λ¦­νμ¬ λ€λ₯Έ ν΄λ¦½ μνΈ μ΄λ―Έμ§λ₯Ό μ νν©λλ€. λ©μμ§κ° νμλλ©΄ λνλλ μ°½μ 'call made'λ₯Ό μλ ₯ν©λλ€. μ΄ νμ΄ν μμ΄μ½μ Round up tip μ΅μμ μ¬μ©νκ² μ΅λλ€. μμ΄μ½μ μ ννκ³  **OK**λ₯Ό ν΄λ¦­ν©λλ€. 
   + μμ΄μ½ μ΄λ¦ μ€μ  ex) ic_~



2. imageViewλ₯Ό μ¬μ©νμ¬ μ±μ μμ΄μ½ νμ

   + ```kotlin
     <ImageView
         android:id="@+id/icon_cost_of_service"
         android:layout_width="wrap_content"
         android:layout_height="wrap_content"
         android:importantForAccessibility="no"
         app:srcCompat="@drawable/ic_store" />
     ```

     `app:srcCompat` μμ±μ λλ‘μ΄λΈ λ¦¬μμ€ `@drawable/ic_store`λ‘ μ€μ νλ©΄ μ΄ XML μ€ μμ μμ΄μ½μ λ―Έλ¦¬λ³΄κΈ°κ° νμλ©λλ€. μ΄ μ΄λ―Έμ§λ μ₯μμ©μΌλ‘λ§ μ¬μ©λλ―λ‘ `android:importantForAccessibility="no"`λ μ€μ ν©λλ€.





### μ€νμΌ λ° νλ§

+ μ€νμΌμ λ¨μΌ μμ ― μ νμ λ·° μμ± κ° λͺ¨μμλλ€. μλ₯Ό λ€μ΄ `TextView` μ€νμΌμ κΈκΌ΄ μμ, κΈκΌ΄ ν¬κΈ°, λ°°κ²½μ λ±μ μ§μ ν  μ μμ΅λλ€. μ΄λ¬ν μμ±μ μ€νμΌλ‘ μΆμΆνλ©΄ λ μ΄μμμ μ€νμΌμ μ¬λ¬ λ·°μ μ½κ² μ μ©νκ³  λ¨μΌ μμΉμ μ μ§ν  μ μμ΅λλ€.

+ μ€νμΌ λ§λ€κΈ°

  + **res > values** λλ ν°λ¦¬μ `styles.xml`μ΄λΌλ μ νμΌμ λ§λ­λλ€.

    ```kotlin
    <style name="Widget.TipTime.TextView" parent="Widget.MaterialComponents.TextView">
        <item name="android:minHeight">48dp</item>
        <item name="android:gravity">center_vertical</item>
        <item name="android:textAppearance">?attr/textAppearanceBody1</item>
    </style>
    ```

    

+ νλ§μ μ€νμΌ μΆκ°νκΈ°

  + μ `RadioButton` μ€νμΌκ³Ό `Switch` μ€νμΌμ κ° μμ ―μ μ μ©νμ§ μμμμ νμΈν  μ μμ΅λλ€. μ΄κ²μ μ± νλ§μμ νλ§ μμ±μ μ¬μ©νμ¬ `radioButtonStyle` λ° `switchStyle`μ μ€μ νκΈ° λλ¬Έμλλ€. 

  + νλ§λ λμ€μ μ€νμΌ, λ μ΄μμ λ±μ μ°Έμ‘°ν  μ μλ λͺλͺλ λ¦¬μμ€(νλ§ μμ±μ΄λΌκ³  ν¨)μ λͺ¨μμλλ€. κ°λ³ `View.`λΏλ§ μλλΌ μ μ²΄ μ±, νλ, λ·° κ³μΈ΅ κ΅¬μ‘°μλ νλ§λ₯Ό μ§μ ν  μ μμ΅λλ€. μ΄μ μ `themes.xml`μμ μ±κ³Ό κ΅¬μ±μμ μ μ²΄μ μΌλ‘ μ¬μ©λλ `colorPrimary`, `colorSecondary` κ°μ νλ§ μμ±μ μ€μ νμ¬ μ±μ νλ§λ₯Ό μμ νμ΅λλ€. 

  + `radioButtonStyle` λ° `switchStyle`μ μ€μ ν  μ μλ λ€λ₯Έ νλ§ μμ±μλλ€. μ΄ νλ§ μμ±μ μ κ³΅νλ μ€νμΌ λ¦¬μμ€λ νλ§κ° μ μ©λλ λ·° κ³μΈ΅ κ΅¬μ‘°μ λͺ¨λ  λΌλμ€ λ²νΌκ³Ό λͺ¨λ  μ€μμΉμ μ μ©λ©λλ€.

  + `res/values/themes.xml`

    ```kotlin
    <item name="textInputStyle">@style/Widget.MaterialComponents.TextInputLayout.OutlinedBox</item>
    <item name="radioButtonStyle">@style/Widget.TipTime.CompoundButton.RadioButton</item>
    <item name="switchStyle">@style/Widget.TipTime.CompoundButton.Switch</item>
    ```

    



### κΈ°κΈ° νμ νκΈ°

+ κΈ°κΈ°λ₯Ό νμ ν΄ κ°λ‘ λͺ¨λκ° λλ©΄, Calculate λ²νΌμ ν¬ν¨ν μΌλΆ UI κ΅¬μ±μμκ° μλ¦¬λ κ²μ νμΈν  μ μμ΅λλ€. μ΄λ‘ μΈν΄ μ±μ μ¬μ©νμ§ λͺ»ν©λλ€. μ΄ λ²κ·Έλ₯Ό ν΄κ²°νλ €λ©΄ `ConstraintLayout` μ£Όμμ `ScrollView`λ₯Ό μΆκ°ν©λλ€.

  ```kotlin
  <ScrollView
     xmlns:android="http://schemas.android.com/apk/res/android"
     xmlns:app="http://schemas.android.com/apk/res-auto"
     xmlns:tools="http://schemas.android.com/tools"
     android:layout_height="match_parent"
     android:layout_width="match_parent">
  
     <androidx.constraintlayout.widget.ConstraintLayout
         android:layout_width="match_parent"
         android:layout_height="wrap_content"
         android:padding="16dp"
         tools:context=".MainActivity">
  
         ...
     </ConstraintLayout>
  
  </ScrollView>
  ```

  

### Enter ν€λ₯Ό λλ₯΄λ©΄ ν€λ³΄λ μ¨κΈ°κΈ°

+ νμ€νΈ νλμ κ²½μ° νΉμ  ν€λ₯Ό ν­ν  λ μ΄λ²€νΈμ μλ΅νλλ‘ ν€ λ¦¬μ€λλ₯Ό μ μν  μ μμ΅λλ€. ν€λ³΄λμμ κ°λ₯ν λͺ¨λ  μλ ₯ μ΅μμλ `Enter` ν€λ₯Ό ν¬ν¨ν ν€μ ν€ μ½λκ° μ°κ²°λμ΄ μμ΅λλ€. ν°μΉ ν€λ³΄λλ μννΈ ν€λ³΄λλΌκ³ λ νλ©° μ€μ  ν€λ³΄λκ° μλλλ€.

  ```kotlin
   private fun handleKeyEvent(view: View, keyCode: Int): Boolean {
          if (keyCode == KeyEvent.KEYCODE_ENTER) {
              // Hide the keyboard
              val inputMethodManager =
                  getSystemService(Context.INPUT_METHOD_SERVICE) as InputMethodManager
              inputMethodManager.hideSoftInputFromWindow(view.windowToken, 0)
              return true
          }
          return false
      }
  
  ...
  
  override fun onCreate(savedInstanceState: Bundle?) {
       binding.calculateButton.setOnClickListener { calculateTip() }
       binding.costOfServiceEditText.setOnKeyListener { view, keyCode, _ -> handleKeyEvent(view, keyCode)
          }
  }
  ```

  



### π Quiz/Unit2/Pathway2

1. Which line(s) of XML code will produce an error?

   ```kotlin
   1    <TextView
   2        android:layout_width="wrap_content"
   3        android:layout_height"wrap_content"
   4        android:padding="8dp"
   5        android:text="@string/title"
   6        android:textSize=18sp />
   ```

   => 

   + Line 3 - Missing = symbol after `android:layout_height` attribute.
   + Line 6 - Missing quotations around the attribute value `18sp`.



2. Which of the following is true about Gradle?

   =>

   + Gradle is an automated build system used by Android Studio to build your apps.
   + Gradle handles installing your app on a device.
   + You can configure Android-specific options for your project in your appβs `build.gradle` file.



3. Which of the following statements about app icons are true?

   => 

   + mdpi, hdpi, xhdpi, xxhdpi, and xxxhdpi are density qualifiers for resource directories to indicate that these are resources to be used on devices with a specific screen density.
   + Adaptive icons are made up of a foreground and background layer, and an OEM mask will be applied on top of them.



4. Which of the below steps are part of changing the color of your app theme?

   =>

   + Modify the `themes.xml` (night) file.
   + Set the primary and secondary color theme attributes of your app theme
   + Define the colors used in your app as color resources in the `colors.xml` file.



5. Why use the Material Components for Android library?

   => 

   + It provides widgets that follow the Material Design guidelines such as text fields and switches.
   + It provides default Material themes that you can use directly or extend and then customize.
   + It helps you more quickly build beautiful user experiences.

