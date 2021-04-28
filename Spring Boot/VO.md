## 들어가며
프로그래밍을 하며, VO라는 단어를 들어보셨을겁니다.

하지만 VO라는 단어가 실무에서 혼란스럽게 쓰이고 있습니다.

구글에 VO를 검색해보면 아직도 여러 글들이 Getter/Setter만 있는 객체를 VO 라고 칭하고 있는데 이를 DTO로 칭하는게 혼란의 여지가 적습니다.

### Martin Fowler의 Value-Object

> Martin Fowler의 글에 의하면
>
>나는 구별하는 방법에 따라 값 객체와 참조 객체,
>두 가지 클래스의 객체를 고려하는 것이 유용하다는 것을 알게 되었다.
>
>용어의 혼란이 온것은 세기가 바뀔 무렵 J2EE 문헌에서 
>Date Transfer Object를 Value Object라고 사용했었기 때문이다.
>그러한 사용은 지금으로서는 대부분 사라졌지만, 너는 여전히 우연히 접할 수 있을 것이다.

그렇다면, Value-Object와 Reference-Object를 구분하는 방법을 알아봅시다.

### VO (Value-Object)?
Martin Fowler가 언급한 VO의 개요는 다음과 같습니다.

>프로그래밍할 때, 사물을 복합물로 표현하는 것이 유용한 경우가 종종 있다.<br>
>(복할물: 두 가지 이상의 성분이 섞인 물질)<br>
>예를 들어, 2차원 좌표는 x, y로 이루어져 있고,<br>
>돈이나 통화 같은 경우 숫자로 이루어져 있다.<br>
>날짜의 범위는 시작 날짜와 종료날짜로 구성될 수 있고,<br>
>연도와 월, 일의 복합물일 수 도 있다.

즉, Value-Object 란, 한개 혹은 그 이상의 속성들을 묶어서 특정 값을 나타내는 객체를 말합니다.<br>
VO는 도메인 객체의 일종이며, 보통 기본키로 식별 값을 갖는 Entity와 구별해서 사용합니다.<br>
그렇다면 VO는 어떤 조건들에 의해 구분해서 사용하는지 알아봅시다.


### 1.equals & hash code 메서드 재정의
일반적으로 타입이 같고, 내부의 속성 값도 같은 두 객체가 있다면, 두 객체는 값은 객체라고 취급할 것 입니다.

`오히려 다르다고 하는게 더 이상하다고 생각 할 수도 있습니다.`<br>
`예를들면, 빨간색이 빨간색과 다르다고 하는것과 같습니다.`

하지만 실제로, 값이 같은 두 객체를 생성하고 객체를 비교해보면 둘은 서로 다른 객체로 비교됩니다.

좌표를 예시로 한 코드를 보면,
```java
public class Point {
    private int x;
    private int y;
    
    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}

@Test
public void isPointEqauls() {
    Point point1 = new Point(1, 2);
    Point point2 = new Point(1, 2);
    
    // point1 != point2
    Assertions.assertTaht(point1 == point2).isFalse();
}
```

테스트 실행 시 같은 값을 가진 좌표1과 좌표2는 다른 객체라는걸 알 수 있습니다.<br>
분명 사람이 보기엔 같은 값을 가진 좌표니 같은 좌료인데 다른 좌표라고 합니다.<br>
이러한 점은 우리가 현실과 같은 도메인을 설계하고 객체를 사용하는 점에 있어 혼란을 줍니다.


이 문제를 해결하기 위해서는 동일성 비교와 동등성 비교의 차이에 대해 알아야 합니다.

>동일성 비교<br>
>동일성 비교는 해당 객체가 참고하고 있는 주소 값을 확인합니다.<br>
>하지만 현재 상태에서 Point1과 Point2가 참조하고 있는 메모리의 주소 값은 다르며,<br>
>이 주소 값은 임의로 바꿀 수 없습니다.
>
>동등성 비교<br>
>동등성 비교는 객체가 포함하고 있는 속성 값을 기준으로 객체를 비교 합니다.<br>
>이러한 동등성 비교를 구현하기 위해서는 equals 메소드를 재정의함으로써 가능해집니다.<br>
>equals 메소드 재정의 시에는 어떠한 속성 값들을 기준으로 동등성을 비교할 것인지 정해야 합니다.

위의 Point 객체의 equals 메소드와 hashCode 메소드를 재정의 해봅시다.

```java
// equals & hashCode 재정의
@Override
public boolean equals(Object o) {
    if (this == o) {
        return true;
    }
    
    if (o == null || getClass() != o.getClass()) {
        return false;
    }
    
    final Point point = (Point) o;
    return x == point.x && y == point.y;
}

@Override
public int hashCode() {
    return Object.hash(x, y);
}
```

