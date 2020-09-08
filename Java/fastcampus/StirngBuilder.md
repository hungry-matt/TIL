# StringBuilder
String은 소위 불변객체라고 한다.
String str1 , String str2를 더하게 되면 새로운 String 객체를 만든다.
즉, 객체끼리 더하는 연산을 했을때 메모리 할당과 해제를 하게 되며 더하는 연산이 많을 수록 부하가 오게 된다.
이런 문제를 해결하기 위해 StringBuilder를 사용하여 String과 같이 객체를 새로 생성하지 않고 기존 데이터에 연산을 처리하여 상대적으로 속도도 빠르고 부하가 적다.
