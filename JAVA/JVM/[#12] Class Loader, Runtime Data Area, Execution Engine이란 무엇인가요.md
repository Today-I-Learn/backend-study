###  Class Loader, Runtime Data Area, Execution Engine 이란 무엇인가요?


 Class Loader, Runtime Data Area, Execution Engine은 JVM을 구성하는 요소입니다.

 자바에서 소스를 작성하면 .java 파일이 생성되고 이것을 자바 컴파일러가 컴파일하면 .class파일인 바이트코드가 생성됩니다.
 이렇게 생성된 클래스파일들을 JVM이 운영체제로부터 할당받은 메모리 영역인 Runtime Data Area로 적재하는 역할을 Class Loader가 수행하게 됩니다.
 자바 애플리케이션이 실행중일때 이러한 작업들이 수행됩니다.

 Execution Engine은 Class Loader에 의해 메모리에 적재된 클래스들을 기계어로 변경해 명령어 단위로 실행하는 역할을 합니다.
 명령어를 실행하는데에는 하나하나 실행하는 인터프리터 방식이 있고 JIT 컴파일러를 사용하여 바로 사용할 수 있도록 기계어로 변경하여 수행시간을 최적화하여 실행하는 방식이 있습니다.

 Runtime Data Area는 JVM의 메모리 영역으로 자바 애플리케이션을 실행할 때 사용되는 데이터들을 적재하는 영역입니다.
 이 영역은 크게 Method Area, Heap Area, Stack Area, PC Register, Native Method Stack 이렇게 총 5가지로 나눌수 있습니다.


 ### Runtime Data Area의 5가지 영역에 대해 설명해줄수 있나요?

 Method Area는 클래스 멤버 변수의 이름, 데이터 타입, 접근 제어자 정보같은 필드 정보와 메소드의 이름, 리턴 타입, 파라미터, 접근 제어자 정보같은 메소드 정보, Type정보, Constant Pool, static 변수, final class 변수등 이 생성되는 영역입니다.

 Heap Area는 new 키워드를 사용하여 생성된 객체와 배열들이 생성되는 영역입니다.
 메소드 영역에 로드된 클래스들만 생성이 가능하고 Garbage Collector가 참고되지 않는 메모리를 확인하고 제거하는 영역입니다.

 Stack Area는 지역변수, 파라미터, 리턴 값, 연산에 사용되는 임시 값들이 생성되는 영역입니다.
 int a = 10; 라는 소스를 작성했다면 정수값이 할당될 수 있는 메모리공간을 a라고 잡아두고 그 메모리 영역에 값이 10이 들어갑니다. 즉, 스택에 이름이 a이고 값이 10인 메모리 공간을 만들게 됩니다. 
 클래스 Person p = new Person(); 라는 소스를 작성했다면 Person p는 스택 영역에 생성되고 new로 생성된 Person 클래스의 인스턴스는 힙 영역에 생성됩니다. 
 그리고 스택영역에 생성된 p의 값은 힙 영역의 주소값을 갖게 됩니다. 즉, 스택 영역에 생성된 p가 힙 영역에 생성된 객체를 참조하고 있는 것입니다.

 PC Register는 스레드가 생성될 때마다 생성되는 영역으로 현재 쓰레드가 실행되는 부분의 주소와 명령을 저장하고 있는 영역입니다. 이를 통해 스레드가 돌아가면서 수행이 가능하도록 합니다.

 Native method stack은 자바 외 언어로 작성된 네이티브 코드를 위한 메모리 영역이며 보통 C/C++등의 코드를 수행하기 위한 스택입니다.



 