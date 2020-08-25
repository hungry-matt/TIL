# Comparable 

정렬에 앞서 리스트 속 데이터 간 크기 비교가 가능 해야 한다.

즉, 리스트 안에 들어 있는 오브젝트의 수치화가 가능해야 한다는 것이다.

그래서 Comparable 를 구현(implements) 한다.

이 인터페이스 안에는 int compareTo(T a) 라는 단 하나의 interface 메소드만 존재 한다.

이 메소드는 아래와 같이 리턴값을 3가지로 분류 하고 있다.

- parameter 보다 작은 경우 음수를 리턴
- parameter 와 같은 경우 0을 리턴
- parameter 보다 클 경우 정수를 리턴

~~~
내림차순 
ex) return (x < y) ? -1 : (x == y) ? 0 : 1;
~~~

```java
List<String> list = new ArrayList();
list.sort(new Comparator<String>() {
    @Override
    public int compare(String o1, String o2) {
        int x = Integer.parseInt(o1);
        int y = Integer.parseInt(o2);

        return (x < y) ? -1 : (x == y) ? 0 : 1;
    }
})
```
