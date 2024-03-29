# 유의적 버전 (Semantic Versioning)

### 요약
- 소프트웨어의 특정 시점의 상태에 대해 식별 하기 위한 이름을 의미

~~~
소프트웨어 버전이란 컴퓨터 소프트웨어의 특정 시점의 상태에 대해 식별 가능한 유일한 이름을 지정하는 것을 의미합니다.

개발하는 소프트웨어의 규모가 커지고 외부 라이브러리를 많이 사용할 수록 의존성 지옥에 빠지기 쉬운 이유중 하나는 
라이브버리의 버전을 변경할 때 어떤 규칙에 의해서 버전이 매겨지는지 통용되는 명확한 규칙이 없기 때문 입니다.

유의적 버전은 이런 의존성 문제를 해결하고자 나온 라이브러리의 버전 명시 규칙과 요구 사항으로 요약하면 다음과 같습니다.
~~~

- 기존 버전과 호환되지 않게 API가 변경되면 "MAJOR 버전"을 올린다.
- 기존 버전과 호환되면서 새로운 기능이 추가 되었을 때는 "MINOR 버전"을 올린다.
- 기존 버전과 호환되면서 버그를 수정했을 경우 "PATCH 버전"을 올린다.
- 버전 형식 뒤에 "정신 출시전" 이나 빌드 메타데이타를 위한 레이블을 추가할 수 있다.

예로 lib-bar의 버전이 2.1.1 일 경우 API가 호환되지 않는 새 버전은 3.y.z 가 됩니다. (y.z 는 숫자)

## 기억해 둘 사항들
- 최초 개발 배포 버전을 0.1.0 으로 한다.
- 자릿수를 맞추기 위해 0으로 시작하는 숫자를 쓰지 않도록 한다.
    - 예를 들어 2.07.1 은 좋지 않다. 2.7.1 을 쓰도록 하자.
- 부모 버전이 오르면 자식 버전은 0 으로 초기화 한다.
    - MAJOR 버전이 오르면 MINOR와 PATCH 버전은 0으로 초기화 한다.
    - MINOR 버전이 오르면 PATCH 버전은 0으로 초기화 한다.
