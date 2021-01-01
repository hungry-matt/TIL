# Authentication 관련 클래스와 처리

## 인증과 인가란?
- 인증 : 사용자가 본인이 맞는지 확인하는 절차
- 인가 : 인증된 사용자가 요청된 자원에 접근 가능한지 결정하는 절차

## 인증 방식
1. credential 기반 인증 : 사용자명과 비밀번호를 이용한 방식
2. 이중 인증(two factor 인증) : 사용자가 입력한 개인 정보를 인증 후, 다른 인증 체계(예:물리적인 카드)를 이용하여 두가지의 조합으로 인증하는 방식
3. 하드웨어 인증 : 자동차 키와 같은 방식

이중 Spring Security는 credential 기반의 인증을 취함
- principal : 아이디
- credential : 비밀번호

## Spring Security 주요 모듈

### SecurityContextHolder, SecurityContext, Authentication
- 세가지 클래스는 Spring Security에서 주요 컴포넌트임.
- 아이디/패스워드를 가진 사용자 정보가 인증에 성공하면 principal과 credential 정보를 Authentication에 담음.
```
Authentication(pricipal, credential)
```

- Spring Security에서 Authentication의 정보를 SecurityContext에 보관함.
```
SecurityContext(Authentication(pricipal, credential))
```

- 이 SecurityContext를 SecurityContextHolder에 담아 보관함.
```
SecurityContextHolder(SecurityContext(Authentication(pricipal, credential)))
```

## Spring Security에서 인증 처리
1. username과 password를 조합해서 UsernamePasswordAuthenticationToken 인스턴스를 만듬.
2. 이 토큰(UsernamePasswordAuthenticationToken)은 검증을 위해 AuthenticationManager의 인스턴스로 전달.
3. AuthenticationManager는 인증에 성공하면 Authentication 인스턴스를 리턴.
4. 이 Authentication을 SecurityContextHolder.getContext().setAuthentication(...)를 set 해줌.

### 로그인한 사용자 정보 얻기
```java
Object principal = SecurityContextHolder().getContext().getAuthentication().getPrincipal();

if (priciapl instanceof UserDetails) {
    String username = ((UserDateils)principal).getUserName();
} else {
    String username = principal.toString();
}
```

### 참고
- [Authentication](https://flyburi.com/584)
