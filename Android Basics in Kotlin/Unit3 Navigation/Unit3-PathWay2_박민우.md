# π₯ Unit 3 : Navigation

## Pathway 2: Introduction to the Navigation component

## π Fragments and the Navigation component

<br>

#### Fragment

+ κ°λ¨νκ² λ§ν΄ μ±μ μ¬μ©μ μΈν°νμ΄μ€μμ **μ¬μ¬μ© κ°λ₯ν λΆλΆ**μλλ€. νλκ³Ό λ§μ°¬κ°μ§λ‘ νλκ·Έλ¨ΌνΈλ μλͺ μ£ΌκΈ°κ° μκ³  μ¬μ©μ μλ ₯μ μλ΅ν  μ μμ΅λλ€. νλκ·Έλ¨ΌνΈλ νλμ΄ νλ©΄μ νμλ  λ νλμ λ·° κ³μΈ΅ κ΅¬μ‘° λ΄μ ν­μ ν¬ν¨λ©λλ€. μ¬μ¬μ©μ±κ³Ό λͺ¨λμ±μ κ°μ‘°νλ―λ‘ **λ¨μΌ νλμμ μ¬λ¬ νλκ·Έλ¨ΌνΈλ₯Ό λμμ νΈμ€ν**ν  μλ μμ΅λλ€. κ° νλκ·Έλ¨ΌνΈλ λ³λμ μμ²΄ μλͺ μ£ΌκΈ°λ₯Ό κ΄λ¦¬ν©λλ€.

<br>

#### Fragment Lifecycle

+  *Lifecycle.State* μ΄κ±°νμΌλ‘ ννλλ λ€μ― κ°μ§ μν
  + INITIALIZED: νλκ·Έλ¨ΌνΈμ μ μΈμ€ν΄μ€κ° μΈμ€ν΄μ€νλμμ΅λλ€.
  + CREATED: μ²« λ²μ§Έ νλκ·Έλ¨ΌνΈ μλͺ μ£ΌκΈ° λ©μλκ° νΈμΆλ©λλ€. μ΄ μνμμ νλκ·Έλ¨ΌνΈμ μ°κ²°λ λ·°λ λ§λ€μ΄μ§λλ€.
  + STARTED: νλκ·Έλ¨ΌνΈκ° νλ©΄μ νμλμ§λ§ 'ν¬μ»€μ€'κ° μμΌλ―λ‘ μ¬μ©μ μλ ₯μ μλ΅ν  μ μμ΅λλ€.
  + RESUMED: νλκ·Έλ¨ΌνΈκ° νμλκ³  ν¬μ»€μ€κ° μμ΅λλ€.
  + DESTROYED: νλκ·Έλ¨ΌνΈ κ°μ²΄μ μΈμ€ν΄μ€νκ° μ·¨μλμμ΅λλ€.

<br>

