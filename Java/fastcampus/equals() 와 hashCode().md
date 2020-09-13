# 1.equals()
두 객체의 내용이 같은지 확인하는 메서드

```java
Memeber lee = new Member(1000, "lee");
Memeber kim = new Member(1000, "kim");

System.out.println(lee.equlas(kim)); // false;
```

### 왜 결과가 false 일까요?
- Object에 정의된 equals()를 확인하면 단순히 Object의 ==로 비교하는걸 확인할 수 있다.

```java
public boolean equals(Object obj) {
    return (this == obj);
}
```

### 어떻게 값이 동일한지 비교할 수 있을까요?
- equals()를 오버라이드 하면 해결할 수 있다.

```java
@Override
public boolean equals(Object obj) {
    if(obj instanceof Member) {
        Member member = (Member) obj;
        return (this.id == member.getId());
    }

    return false;
}
```

# 2.hashCode()
두 객체가 같은 객체인지 확인하는 메서드

```java
HashSet hashSet = new HashSet();

Memeber lee = new Member(1000, "lee");
Memeber kim = new Member(1000, "kim");

hashSet.add(lee);
hsashSet.add(kim);

Iterator ir = hashSet.iterator();
~~~중략~~~
//lee 의 아이디는 1000번 입니다.
//kim 의 아이디는 1000번 입니다.
```

### 왜 중복된 아이디가 나올까요?
- Hash를 사용한 Collection(HashMap, HashTable, HashSet, LinkedHashSet 등)은 key를 결정할때 hashCode()를 사용하기 때문에 그렇다.
- hashCode()로 native call을 하여 Memory에서 가진 해쉬 주소값을 출력한다.

### 어떻게 key 값을 이용하여 비교할 수 있을까요?
- hashCode()를 오버라이드 하면 해결할 수 있다.
- HashSet에 데이터를 추가할 때 재정의된 hashCode()를 호출하며 결과값을 재정의된 equals()로 비교한다.

```java
@Override
public int hashCode() {
    return this.id;
}
```