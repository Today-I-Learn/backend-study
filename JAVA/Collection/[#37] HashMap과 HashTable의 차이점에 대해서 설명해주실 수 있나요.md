### HashMap과 HashTable의 차이점에 대해서 설명해주실 수 있나요?

기본적으로 HashMap과 Hashtable 모두 유니크한 Key와 Value의 쌍을 저장하는 자바 Collection 객체로써 이 둘의 가장 큰 차이는 메서드의 구현에 있습니다.
Hashtable의 경우 대부분의 연산에 `synchronized` 키워드를 붙여 명시적으로 동기화를 수행하고 있지만 HashMap은 연산에 `synchronized` 키워드를 사용해서 명시적으로 동기화를 수행하고 있지 않습니다.
때문에 멀티 스레드 환경에서 Hashtable이 HashMap에 비해서 Thread Safe함을 보장할 수 있지만 동기화 처리로 인하여 HashMap보다 낮은 성능을 보이고 있습니다.
또한 Hashtable에서는 객체를 저장할 때 `hashCode`를 구현한 객체만 저장할 수 있기 떄문에 `null`값은 객체가 아니므로 Key와 Value에 모두 `null`을 사용할 수 없습니다. 반면에 HashMap은 `null`값을
저장하는 것에 대한 예외를 허용하고 있기때문에 `null`을 Key와 Value으로 사용할 수 있습니다.

HashMap은 내부적으로 보조 해시함수와 Seperate Chaining 방식을 사용하여 데이터를 저장하고 있기 때문에 Hashtable에 비해서 충돌이 덜 발생한다는 장점이 있으며 이 외에도 각각 Key값을 순회하기 위해서 `Iterator`과 
`Enumeration`을 사용한다는 등의 차이가 존재합니다. 