+ `Fragment` ν΄λμ€λ μλͺ μ£ΌκΈ° μ΄λ²€νΈμ μλ΅νκΈ° μν΄ μ¬μ μν  μ μλ μ¬λ¬ λ©μλλ₯Ό μ κ³΅νλ€. 

  - `onCreate()`: νλκ·Έλ¨ΌνΈκ° μΈμ€ν΄μ€νλμκ³  `CREATED` μνμλλ€. κ·Έλ¬λ μ΄μ μμνλ λ·°κ° μμ§ λ§λ€μ΄μ§μ§ μμμ΅λλ€.
  - `onCreateView()`: **μ΄ λ©μλμμ λ μ΄μμμ νμ₯**ν©λλ€. νλκ·Έλ¨ΌνΈκ° `CREATED` μνλ‘ μ νλμμ΅λλ€.
  - `onViewCreated()`: λ·°κ° λ§λ€μ΄μ§ ν νΈμΆλ©λλ€. μ΄ λ©μλμμ μΌλ°μ μΌλ‘ `findViewById()`λ₯Ό νΈμΆνμ¬ νΉμ  λ·°λ₯Ό μμ±μ λ°μΈλ©ν©λλ€.
  - `onStart()`: νλκ·Έλ¨ΌνΈκ° `STARTED` μνλ‘ μ νλμμ΅λλ€.
  - `onResume()`: νλκ·Έλ¨ΌνΈκ° `RESUMED` μνλ‘ μ νλμκ³  μ΄μ  ν¬μ»€μ€λ₯Ό λ³΄μ ν©λλ€(μ¬μ©μ μλ ₯μ μλ΅ν  μ μμ).
  - `onPause()`: νλκ·Έλ¨ΌνΈκ° `STARTED` μνλ‘ λ€μ μ νλμμ΅λλ€. UIκ° μ¬μ©μμκ² νμλ©λλ€.
  - `onStop()`: νλκ·Έλ¨ΌνΈκ° `CREATED` μνλ‘ λ€μ μ νλμμ΅λλ€. κ°μ²΄κ° μΈμ€ν΄μ€νλμμ§λ§ λ μ΄μ νλ©΄μ νμλμ§ μμ΅λλ€.
  - `onDestroyView()`: νλκ·Έλ¨ΌνΈκ° `DESTROYED` μνλ‘ μ νλκΈ° μ§μ μ νΈμΆλ©λλ€. λ·°λ λ©λͺ¨λ¦¬μμ μ΄λ―Έ μ­μ λμμ§λ§ νλκ·Έλ¨ΌνΈ κ°μ²΄λ μ¬μ ν μμ΅λλ€.
  - `onDestroy()`: νλκ·Έλ¨ΌνΈκ° `DESTROYED` μνλ‘ μ νλ©λλ€.

  <img src = "https://user-images.githubusercontent.com/31370590/126290914-05546013-f2da-4dd0-b899-c93592aadd1f.PNG" width = "350" height = "500"> 

+ μλͺ μ£ΌκΈ° μνμ μ½λ°± λ©μλλ activityμ μ¬μ©λ κ²κ³Ό λ§€μ° λΉμ·ν©λλ€. κ·Έλ¬λ `onCreate()` λ©μλμ μ°¨μ΄μ μ μν΄μΌ ν©λλ€. activityμμλ μ΄ λ©μλλ₯Ό μ¬μ©νμ¬ λ μ΄μμμ νμ₯νκ³  λ·°λ₯Ό λ°μΈλ©ν©λλ€. κ·Έλ¬λ **νλκ·Έλ¨ΌνΈ μλͺ μ£ΌκΈ°μμ `onCreate()`λ λ·°κ° λ§λ€μ΄μ§κΈ° μ μ νΈμΆ**λλ―λ‘ μ¬κΈ°μ λ μ΄μμμ νμ₯ν  μ μμ΅λλ€. λμ  `onCreateView()`μμ νμ₯ν©λλ€. κ·Έλ° λ€μ λ·°λ₯Ό λ§λ  ν `onViewCreated()` λ©μλκ° νΈμΆλκ³  μ¬κΈ°μ μμ±μ νΉμ  λ·°μ λ°μΈλ©ν  μ μμ΅λλ€. 

<br>

## Jetpack Navigation Component

#### Andriod Jetpackμμ μ κ³΅νλ *Navigation component*

