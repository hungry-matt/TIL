# pageContext (javax.servlet.jsp.PageContext)
- pageContext 객체는 jsp 기본 내장 객체
- pageContext는 jsp 페이지에 대해 1:1로 연결된 객체로 jsp 페이지당 하나의 pageContext 객체가 생성됨

메서드 | 반환타입 | 설명
---|---|---
getRequest() | ServletRequest | request 기본 객체를 반환
getResponse() | ServletResponse | response 기본 객체를 반환
getSession() | HttpSession | session 기본 객체를 반환
getServletContext() | ServletContext | application 기본 객체를 반환
getOut() | JspWriter | out 기본 객체 반환
getException() | Exception | exception 기본 객체 반환
getPage() | Object | page 기본 객체 반환

## <c:url>
<c:url> 태그는 URL에 자동으로 Context Path를 붙여준다. 컨텍스트를 변경하더라도 URL을 수정할 필요가 없게 된다.
