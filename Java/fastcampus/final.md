# final
- final 변수는 값이 변경될 수 없는 상수임. (오직 한번만 값을 할당할 수 있음)
- final 메서드는 하위 클래스에서 재정의 할 수 없음.
- final 클래스는 더 이상 상속 되지 않음. ex) String 클래스
- 프로젝트 구현시 여러 파일에서 공유해야 하는 상수 값은 하나의 파일에 선언하여 사용하면 편리.

~~~java
public class Define {
    public static final int min = 1;
    public static final int max = 99999;
    public static final double PI = 3.14;
}
~~~