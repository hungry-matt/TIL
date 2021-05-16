# su(substitute user)
> substitute : 명) 대리자, 대체물 , 동) 대체하다
- 로그아웃하지 않고 다른 사용자의 권한으로 쉘을 실행하는 데 사용된다.
- 같은 방법으로 다른 사용자로 전환하는 데 사용된다.
- 어떤 사용자의 권한으로 실행할지 정하지 않고 실행한 경우에는, 루트 사용자로 간주된다.

## 사용법
사용자의 비밀번호를 묻고, 제대로 입력했다면 해당 계정과 연관된 모든 파일에 대한 접근 권한이 부여된다.
```
[user@test ~]$ su
Password:
[root@test home]#
```

또한, 루트 사용자가 아닌 다른 사용자로 전환할 수 있다.
```
[user@test ~]$ su user2
Password:
[user2@test home]$
```

> su 뒤에 '-'을 붙이면 동작방식이 달라진다. 
'-'은 '-l' 혹은 '--login'과 동일한 명령어이다.

> su 명령어는 현재 계정의 환경변수들을 유지한채 대상 계정으로 전환하고 su - 명령어는 대상 계정의 환경변수까지 전환하는 차이가 있다.

# sudo
- 명칭은 본래 "superuser do"에서 유래하였으나, 후에 프로그램의 기능이 확장되며 "substitute user do"(다른 사용자의 권한으로 실행)의 줄임말로 해석되게 되었다.
- 일반 사용자가 root 권한을 빌려 실행할 수 있다.

## 사용법
```
[user@test ~]$ sudo yum install git
```

# References
- [su](https://ko.wikipedia.org/wiki/Su_(%EC%9C%A0%EB%8B%89%EC%8A%A4))

- [sudo](https://ko.wikipedia.org/wiki/Sudo)