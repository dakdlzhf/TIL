# ๐ฏ login ๋์ ๋ง๋ค์ด๋ณด๊ธฐ 1ํ

**๊ฐ๋จํ login ๋์์ ๋ง๋ค์ด๋ณด๊ฒ ์ต๋๋ค**

1) form ์ ์๋ ฅ๋ฐ๋ loginForm.jsp ์ ๋ก๊ทธ์ธ ๋ก์ง์ ์ฒ๋ฆฌํ๋ loginProc.jsp ๋ฅผ ๋ง๋ ๋ค
2) ์์ฒญ์์ ํ๋ผ๋ฏธํฐ๋ฅผ ๊ฐ์ ธ์จ๋ค
3) ์์ด๋์ ๋น๋ฐ๋ฒํธ๊ฐ ๊ฐ์ผ๋ฉด ๋ก๊ทธ์ธ์ฑ๊ณต์ผ๋ก ์ฒ๋ฆฌํ๋ฉฐ, DB ๊ฐ์๊ธฐ๋๋ฌธ์ ์ผ๋จ ์์ด๋์ ํจ์ค์๋๋ฅผ ๋์ผํ๊ฒ ๋ง๋ ๋ค.
4) ์์ด๋ ๊ธฐ์ตํ๊ธฐ checkbox ์ ์ฒดํฌ๊ฐ๋์๋ค๋ฉด ์ฟ ํค๋ฅผ 1์๊ฐ์ง๋ฆฌ ์์ฑํ๋ค
5) ์์ด๋์ ๋น๋ฐ๋ฒํธ๊ฐ ๊ฐ์ง์๋๋ค๋ฉด redirect ๋ก loginForm.jsp ๋ก ๋๋ ค๋ณด๋ธ๋ค
6) ๋ก๊ทธ์ธ ํ์ด์ง์ remember ์ฟ ํค ( checkbox ) ์ ๊ฐ์ด ์กด์ฌํ๋ค๋ฉด checkbox ๋ฅผ ์ฒดํฌ์ํ๋ก ๋ณด์ฌ์ง๋๋ก ํ๊ณ  loginForm.jsp ์์ 
7) ๊ธฐ์ต๋ ์์ด๋๊ฐ useridํ์คํธ ์์์ ํ์ ๋์ด์ผ ํ๋ค.

***

:rocket:์์ํด๋ณด์!!!



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
		<input type="text" name="userid" placeholder="์์ด๋" /><br> 
		<input type="text" name="userpw" placeholder="ํจ์ค์๋" /><br> 
		์์ด๋ ๊ธฐ์ตํ๊ธฐ <input type="checkbox" name="remember" value="chk" /><br> 
		<input type="submit" value="๋ก๊ทธ์ธ" />
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

	System.out.println("login ์ฑ๊ณต");
	if (remember != null) {
		System.out.println("์ฟ ํค์์ฑ");
		Cookie rememberCookie = new Cookie("remember", userid);
		rememberCookie.setMaxAge(60 * 60);
		response.addCookie(rememberCookie);

		response.sendRedirect("loginForm.jsp"); //์์ด๋ ๊ธฐ์ต checkbox ๊ฐ ์ฒดํฌ๋๊ฑธ ํ์ธํ๊ธฐ์ํด
	} else {
		System.out.println("์ฟ ํค์์");
		Cookie rememberCookie = new Cookie("remember", userid);
		rememberCookie.setMaxAge(0);
		response.addCookie(rememberCookie);
	}
} else {
	 // java ๋จ์์ alert ๋ฅผ ์ฌ์ฉํ๋ ค๋ฉด PrintWriter ์ฌ์ฉํด์ script ๋ฅผ ์๋์ฒ๋ผ ์์ฑํด ์ฃผ๋ฉด๋๋ค.
	writer.println("<script type='text/javascript'>");
	writer.println("alert('๋น๋ฐ๋ฒํธ๊ฐ ์ผ์นํ์ง์์ต๋๋ค.');");
	writer.println("history.back()");
	writer.println("</script>");
	writer.flush(); //flush()๋ ํ์ฌ ๋ฒํผ์ ์ ์ฅ๋์ด ์๋ ๋ด์ฉ์ ํด๋ผ์ด์ธํธ๋ก ์ ์กํ๊ณ  ๋ฒํผ๋ฅผ ๋น์ด๋ค. (JSP)
	response.sendRedirect("loginForm.jsp");
}
%>

<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>๋ก๊ทธ์ธ ์ฌ๋ถ</title>
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

:star2: ์์ฑ

**๊ฐ๋ฐ์๋๊ตฌ๋ฅผ ์ด์ด์ Network ์ Application ์ ํ์ธํด ๋ณด๋ฉด์ ๊ฐ๋์ ํ์ํด๋ณด์๋ค. ์์ง DB ๋ฅผ ์ฐ๋ํ๊ฒ์์๋๋ผ์ ๊ฐ๋จํ๊ฒ ๋ง๋ค์ด๋ดค์ง๋ง ใใ ์์ผ๋ก ์ข๋ ๋ฐฐ์๊ฐ๋ฉฐ ๋ค์ํ ๊ธฐ๋ฅ๋ค๊ณผ ๋ฆฌํฉํ ๋ง  + DB ๋ฅผ ์ฐ๋ํ ๊ฒ์ ๊ธฐ๋กํด ๋์๊ฐ๊ฒ ๋ค.**

# ๐ฏ login ๋์ ๋ง๋ค์ด๋ณด๊ธฐ 2ํ
