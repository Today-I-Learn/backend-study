### HashSet과 TreeSet의 차이점은 무엇인가요?

HashSet은 Set 인터페이스의 구현 클래스 입니다. HashSet은 객체들을 순서 없이 저장하고 동일한 객체는 중복 저장하지 않습니다.
HashSet에서의 동일한 객체는 꼭 같은 인스턴스를 뜻하지는 않으며 객체를 저장하기 전에 객체의 hashCode() 메소를 호출해 해시코드를 얻어낸 뒤 저장되어 있는 객체중 동일한 해시코드가 있다면 다시 equals() 메소드로 두 객체를 비교해 true가 나오면 동일한 객체로 판단하고 중복 저장을 하지 않습니다.

TresSet은 Set 컬렉션의 검색 기능을 강화시킨 컬렉션 입니다. 이진 트리 구조를 사용하여 tree 구조를 가지면서 객체를 저장합니다.
TreeSet 각각의 노드는 노드값인 value와 왼쪽과 오른쪽 자식 노드를 참조하기 위한 두개의 변수로 구성됩니다.
TreeSet에 객체를 저장하면 자동으로 정렬되는데 부모값과 비교해서 낮은 값은 왼쪽 자식 노드에 , 높은 것은 오른쪽 자식 노드에 저장하게 됩니다.

같은 Set 컬렉션이지만 HashSet과 TreeSet의 차이점은 HashSet은 해시테이블을 이용하여 구현하기 때문에 그 요소들이 정렬되지 않습니다.
또한 HashSet의 add, remove, contains 메소드는 일정한 시간복잡도인 O(1)을 갖습니다.
반면에 TreeSet은 각각의 요소들을 자동으로 정렬시키며 add, remove, contains 메소드의 시간복잡도가 O(logN)을 갖게 됩니다.

[내용 보충]

LinkedHashMap은 HashMap을 확장하는 클래스입니다. LinkedHashMap의 가장 큰 특징은 자료가 입력된 순서를 기억한다는 것입니다.
HashMap의 경우 데이터 입력되는 순서를 보장하지 않습니다. 그렇기 때문에 HashMap의 모든 데이터를 꺼내기 위해서는 keySet()을 통해 HashMap 전체를 순회해야 합니다.
즉 반환되는 Set의 동작에서 HashMap의 데이터 입력순서가 보장되지 않기 때문에 이 순서는 Java 버전에 따라 달라질수도 있고 환경에 따라 달라질 수도 있습니다.
만약 사진을 찍은 사진과 같은 키-값 쌍이 필요하거나 전체 크기를 알지 못하거나 사진을 찍은 순서대로 동영상을 변환해야하는 순서를 알아야 하는 경우들의 경우 LinkedHashMap을 유용하게 사용할 수 있습니다. 