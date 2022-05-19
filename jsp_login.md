# :star:login 동작 만들어보기

**간단한 login 동작을 만들어보겠습니다**

1) form 을 입력받는 loginForm.jsp 와 로그인 로직을 처리하는 loginProc.jsp 를 만든다
2) 요청에서 파라미터를 가져온다
3) 아이디와 비밀번호가 같으면 로그인성공으로 처리하며, DB 가없기때문에 일단 아이디와 패스워드를 동일하게 만든다.
4) 아이디 기억하기 checkbox 에 체크가되었다면 쿠키를 1시간짜리 생성한다
5) 아이디와 비밀번호가 같지않는다면 redirect 로 loginForm.jsp 로 돌려보낸다
6) 로그인 페이지에 remember 쿠키 ( checkbox ) 의 값이 존재한다면 checkbox 를 체크상태로 보여지도록 하고 loginForm.jsp 수정
7) 기억된 아이디가 userid텍스트 상자에 표시 되어야 한다.

***

:rocket:시작해보자!!!



 `loginForm.jsp` 

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<form action="loginProc.jsp" method="post">
		<input type="text" name="userid" placeholder="아이디" /><br> 
		<input type="text" name="userpw" placeholder="패스워드" /><br> 
		아이디 기억하기 <input type="checkbox" name="remember" value="chk" /><br> 
		<input type="submit" value="로그인" />
	</form>
</body>
</html>
```



`loginProc.jsp`

```jsp
<%@page import="java.io.PrintWriter"%>
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>

<%
String userid = request.getParameter("userid");
String userpw = request.getParameter("userpw");
String remember = request.getParameter("remember");
PrintWriter writer = response.getWriter();
	
if (userid.equals(userpw)) {

	System.out.println("login 성공");
	if (remember != null) {
		System.out.println("쿠키생성");
		Cookie rememberCookie = new Cookie("remember", userid);
		rememberCookie.setMaxAge(60 * 60);
		response.addCookie(rememberCookie);

		response.sendRedirect("loginForm.jsp"); //아이디 기억 checkbox 가 체크된걸 확인하기위해
	} else {
		System.out.println("쿠키없음");
		Cookie rememberCookie = new Cookie("remember", userid);
		rememberCookie.setMaxAge(0);
		response.addCookie(rememberCookie);
	}
} else {
	 // java 단에서 alert 를 사용하려면 PrintWriter 사용해서 script 를 아래처럼 생성해 주면된다.
	writer.println("<script type='text/javascript'>");
	writer.println("alert('비밀번호가 일치하지않습니다.');");
	writer.println("history.back()");
	writer.println("</script>");
	writer.flush(); //flush()는 현재 버퍼에 저장되어 있는 내용을 클라이언트로 전송하고 버퍼를 비운다. (JSP)
	response.sendRedirect("loginForm.jsp");
}
%>

<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>로그인 여부</title>
</head>
<body>
	userid :
	<%=userid%>
	, userpw :
	<%=userpw%>
</body>
</html>
```

***

:star2: 완성

**개발자도구를 열어서 Network 와 Application 을 확인해 보면서 개념을 파악해보았다. 아직 DB 를 연동한것은아니라서 간단하게 만들어봤지만 ㅜㅜ 앞으로 좀더 배워가며 다양한 기능들과 리팩토링  + DB 를 연동한 것을 기록해 나아가겠다.**

