### Java를 사용하여 Multi Thread 환경에서 개발시 고려해야되는 점은 어떤것들이 있나요?

멀티스레드 환경에서 고려해야되는 부분으로는 Field member, 동기화, ThreadLocal이 있습니다.

Field member란 클래스에 변수를 정의하는 공간을 의미합니다. 이곳에 변수를 만들면 메소드끼리 변수를 주고 받는데 있어서 참조가 쉬워집니다.
하지만 객체가 여러 스레드가 접근하는 싱글톤 객체라면 field에서 상태값을 갖고 있을 경우 각각의 스레드에 영향을 줄 수 있기 때문에 상태값을 갖고 있으면 안됩니다.
모든 변수를 parameter로 넘겨받고 return 하는 방식으로 코드를 작성하는 것이 멀티스레드 환경에서 필요합니다.

(내용보충)

만약 변수가 Atomic 타입과 같은 동기화 문제 해결이 보장되는 상황에서는 앞의 내용들이 강제성을 띄지 않습니다.
Atomic 변수는 멀티스레드 환경에서 동기화 문제를 해결하기 위해 synchronized 키워드를 사용해 락을 걸곤 하는데 이런 키워드 없이 동기화 문제를 해결하기 위해 고안된 방법입니다.

field에 Collection이 필요한 경우에는 자바에서는 synchronized 키워드를 사용하여 스레드 간 race condition 을 통제합니다.
Collections라는 util 클래스에서 제공되는 static 메소드를 통해 일반적인 List,set,Map 이 아닌 Collections.synchronizedList(), Collections.synchronizedSet(), Collections.synchronizedMap()을 사용 할 수 있습니다.
JDK 1.7 부터는 concurrent package를 통해 ConcurrentHashMap이라는 구현체를 제공합니다. Collections util 을 사용하는 것보다 synchronized 키워드가 적용된 범위가 좁아서 보다 좋은 성능을 낼 수 있습니다.

(내용보충)

멀티 스레드 환경에서 일반적인 Map을 사용했을 경우 Out of memory error 를 유발할 가능성이 있습니다.
여러 스레드가 동시에 Map에 접근하는 메서드를 호출하면 synchronized 블록을 사용하지 않은 경우 Map 내부 값들과 연결되는 레퍼런스가 올바르게 연결되지 않게 됩니다.
이러한 경우 레퍼런스가 남은 객체는 GC가 처리할 수 없으므로 메모리를 계속 차지하게 되고, 이러한 일이 반복되면 차지하는 메모리가 점점 증가하여 결국 메모리 부족 오류가 발생하게 됩니다.

마지막으로 ThreadLocal은 스레드 사이에 간섭이 없어야 하는 데이터에 사용한다. 멀티스레드 환경에서는 클래스의 필드에 멤버를 추가할 수 없고 매개변수로 넘겨받아야 하기 때문입니다.
즉, 스레드 내부의 싱글톤을 사용하기 위해 사용하며. 주로 사용자 인증, 세션 정보, 트랜잭션 컨텍스트에 사용합니다.
스레드 풀 환경에서 ThreadLocal 을 사용하는 경우 ThreadLocal 변수에 보관된 데이터의 사용이 끝나면 반드시 해당 데이터를 삭제해 주어야 하며 그렇지 않을 경우 재사용되는 쓰레드가 올바르지 않은 데이터를 참조할 수 있습니다.

