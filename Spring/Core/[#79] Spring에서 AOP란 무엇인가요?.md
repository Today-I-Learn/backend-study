### Spring에서 AOP란 무엇인가요?
AOP란 Aspect Oriented Programming의 약자로 관점 지향 프로그래밍을 의미합니다.
소스 코드상에서 다른 부분에 계속 반복해서 쓰는 코드들을 발견할 수 있는 데 
이것을 Aspect로 모듈화하고 핵심적인 비즈니스 로직에서 분리하여 재사용하겠다는 것이 AOP의 취지입니다.

OOP는 비지니스 로직 모듈화를 하지만 AOP의 경우 로깅,트랜잭션,보안과 같은 인프라 혹은 부가기능을 모듈화를 합니다.

AOP의 주요 개념으로는 Target, Aspect, Advice, PointCut, JoinPoint가 있습니다.

<!--  
- Target은 부가기능을 부여할 대상을 의미합니다.
- Aspect는 객체지향 모듈을 Object라고 부르는 것과 비슷하게 부가기능 모듈을 Aspect라고 부릅니다.
부가될 기능을 정의한 Advice와 Advice를 어디에 적용할지를 결정하는 PointCut을 함께 갖고 있습니다.
- Advice는 부가기능을 담은 구현체를 의미합니다.
- JoinPoint는 Aspect를 적용 가능한 지점을 의미합니다.
- PointCut은 Joinpoint의 부분 집합으로서 실제로 Advice가 적용되는 Jointpoint를 나타냅니다.
-->