>객체의 hash code는 객체를 식별할 하나의 정수 값을 가리키고,<br>
>재정의 하지 않으면 메모리 주소 값을 사용해서 해쉬 값을 만듭니다.<br>
>특정 값을 기준으로 같은 해쉬 코드를 얻을 수 있고,<br>
>이는 해쉬 값을 사용하는 컬렉션 등에서 객체를 비교하는 용도로 사용됩니다.

재정의 한 equlas 메소드와 hashCode 메소드를 Test 해봅시다.

```java
@Test
public void isPointAttributesEquals(){
    Point point1 = new Point(1, 2);
    Point point2 = new Point(1, 2);
    
    //point1 == point2
    Assertions.assertThat(point1.equals(point2)).isTrue();
    //point1.hashCode() == point2.hashCode()
    Assertions.assertThat(point1.hashCode() == point2.hashCode()).isTrue();
}
```

이처럼 equals 메소드와 hashCode 메소드를 재정의하면, VO를 사용할 때 속성값이 같은 객체임을 보장하면서 VO를 사용할 수 있습니다.

### 2. 수정자(Setter)가 없는 불변(Immutable) 객체
>Entity와 같은 경우 별도의 식별 값을 가지고 있기 때문에 내부 속성 값이 변경된다고 하더라도
>같은 객체로 계속 인식하고 추적할 수 있습니다.<br>
>하지만 속성 값 자체가 식별 값인 VO는 속겅 값이 바뀌게 되면 식별 값도 바뀌게 되어 추적이 불가능하고,<br>
>복사 될 때는 의도치 않은 객체들이 함께 변경되는 문제를 유발합니다.<br>
>따라서 VO는 값을 변경할 수 없는 불변 객체로 만들어야 합니다. <br>

예시를 통해 불변 객체로 만들어야 하는 이유를 알아봅시다.

```java
@Getter
@Setter
@NoArgsConsructor
@EqualsAndHashCode
@ToString
public class Subsidy{
    private String country;
    private String category;
    private int familyCount;
}

@Test
public void 보조금지급() {
    Subsidy 첫번째가구 = new Subsidy();
    첫번째가구.setCountry("한국");
    첫번째가구.setCategory("근로장려금");
    첫번째가구.setFamilyCount(1);
    
    System.out.println("첫번째가구:" + 첫번째가구);
    //첫번째가구 = (country=한국, category=근로장려금, familyCount=1)

    Subsidy 두번째가구 = 첫번째가구;
    System.out.println("두번째가구:" + 두번째가구);
    //두번째가구 = (country=한국, category=근로장려금, familyCount=1)

    두번째가구.setCategory("자녀장려금");
    두번째가구.setFamilyCount(4);

    System.out.println("첫번째가구:" + 첫번째가구);
    System.out.println("두번째가구:" + 두번째가구);
    //첫번째가구 = (country=한국, category=자녀장려금, familyCount=4)
    //두번째가구 = (country=한국, category=자녀장려금, familyCount=4)
    
}
```

>국가의 보조금을 정하는 국가이름, 보조금 범주, 가족 수를 값으로 갖는 Subsidy라는 VO를 만들었습니다.<br>
>두 가구의 보조금 신청이 들어왔고, 같은 1인가구 근로장려금을 신청하여 객체를 복사하여 사용했습니다.<br>
>어차피 같은 보조금이고 가족 수가 값으니 문제될 게 없다고 생각 했습니다.<br>
>
>그런데 이 때, 두 번째 가구의 심사 결과가 4인가구의 자녀장려금 대상자로 나왔습니다.<br>
>분명 두 번째 가구의 내용만 변경했을 뿐인데, 출력된 결과를 살펴보면, 첫 번째 가구까지 4인 가구 자녀장려금으로 보조금이 변경되었습니다.<br>
>
>문제의 시작은 사용할 값이 같다고 해서 첫 번째 가구 값을 두 번째 가국에 그대로 복사한 곳 입니다.<br>
>현재 두 번째 가구는 첫 번째 가구 값을 복사한 것이 아닌 참조하고 있는 메모리 주소를 복사했기 때문에<br>
>보조금 내용이 바뀌면 메모리 안에 저장된 실제 값이 변경됩니다.<br>
>당연히 같은 메모리를 참조하고 있는 첫 번째 가구의 내용도 변경된 값을 가리키게 되는 것 입니다.

이러한 치명적인 오류를 방지하기 위해서 VO는 한번 설정된 값이 변하지 않도록 해야 합니다.<br>
즉, 값을  변경할 수 있는 수정자(Setter)가 없어야 합니다.

그럼 수정자 없이 어떻게 VO에 값을 설정할까요?<br>
생정자를 통해 객체가 생성될 때, 값이 한 번만 할당되고 이후로는 변경되지 않도록 만들 수 있습니다.<br>
생성자를 통해서 Subsidy 객체를 불변(Immutable)로 만들면 위와 같은 문제를 해결할 수 있습니다.