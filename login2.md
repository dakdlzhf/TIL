# π― login λμ λ§λ€μ΄λ³΄κΈ° 2ν



μ λ²μλ μΏ ν€λ₯Όν΅ν΄ μμ΄λλ₯Ό μ μ₯νκ³  μμ΄λμ²΄ν¬κ° form μ μλ ₯λκ²νμλ€.

μ΄λ² μκ°μ session κΉμ§ μ¬μ©νμ¬ login λ§λ€μ΄λ³΄κΈ° 2νμ μμνκ² λ€.



μ°μ  μ λ² μ½λμ session κΈ°λ₯μ μΆκ°νμ½λλ₯Ό λ³΄κ² λ€.



:star: loginForm.jsp

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%

	String loginId = (String)session.getAttribute("loginId"); //κ°μ²΄λ₯Ό λ°ννκΈ°λλ¬Έμ νλ³ν
	
	if(loginId !=null){
		System.out.println("λ‘κ·ΈμΈ λμ΄μλμν");
		response.sendRedirect("loginSuccess.jsp");
	}else{
		
	
	
	String userid = ""; //null λ‘ νλ©΄ userid μΈν νκ·Έμ null μ΄ λμ€κΈ°λλ¬Έμ ""; λΉλ¬Έμμ΄μ λ£μ΄μ€
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
		<input type="text" name="userid" placeholder="μμ΄λ" value="<%= userid %>" /><br> 
		<input type="text" name="userpw" placeholder="ν¨μ€μλ" /><br> 
		μμ΄λ κΈ°μ΅νκΈ° <input type="checkbox" name="remember" value="chk" <%= checked %>/><br> 
		<input type="submit" value="λ‘κ·ΈμΈ" />
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
	System.out.println("λ‘κ·ΈμΈ λμ΄ μλ μν");
	response.sendRedirect("loginSuccess.jsp");
}else{
	



String userid = request.getParameter("userid");
String userpw = request.getParameter("userpw");
String remember = request.getParameter("remember");
PrintWriter writer = response.getWriter();
	
if (userid.equals(userpw)) {
	System.out.println("login μ±κ³΅");

	session.setAttribute("loginId", userid);
		if (remember != null) {
		System.out.println("μΏ ν€μμ±");
		Cookie rememberCookie = new Cookie("remember", userid);
		rememberCookie.setMaxAge(60 * 60);
		response.addCookie(rememberCookie);

		response.sendRedirect("loginForm.jsp"); //μμ΄λ κΈ°μ΅ checkbox κ° μ²΄ν¬λκ±Έ νμΈνκΈ°μν΄
	} else {
		System.out.println("μΏ ν€μμ");
		Cookie rememberCookie = new Cookie("remember", userid);
		rememberCookie.setMaxAge(0);
		response.addCookie(rememberCookie);
	}
	response.sendRedirect("loginSuccess.jsp");
} else {
	
	writer.println("<script type='text/javascript'>");
	writer.println("alert('λΉλ°λ²νΈκ° μΌμΉνμ§μμ΅λλ€.');");
	writer.println("history.back()");
	writer.println("</script>");
	writer.flush(); //flush()λ νμ¬ λ²νΌμ μ μ₯λμ΄ μλ λ΄μ©μ ν΄λΌμ΄μΈνΈλ‘ μ μ‘νκ³  λ²νΌλ₯Ό λΉμ΄λ€. (JSP)
	response.sendRedirect("loginForm.jsp");
}
%>

<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>λ‘κ·ΈμΈ μ¬λΆ</title>
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
<title>λ‘κ·ΈμΈ μ±κ³΅</title>
</head>
<body>
<%= session.getAttribute("loginId") %> λ λ‘κ·ΈμΈ μ±κ³΅!
<a href="logout.jsp"><button>λ‘κ·Έμμ</button></a>
</body>
</html>	
```



:star: loginout.jsp

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%
	
	System.out.println(session.getAttribute("loginId") + "λκ»μ λ‘κ·ΈμΈ μμνμ¨μ΅λλ€");
	session.invalidate(); //session λ¬΄ν¨ν
	response.sendRedirect("loginForm.jsp");
%>
```

