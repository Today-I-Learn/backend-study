### DBCP(Database Connection Pool)을 사용하는 이유가 무엇인가요??
<br>

- **DBCP(Database Connection Pool) 란?**

DBCP는 DataBase Connection Pool의 약자이며, 데이터베이스와 애플리케이션을 효율적으로 연결하는 커넥션 풀 라이브러리를 말합니다.
이러한 DBCP는 WAS가 실행되면서 미리 일정량의 DB Connection 객체를 생성하고 Pool이라는 공간에 저장합니다.
저장된 DB Connection 객체는 요청에 따라 필요할 때마다 Pool에서 가져다 쓰고 반환할 수 있습니다.
따라서 요청할 때마다 DB Driver에 로드하여 물리적인 Connection 객체를 생성하는 비용이 줄어들어 효율적인 DB Connection을 제공합니다.
  
- **DBCP(Database Connection Pool) 사용 이유**

첫번째 이유로는
애플리케이션 서버에서 Database 로 Connection 을 맺는 일은 매우 느리며 자원을 많이 소모하는 작업이기 때문입니다. 
만약 불 특정 다수의 사용자들이 동시에 Database 의 Connection 을 요구한다면 최악의 경우 server 가 down 되기도 합니다.
이것을 해결하기 위해 Connection pool 을 사용합니다.

두번째 이유로는
커넥션 풀을 사용하지 않으면동시 접속해서 사용하려는 client 수만큼 Connection 객체를 생성해야 하는데
커넥션 풀을 사용한다면 최대로 동시에 빌려 줄 수 있는 Connection 을 설정하였을 시 
그 이상 접속하였을 경우 Connection 을 다른 클라이언트가 반납할 때까지 대기 하도록 해서 Connection 객체의 수를 제한할 수 있습니다.
이를 DB 서버의 수용 가능한 범위내에서 조절하면 DB 서버의 가용성을 높일 수 있습니다.

- **Connection 을 맺는 과정이 왜 오래 걸리는지?**

최초 DB 접속 시 TCP/IP Socket 통신을 하여 연결부분에서 많은 시간이 지체되고, 
사용자 인증과 권한 검사를 수행하고 요청 처리를 위한 준비 작업을 해야하기 때문입니다. 