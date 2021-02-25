# JavaBean

## JavaBean 이란?
자바빈 규약에 따르는 클래스를 자바빈이라 한다.

### 자바빈 규약
1. 모든 멤버 변수의 접근제한자는 private 이어야 하며 getter/setter 메서드로만 접근이 가능해야 한다.

2. Argumnet가 없는 public 생성자가 있어야 한다.

3. java.io.Serializable 인테페이스를 구현 한다.

### 무엇을 위한 규칙인가?
자바빈의 목적은 여러가지 다른 오브젝트들을 하나의 오브젝트(Bean)에 담기 위함이다. 자바빈 규약을 소프트웨어 프로토콜이라 생각하면 쉽다.

### 왜 private 필드와 getter/setter 메서드로만 이뤄져야 하는가?
이는 자바빈만의 표준이 아니다. 이런 표준을 지키는 클래스를 POJO(Plain Old Java Object)라고 부른다. 그래서 그 이유는 Encapsulation을 위해서 이다.

### 왜 java.io.Serializable 인터페이스를 구현하는가?
자바빈의 목적은 여러 오브젝트를 하나의 오브젝트에 담기 위함이라고 했다. 담아서 무엇을 하는가? 우리는 보통 담아서 네트워크를 통해 다른 곳으로 전달 하거나 데이터베이스에 저장 한다. 하지만 오브젝트는 바이트형이 아니라서 스트림을 통해 전달할 수 없다. 따라서 스트림을 통해 전달하려면 바이트로 변환하는 작업이 필요한데 이 작업을 Serialization. 즉, 직렬화라 한다. 그래서 자바빈을 저장하거나 전송하는 일이 많기 때문에 표준에 포함된것 같다.

- [직렬화 참고](https://ktko.tistory.com/entry/JAVA-%EA%B0%9D%EC%B2%B4%EC%9D%98-%EC%A7%81%EB%A0%AC%ED%99%94Serializable-serialVersionUID)