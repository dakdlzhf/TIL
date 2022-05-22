# 🔯 login 동작 만들어보기 2탄



저번에는 쿠키를통해 아이디를 저장하고 아이디체크가 form 에 입력되게하였다.

이번 시간은 session 까지 사용하여 login 만들어보기 2탄을 시작하겠다.



우선 저번 코드에 session 기능을 추가한코드를 보겠다.



:star: loginForm.jsp

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%

	String loginId = (String)session.getAttribute("loginId"); //객체를 반환하기때문에 형변환
	
	if(loginId !=null){
		System.out.println("로그인 되어있는상태");
		response.sendRedirect("loginSuccess.jsp");
	}else{
		
	
	
	String userid = ""; //null 로 하면 userid 인풋 태그에 null 이 나오기때문에 ""; 빈문자열을 넣어줌
	String checked = ""; 
	Cookie[] cookies = request.getCookies();
	
	if(cookies != null && cookies.length > 0){
		for(int i = 0 ; i <cookies.length ; i++){
			if(cookies[i].getName().equals("remember")){
				userid = cookies[i].getValue();
				checked ="checked";
			}
		}
	}
	
%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Insert title here</title>
</head>
<body>


<form action="loginProc.jsp" method="post">
		<input type="text" name="userid" placeholder="아이디" value="<%= userid %>" /><br> 
		<input type="text" name="userpw" placeholder="패스워드" /><br> 
		아이디 기억하기 <input type="checkbox" name="remember" value="chk" <%= checked %>/><br> 
		<input type="submit" value="로그인" />
	</form>
</body>
</html>
<% } %>
```





:star: loginProc.jsp

```jsp
<%@page import="java.io.PrintWriter"%>
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>

<%
	
String loginId = (String)session.getAttribute("loginId");
if(loginId != null){
	System.out.println("로그인 되어 있는 상태");
	response.sendRedirect("loginSuccess.jsp");
}else{
	



String userid = request.getParameter("userid");
String userpw = request.getParameter("userpw");
String remember = request.getParameter("remember");
PrintWriter writer = response.getWriter();
	
if (userid.equals(userpw)) {
	System.out.println("login 성공");

	session.setAttribute("loginId", userid);
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
	response.sendRedirect("loginSuccess.jsp");
} else {
	
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

<% } %>
```





:star: loginSuccess.jsp

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>

<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>로그인 성공</title>
</head>
<body>
<%= session.getAttribute("loginId") %> 님 로그인 성공!
<a href="logout.jsp"><button>로그아웃</button></a>
</body>
</html>	
```



:star: loginout.jsp

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%
	
	System.out.println(session.getAttribute("loginId") + "님께서 로그인 아웃하셨습니다");
	session.invalidate(); //session 무효화
	response.sendRedirect("loginForm.jsp");
%>
```