- Navigation graph: νμ κ·Έλνλ μ±μμ νμμ μκ°μ μΌλ‘ λ³΄μ¬μ£Όλ XML νμΌμλλ€. νμΌμ κ°λ³ activity λ° fragmentμ μμνλ ***destination***κ³Ό ν destinationμμ λ€λ₯Έ destinationμΌλ‘ μ΄λνλ €κ³  μ½λμμ μ¬μ©ν  μ μλ ***destination μ¬μ΄μ action***μΌλ‘ κ΅¬μ±λ©λλ€. λ μ΄μμ νμΌκ³Ό λ§μ°¬κ°μ§λ‘ Android μ€νλμ€λ νμ κ·Έλνμ λμκ³Ό μμμ μΆκ°νλ μκ°μ  νΈμ§κΈ°λ₯Ό μ κ³΅ν©λλ€.
- `Navhost`: `NavHost`λ **activity λ΄μμ νμ κ·Έλνμ destinationμ νμ**νλ λ° μ¬μ©λ©λλ€. νλκ·Έλ¨ΌνΈ κ°μ μ΄λνλ©΄ `NavHost`μ νμλλ destinationμ΄ μλ°μ΄νΈλ©λλ€. `MainActivity`μμ `NavHostFragment`λΌλ κΈ°λ³Έ μ κ³΅ κ΅¬νμ μ¬μ©ν©λλ€.
- `NavController`: `NavController` κ°μ²΄λ₯Ό μ¬μ©νλ©΄ **`NavHost`μ νμλλ destination κ° νμμ μ μ΄**ν  μ μμ΅λλ€. μΈννΈλ₯Ό μ¬μ©ν  λλ `startActivity()`λ₯Ό νΈμΆνμ¬ μ νλ©΄μΌλ‘ μ΄λν΄μΌ νμ΅λλ€. νμ κ΅¬μ±μμλ₯Ό μ¬μ©νλ©΄ `NavController`μ `navigate()` λ©μλλ₯Ό νΈμΆνμ¬ νμλλ νλκ·Έλ¨ΌνΈλ₯Ό κ΅μ²΄ν  μ μμ΅λλ€. `NavController`λ₯Ό μ¬μ©νλ©΄ μμ€ν 'μλ‘' λ²νΌμ μλ΅νμ¬ μ΄μ μ νμλ νλκ·Έλ¨ΌνΈλ‘ λ€μ μ΄λνλ κ²κ³Ό κ°μ μΌλ°μ μΈ μμμ μ²λ¦¬ν  μλ μμ΅λλ€.

<br>

#### Navigation Component λ₯Ό μ¬μ©νκΈ° μν μ€λΉ

1. Navigation Dependency

   + `build.gradle` νμΌμ **buildscript > ext**μμ `material_version` μλμ `nav_version`μ `2.3.1`λ‘ μ€μ 

     ```kotlin
     buildscript {
         ext {
             nav_version = "2.3.1"
         }
     } 
     ```

   + μ± μμ€ `build.gradle` νμΌμμ μ’μ ν­λͺ© κ·Έλ£Ήμ λ€μμ μΆκ°

     ```kotlin
     implementation "androidx.navigation:navigation-fragment-ktx:$nav_version"
     implementation "androidx.navigation:navigation-ui-ktx:$nav_version"
     ```

2. Safe Args Plug-in

   + **Words** μ±μ νμ κ΅¬μ±μμλ₯Ό κ΅¬ννκΈ° μ μ νλκ·Έλ¨ΌνΈ κ°μ λ°μ΄ν°λ₯Ό μ λ¬ν  λ μ ν μμ μ±μ μ§μνλ Gradle νλ¬κ·ΈμΈμΈ **Safe Args**λΌλ ν­λͺ©λ μΆκ°ν΄μΌ ν©λλ€.

     1. μ΅μμ `build.gradle` νμΌμ **buildscript > dependencies**μμ λ€μ ν΄λμ€ κ²½λ‘λ₯Ό μΆκ°

        ```kotlin
        classpath "androidx.navigation:navigation-safe-args-gradle-plugin:$nav_version"
        ```

     2. μ± μμ€ `build.gradle` νμΌμ μλ¨μ μλ `plugins` λ΄μμ `androidx.navigation.safeargs.kotlin`μ μΆκ°

        ```kotlin
        plugins {
            ~
             id 'androidx.navigation.safeargs.kotlin'
        }
        ```

<br>

#### Navigation Graph μ¬μ©

+ Navigation Graph : νλκ·Έλ¨ΌνΈ κ° νμμ κ΅¬ννλλ° λμμ΄ λλ μκ°μ  νΈμ§κΈ°
+ νμ κ·Έλν(λλ μ€μ¬μ NavGraph)λ μ± νμμ κ°μ λ§€νμλλ€. κ° νλ©΄(λλ μ΄ κ²½μ°μ νλκ·Έλ¨ΌνΈ)λ μ΄λν  μ μλ κ°λ₯ν 'destination'μ΄ λ©λλ€. `NavGraph`λ κ° destinationμ΄ μλ‘ κ΄λ ¨λλ λ°©μμ λ³΄μ¬μ£Όλ XML νμΌλ‘ λνλΌ μ μμ΅λλ€. 
+ νμ κ·Έλνμ destinationμ `FragmentContainerView`λ‘ μ¬μ©μμκ² νμ

