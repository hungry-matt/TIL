# Exception ?
- 프로그래밍에서 예외란 `입력 값에 대한 처리가 불가능`하거나, 프로그램 실행중에 `참조된 값이 잘못된 경우` 등 `정상적인 흐름에서 어긋난 것`을 말함.
- java 에서는 `개발자가` 직접 예외 상항을 `미리 예측하여 핸들링 할 수 있음`.

## Checked Exception vs Unchecked Exception
간단하게 `RuntimeException`을 `상속하지 않은 클래스는 CheckedException`, 반대로 `상속한 클래스는 Unchecked Exception`으로 분류.

구분 | Checked Exception | Unchecked Exception
---|---|---
처리 여부 | 반드시 예외를 처리 | 예외 처리를 강제하지 않음
확인 시점 | 컴파일 단계 | 실행(Runtime) 단계
예외 발생시 트랜잭션 처리 | Roll-Back 하지 않음 | Roll-Back 함
예외 종류 | RuntimeException을 제외한 모든 예외(IOException, ClassNotFountException 등) | RuntimeException 하위 예외(NullPointerException, ClassCastException 등)

## 참고
- [자바 예외 구분](https://madplay.github.io/post/java-checked-unchecked-exceptions)