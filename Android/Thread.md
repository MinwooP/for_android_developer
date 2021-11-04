# Thread

한 개의 프로그램(프로세스)에서는 많은 스레드를 동시에 처리할 수 있다. 그리고 프로세스의 메모리 또한 공유한다. 프로세스로부터 각 메모리를 할당 받은 스레드는 독립적으로 실행된다.

<br>

안드로이드 역시 1개의 앱(프로그램)에서 여러개의 스레드를 사용할 수 있다. 예를 들어, **음악을 들을 때, 다운로드를 받을 때, 푸쉬 알림** 등이 모두 스레드를 이용한 기능이다.

<br>

#### 1. 메인 스레드

액티비티를 포함해 모든 컴포넌트가 실행되는 오직 1개만 존재하는 스레드이다. 

그래서 메인 스레드에는 제약사항이 몇 가지 있다.

+ 화면의 **UI를 그리는 처리**를 담당한다.
+ **UI와 상호작용**하고, 이벤트 결과를 사용자에게 보여준다.
+ UI 이벤트 등 작업에 일정시간 동안 응답이 없으면 *ANR 팝업을 표시한다. (ANR : 응용 프로그램이 응답하지 않음)

<br>

#### 2. 백그라운드 스레드

메인 스레드가 UI 처리 및 사용자와의 상호작용을 한다면, 백그라운드 스레드는 그 나머지를 모두 맡아서 처리합니다. 이를 테면, 네트워크 작업 및 파일 다운로드 등 시간이 오래 걸리는 작업들이다. 그래서 안드로이드는 종료 시간을 알 수 없는 작업들에 대해서는 이 백그라운드 스레드에서 처리하길 권장하고 있다.

안드로이드는 **메인 스레드가 아닌 스레드에서는 UI에 접근할 수 없는 치명적인 규칙**이 있다. 즉, 다른 스레드 내에서 TextView에 접근할 수 없다는 것이다. 

<br>

#### 3. 스레드 만들어보기
