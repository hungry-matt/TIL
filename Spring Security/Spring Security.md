# Spring Security
- 단순 인증/권한처리만 하는게 아닌 CSRF 같은 보안 이슈도 Security에서 처리 가능
- OAuth2.0 등을 지원하여 다양한 방법의 로그인들을 지원
- 권한을 URI 기준으로 처리하여, 인증방법이 바뀌거나 추가되어도 인증 외에는 변경되지 않는 장점이 있음

## 인증 (Authentication)
인증은 참이라는 근거가 있는 무언가를 확인하거나 확증하는 행위
- 사용자의 정보를 확인하는 절차
- 보통 id, password를 통해서 서버에 요청을 하고 올바른 사용자인지 서버는 응답

## 인가 (Authorization)
인가란 리소스에 대한 접근 권한 및 정책을 지정하는 기능

## HTTP 관련 인증, 보안 설정
메소드 | 기능
---|---
permitAll() | 모든 접속 허가
hasAnyAuthority() | 해당 권한을 가진 유저만 접속 가능
anyRequest().authenticated() | 나머지 URL은 인증을 거쳐야 함
.csrf().ignoringAntMatchers("/user/save") | CSRF 토큰 없이 실행
defaultSuccessURL("/") | 로그인이 성공 되면 해당 URL로 이동
logoutRequestMatcher(new AntPathRequestMatcher("/logout")) | 해당 '/logout'을 받으면 로그아웃
.deleteCookies("JSESSIONID") | JSESSIONID 삭제
accessDeniedPage("/access-denied") | 권한이 없는 URL에 접속하려고 하면 해당 URL로 리다이렉션