<br>

#### MainActivtiyμμ FragmentContainerView μ¬μ©

1. MainActivity μμ 

   `MainActivity`μ μ©λλ₯Ό λ³κ²½νμ¬ νλκ·Έλ¨ΌνΈμ `NavHost` μ­ν μ ν  `FragmentContainerView`λ₯Ό ν¬ν¨ν©λλ€. μ΄ μμ λΆν° λͺ¨λ  μ±μ νμμ `FragmentContainerView` λ΄μμ μ€νλ©λλ€. 

   ```kotlin
   <androidx.fragment.app.FragmentContainerView
      android:id="@+id/nav_host_fragment"
      android:layout_width="match_parent"
      android:layout_height="match_parent"
   
      android:name="androidx.navigation.fragment.NavHostFragment"
      app:defaultNavHost="true"
      app:navGraph="@navigation/nav_graph" 
      />
   ```

   + `activity_main.xml`μμ `FrameLayout`μμ μλ μ‘΄μ¬νλ `recyclerView`λ₯Ό `FragmentContainerView`λ‘ λ°κΏλλ€. 

   + `android:name="androidx.navigation.fragment.NavHostFragment"`λ‘ μ€μ νλ€.  

     μ΄ μμ±μ νΉμ  νλκ·Έλ¨ΌνΈλ₯Ό μ§μ ν  μ μμ§λ§ `NavHostFragment`λ‘ μ€μ νλ©΄ `FragmentContainerView`κ° νλκ·Έλ¨ΌνΈ κ°μ μ΄λν  μ μμ΅λλ€.

   + `app:defaultNavHost="true"`

     μ΄λ κ² νλ©΄ **νλκ·Έλ¨ΌνΈ μ»¨νμ΄λκ° νμ κ³μΈ΅ κ΅¬μ‘°μ μνΈμμ©**ν  μ μμ΅λλ€. μλ₯Ό λ€μ΄ μμ€ν λ€λ‘ λ²νΌμ λλ₯΄λ©΄ μ»¨νμ΄λλ μ νλμ΄ νμλ  λμ λ§μ°¬κ°μ§λ‘ μ΄μ μ νμλ νλκ·Έλ¨ΌνΈλ‘ λ€μ μ΄λν©λλ€.

   + `app:navGraph="@navigation/nav_graph" `

     μ΄λ μ±μ νλκ·Έλ¨ΌνΈκ° μλ‘ μ΄λν  μ μλ λ°©λ²μ μ μνλ XML νμΌμ κ°λ¦¬ν΅λλ€.

     

2. νμ κ·Έλν μ€μ 

   + `nav_graph.xml`μ΄λ¦μ μλ‘μ΄ Android Resource File μμ±(Resource type: Navigation)νλ©΄ μ μκ°μ  νΈμ§κΈ°κ° νμλ©λλ€. `FragmentContainerView`μ `navGraph` μμ±μμ `nav_graph`λ₯Ό μ΄λ―Έ μ°Έμ‘°νμΌλ―λ‘ μ destinationμ μΆκ°νλ €λ©΄ νλ©΄ μλ¨ μΌμͺ½μμ μλ‘ λ§λ€κΈ° λ²νΌμ ν΄λ¦­νμ¬ κ° νλκ·Έλ¨ΌνΈμ destinationμ λ§λ­λλ€. 

   + Navigation Action λ§λ€κΈ°

     `letterListFragment`μμ `wordListFragment` destination κ°μ νμ μμμ λ§λ€λ €λ©΄ `letterListFragment` destination μλ‘ λ§μ°μ€λ₯Ό κ°μ Έκ°μ μ€λ₯Έμͺ½μ νμλλ μμμ `wordListFragment` destinationμΌλ‘ λλκ·Έν©λλ€. νμ΄νλ‘ νμλλ `action_letterListFragment_to_wordListFragment`μ΄λ¦μ actionμ΄ μμ±λ©λλ€. 

   + `WordListFragment`μ μΈμ μ§μ 

     μΈννΈλ₯Ό μ¬μ©νμ¬ νλ μ¬μ΄λ₯Ό μ΄λν  λ μ νλ λ¬Έμκ° `wordListFragment`μ μ λ¬λ  μ μλλ‘ 'extra'λ₯Ό μ§μ νμ΅λλ€. Navigationμ  destination κ°μ λ§€κ°λ³μ μ λ¬λ μ§μνλ©΄μ μ νμ μμ ν λ°©μμΌλ‘ μ΄λ₯Ό μ€νν©λλ€.

     `wordListFragment` destinationμ μ ννκ³  μμ± μ°½μ **Arguments**μμ λνκΈ° λ²νΌμ ν΄λ¦­νμ¬ μ μΈμλ₯Ό λ§λ­λλ€. μΈμλ `letter`λΌκ³  νκ³  μ νμ `String`μ΄μ΄μΌ ν©λλ€. μ¬κΈ°μμ μ΄μ μ μΆκ°ν Safe Args νλ¬κ·ΈμΈμ΄ νμν©λλ€. μ΄ μΈμλ₯Ό λ¬Έμμ΄λ‘ μ§μ νλ©΄ νμ μμμ΄ μ½λμμ μ€νλ  λ `String`μ΄ μμλ©λλ€.



