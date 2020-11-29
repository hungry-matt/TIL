# Goal
```
- Sync, Async에 대해 이해하고 설명해보자.
- Blocking, Non-Blocking에 대해 이해하고 설명해보자.
- CompletableFuture에 대해 이해하고 설명해보자.
```
## 들어가며
CompletableFuture에 대해서 공부하기 전 Sync(동기), Async(비동기)와 Blocking, Non-Blocking에 대해서 먼저 알아보자.

## Synchronous (동기), Asynchronous(비동기)
- `호출된 함수`의 수행 결과 및 종료를 `호출한 함수가`가(`호출된 함수`뿐 아니라 `호출한 함수`도 함께) 신경쓰면 Synchronous
(요청자가 요청한 내용의 처리를 기다리면 Synchronous?)
- `호출된 함수`의 수행 결과 및 종료를 `호출된 함수` 혼자 직접 신경 쓰고 처리한다면 Asynchronous

## Blocking / Non-blocking
- 행위자가 취한 행위 자체가, 또는 그 행위로 인해 다른 무엇이 막혀버린, 제한된, 대기 하는 상태.
- `호출된 함수`가 자신이 할 일을 모두 마칠 때까지 제어권을 계속 가지고서 `호출한 함수` 에게 바로 돌려주지 않으면 Block.
- `호출된 함수`가 자신이 할 일을 채 마치지 않았더라도 바로 제어권을 건네주어(return) `호출한 함수`가 다른 일을 진행할 수 있도록 해주면 Non-block.

### 참고
- [Sync, Async](https://musma.github.io/2019/04/17/blocking-and-synchronous.html)
- [CompletableFuture - 초급](https://brunch.co.kr/@springboot/267#comment)
- [코드 베이스 - 중급](https://www.hungrydiver.co.kr/bbs/detail/develop?id=2)
- [람다식 활용 - 고급](https://m.blog.naver.com/2feelus/220714398973)
