# branch?
독립으로 어떤 작업을 진행하기 위한 개념 입니다.

다른 브랜치의 영향을 받지 않기 때문에 여러 작업을 동시에 진행할 수 있습니다.

## branch 생성
-b 옵션을 추가 하여 branch를 생성할 수 있다.
```
//생성되어 있는 branch checkout
$ git checkout main

//barnch 생성
$ git checkout -b main#1_test

//생성된 branch를 원격저장소에 push하여 추가
$ git push origin main#1_test

```

## branch 삭제
-d 옵션을 추가 하여 barnch를 삭제할 수 있다.

```
//생성되어 있는 branch checkout
$ git checkout main

//branch 삭제
$ git branch -d main#2

//원격 리모트 branch 삭제
$ git push origin :main#2
```