3. νμ μμ μ€ν

   `LetterAdapter`.`kt`λ₯Ό μ΄μ΄ νμ μμμ μ€ν

   + λ²νΌμ `onClickListener()` μ½νμΈ λ₯Ό μ­μ ν©λλ€. λμ  λ°©κΈ λ§λ  νμ μμμ κ²μν΄μΌ ν©λλ€. `onClickListener()`μ λ€μμ μΆκ°ν©λλ€.

     ```kotlin
     val action = LetterListFragmentDirections.actionLetterListFragmentToWordListFragment(letter = holder.button.text.toString())
     ```

     `LetterListFragmentDirections`λ₯Ό μ¬μ©νλ©΄ `letterListFragment`λΆν° κ°λ₯ν λͺ¨λ  νμ κ²½λ‘λ₯Ό μ°Έμ‘°ν  μ μμ΅λλ€. `actionLetterListFragmentToWordListFragment()` ν¨μλ

     `wordListFragment.`λ‘ μ΄λν  νΉμ  actionμλλ€.

   + νμ μμ μ°Έμ‘°κ° μμΌλ©΄ *NavController*(νμ μμ μ€νμ νμ©νλ κ°μ²΄) μ°Έμ‘°λ₯Ό κ°μ Έμμ μμμ μ λ¬νλ `navigate()`λ₯Ό νΈμΆνλ©΄ λ©λλ€.

     ```kotlin
     holder.view.findNavController().navigate(action)
     ```



4. MainActivity κ΅¬μ±

   + `navController` μμ±μ λ§λ­λλ€. `onCreate`μμ μ€μ λλ―λ‘ `lateinit`λ‘ νμλ©λλ€.

     ```kotlin
     private lateinit var navController: NavController
     ```

   + κ·Έλ° λ€μ `onCreate()`μμ `setContentView()`λ₯Ό νΈμΆν ν `nav_host_fragment`(`FragmentContainerView`μ IDμ) μ°Έμ‘°λ₯Ό κ°μ Έμμ `navController` μμ±μ ν λΉν©λλ€.

     ```kotlin
     val navHostFragment = supportFragmentManager
         .findFragmentById(R.id.nav_host_fragment) as NavHostFragment
     navController = navHostFragment.navController
     ```

   + κ·Έλ¦¬κ³  `onCreate()`μμ `setupActionBarWithNavController()`λ₯Ό νΈμΆνμ¬ `navController`λ₯Ό μ λ¬ν©λλ€. μ΄λ κ² νλ©΄ μμ λͺ¨μ(μ± λ°) λ²νΌμ΄ νμλ©λλ€.

     ```kotlin
     setupActionBarWithNavController(navController)
     ```

   + λ§μ§λ§μΌλ‘ `onSupportNavigateUp()`μ κ΅¬νν©λλ€. XMLμμ `defaultNavHost`λ₯Ό `true`λ‘ μ€μ νλ κ²κ³Ό ν¨κ» μ΄ λ©μλλ₯Ό μ¬μ©νλ©΄ **μλ‘** λ²νΌμ μ²λ¦¬ν  μ μμ΅λλ€. κ·Έλ¬λ activityκ° κ΅¬νμ μ κ³΅ν΄μΌ ν©λλ€.

     ```kotlin
     override fun onSupportNavigateUp(): Boolean {
        return navController.navigateUp() || super.onSupportNavigateUp()
     }
     ```

   + μ΄λ λͺ¨λ  κ΅¬μ±μμλ νμμ΄ νλκ·Έλ¨ΌνΈλ‘ μλνλλ‘ μ μλ¦¬μ μμ΅λλ€. κ·Έλ¬λ μ΄μ  νμμ΄ μΈννΈ λμ  νλκ·Έλ¨ΌνΈλ₯Ό μ¬μ©νμ¬ μ€νλλ―λ‘ `WordListFragment`μμ μ¬μ©νλ λ¬Έμμ μΈννΈ extraκ° λ μ΄μ μλνμ§ μμ΅λλ€. λ€μ λ¨κ³μμλ `WordListFragment`λ₯Ό μλ°μ΄νΈνμ¬ `letter` μΈμλ₯Ό κ°μ Έμ΅λλ€.



