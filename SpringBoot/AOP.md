# 관심사의 분리
- 프로그래밍의 기초 개념중 하나
- 관심이 같은것 끼리는 하나의 객체 안에 모이게 하고 다른 것은 가능한 한 따로 떨어져 서로 영향을 주지 않도록 분리

### 인터페이스 도입

```java
public class UserDao {
    ConnectionMaker connectionMaker;

    public UserDao {
        this.connectionMaker = new NConnectionMaker(); // 이건뭐지? 여기에 클래스 이름이 나오네!?
    }

    public void add(User user) throws ClassNotFoundException, SQLException {
        Connection c = connectionMaker.makeConnection();

        ......
    }
}
```

```java
public interface ConnectionMaker {
    public Connection makeConnection() throws ClassNotFoundException, SQLException;
}
```

```java
public class NConnectionMaker implements ConnectionMaker {
    public Connection makeConnection() throws ClassNotFoundException, SQLException {
        Class.forName("oracle.jdbc.driver.OracleDriver");

        Connection c = DriverManger.getConnection("jdbc:oracle:thin:@111.111.11.11:8082:edu", "edu", "edu");

        return c;
    }
}
```

### 위 UserDao의 문제점은 무엇일까?
- 클래스 사이에 불필요한 의존관계를 갖고 있는 구조
- UserDao가 NConnectioMaker를 알고 있기 때문에 생긴 불필요한 의존관계 (의존적)

### 그렇다면 어떻게 해결할 수 있을까?
- 생성자를 통한 의존관계 주입
- 생성자를 통해 의존관계를 느슨하게 한다

```java
public class UserDao {

    ConnectionMaker connectionMaker;

    public UserDao(ConnectionMaker connectionMaker) {
        this.connectionMaker = connectionMaker; // 생성자 파라미터를 통해 ConnectionMaker 구현체를 전달 받음
    }
}
```

```java
public class UserDaoTest {

    public static void main(String[] args) throws ClassNotFoundException, SQLException {

        ConnectionMaker connectionMaker = new NConnectionMaker();

        UserDao userDao = new UserDao(connectionMaker); // UserDao가 사용할 ConnectionMaker 구현 클래스를 결정하고 오브젝트를 만든다

        ............
    }
}
```