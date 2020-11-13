# Goal

```
- DTO(Data Transfer  Object)란 무엇인지 이해한다.
- package 구조에 따른 흐름, 해당 package의 역할 및 기능을 이해한다.
```

## DTO(Data Transfer Object)란?
dto package
- 계층간 데이터를 교환을 위한 객체(Java Beans)이다.
    - DB에서 데이터를 얻어 Service나 Controller 등으로 보낼 때 사용하는 객체를 말한다.
    - 로직을 갖고 있지 않는 순수한 데이터 객체이며, getter/setter 메서드만을 갖는다.
    - 하지만 DB에서 꺼낸 값을 임의로 변경할 필요가 없기 때문에 DTO클래스에는 setter가 없다. (대신 생성자에서 값을 할당한다.)
- Request와 Response용 DTO는 View를 위한 클래스
    - 자주 변경이 필요한 클래스
    - Presentation Model
    - toEntity() 메서드를 통해서 DTO에서 필요한 부분을 이용하여 Entity로 만든다.
    - 또한 Controller Layer에서 Response DTO 형태로 Client에 전달한다.

## DTO 는 어디서 처리되어야 할까?
DTO 는 데이터를 어딘가로 전달하는 목적을 가지고 있으며 서비스는 내부 서비스를 호출할수도 있고 컨트롤러에서 여러 서비스를 호출하여 새로운 객체를 외부 시스템으로 전달할수도 있다. 그렇기 때문에 서비스에서는 도메인 클래스를 반환 해야 하며 DTO 의 정책이 변경되었을때 유연하게 대처할수 있게 된다.

## DTO 의 불변성
DTO 의 목적은 데이터를 전달 하기 위함인데 중간에서 데이터가 변경 되면 데이터의 신뢰도와 안정성이 떨어지게 된다.