Navigation APIs

+ `NavHostFragment` : νμ κ΅¬μ±μμκ° κ΅νλλ λͺ©μ μ§ μ»¨νμ΄λ μ­ν μ νλ€. μ΄λ activityλ₯Ό ν΅ν΄  νμν  λ λμ²΄λλ fragmentλ₯Ό λ΄λ μ»¨νμ΄λμ΄λ€.

+ `NavController` : νμ κ΅¬μ±μμ(navigate components)μ λ΄λΆμμλ‘ μ€μ λ‘ νμ μμμ νλ€. μ§νμ€μΈ μμμ λ³΄μ¬μ£Όλ μλ΄μμ κ°λ€.  

+ `NavigationView` : `NavHostFragment`μμ μκ³ , νμ κ΅¬μ±μμμ μΌλΆλ μλ. νμ κ΅¬μ±μμ μ μ μ‘΄μ¬νμΌλ©°, νμ μ°½ λ΄μ μλ λ©λ΄μ κ΄λ ¨μ΄ μμ. λ©λ΄ ν­λͺ©κ³Ό νμ μ°½μ μ ννλ©΄ μ± λ΄ λ€λ₯Έ λͺ©μ μ§λ‘ μ΄λνλ€. νμ§λ§ νμ κ΅¬μ±μμμ μΌλΆκ° μλλ©°, νμ κ΅¬μ±μμμ ν­λͺ©κ³Ό μνΈμμ© νλ κ²μ΄λ€.  

+ `NavigationUI` : `NavHostFragment` μΈλΆ μ½νμΈ  μλ°μ΄νΈλ₯Ό μ±μμ§λλ€. ex) navigationView, BottomNavBar ? 

  => μ΄λ₯Ό μ¬μ©νλ©΄ ν¨μ¬ κ°νΈνκ² μ± λ΄ νμμ λ§λ€κ³  μμ ν  μ μμ.





#### Quiz/Unit3/Pathway2

1. True or False: `onCreateView()` is only called once for a fragmentβs entire lifecycle.

   => False



2. Which of the following is a benefit of using fragments?

   => 

   + Navigation between fragments allows for more sophisticated user interface patterns, such as tab bars.
   + Using multiple fragments within an activity allows for an adaptive layout across multiple screen sizes.
   + The same fragments can be reused across multiple activities.



3. In the fragment lifecycle, which of the following tasks should be performed in `onViewCreated()`?

   => 

   + Binding view objects to properties in your fragment
   + Setting properties of individual views, such as a recycler viewβs adapter



4. In the fragment lifecycle, which of the following tasks should be performed in `onCreateView()`?

   => Inflating the layout



5. The **onSupportNavigateUp()** method needs to be overridden in the host activity to ensure your appβs fragment-based navigation responds to the appβs "Up" button.



6. Given the code for navigating between two fragments in a note-taking app, a list of books and a list of notes, which of the following is true about the navigation graph file?

   => 

   + Both the books list and notes list are destinations.
   + Thereβs an action defined on the navigation graph that goes from the books list to the notes list.