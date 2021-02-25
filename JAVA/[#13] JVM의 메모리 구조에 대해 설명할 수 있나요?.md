### JVM의 메모리 구조에 대해 설명할 수 있나요?
<br>
JVM의 메모리 구조는 총 5가지 입니다. <br>
1. method Area(메소드 영역) : 클래스 변수의 이름, 타입, 접근제어자 등과 같은 클래스와 관련된 정보를 저장합니다. 
                             그외에도 static 변수, 인터페이스 등을 저장합니다.
                             또한, 모든 스레드에서 공유하며, JVM 시작시 생성되고 프로그램 종료까지 유지됩니다.
                             
2. Heap Area (힙 영역) : new를 통해서 생성된 객체와 배열의 인스턴스를 저장하는 곳입니다. 
                         힙영역에서 생성된 객체는 스택 영역의 변수나 다른 객체의 필드에서 참조합니다. 
                         명시적으로 null, 참조되지 않는 객체는 GC의 대상이 됩니다.
                         
3. Stack Area (스택 영역) : 메소드가 실행되면 스택 영역에 메소드에 대한 영역이 1개 생성됩니다.
                           스택 영역에서는 지역변수, 매개변수, 리턴값 등을 저장합니다.
                           메소드가 호출될 때마다 프레임이라고 불리는 영역으로 할당되며 프레임별로 관리됩니다. 
                           primitive 타입은 바로 스택영역에 저장되고, 그 외에는 힙영역이나 메소드 영역의 객체 주소를 저장합니다.
                           
4. PC register : 스레드가 시작될 때 생성되며, 현재 스레드가 실행되는 부분의 주소와 명령을 저장합니다.

5. Native Method Stack : 자바 외의 언어로 작성된 코드를 위한 메모리 영역입니다. JNI (Java Native Interface)에 의해 실행됩니다

<br>

Heap 영역은 크게 Young Generation, Old Generation 로 나눌수 있습니다. 
<br>
Young Generation은 새롭게 생성한 객체들이 위치합니다. 대부분의 객체는 금방 접근 불가능한 상태가 되기 때문에, 
많은 객체가 Young 영역에 생성되었다가 사라집니다. Young Generation은 Eden 1개와 Survivor1,2로 구성됩니다. 
이 때, Eden은 Object가 heap에 최초로 할당되는 장소이며 Eden영역이 꽉차면 Object의 참조 여부에 따라 Survivor영역으로 넘깁니다.
Survivor영역에서는 각 영역이 채워지게 되면, 살아남은 객체는 비워진 Survivor로 이동합니다. 이때 참조가 없는 객체들은 Minor GC로 수집 됨
따라서, 항상 Survivor1과 2중 한 곳은 비어있는 상태입니다.
(Minor GC는 Eden, Survivor에서 발생하는 GC를 말합니다.)
<br>
Old Generation은 Young 영역에서 계속 사용되어 살아남은 객체가 복사되는 영역입니다. Young 영역보다 크게 할당되며,
Major GC가 이루어지며, Minor GC보다 횟수가 적음
(Major GC는 Old, Permanent 영역에서 발생하는 GC를 말합니다.)        
<br>
Permanent : Class, Method 등의 Code등이 저장되는 영역으로 JVM에 의해 사용됩니다.
