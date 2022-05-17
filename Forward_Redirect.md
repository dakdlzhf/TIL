## :rocket: Forward & Redirect

## ***:star2: 서버내에서 처리할 페이지를 연결해주는 작업  = 포워딩 :star2:***

* FORWARD 동작 방식

  `main.jsp`

  ```jsp
  <form action="forward.jsp" method="get">
  		이름: <input type="text" name="name" /><br>
  		나이: <input type="text" name="age" />
  		<input type="submit" value="포워딩요청" />
  	</form>
  	
  	<hr></hr>
  	
  	<form action="redirect.jsp" method="get">
  		이름: <input type="text" name="name"/><br>
  		나이: <input type="text" name="age" />
  		<input type="submit" value="리디렉트요청" />
  </form>
  ```

  `forward.jsp`

  ```jsp
  <%@ page language="java" contentType="text/html; charset=UTF-8"
      pageEncoding="UTF-8"%>
  <%
  	String name = request.getParameter("name");
  	String age = request.getParameter("age");
  	System.out.println("forward.jsp에서 request파라미터 확인");
  	System.out.println("이름 : "+ name);
  	System.out.println("나이 : "+ age);
  	System.out.println("forward_ret으로 요청을 전달");
  	RequestDispatcher dispatcher = request.getRequestDispatcher("forward_ret.jsp");
  	
  	//브라우저에서 요청이들어오면 request 객체와 response 객체가 기본으로 생성되는데 그생성된 객체들을 포워딩하여 그대로 forward_ret.jsp 로 넘겨준다.
  	//forward_ret.jsp 를 요청한 것처럼 그대로 객체를 유지해서 전달 
  	//요청된 URL 도 변경되지않는다. 현재 URL 은 ( locallhost:8080/contextpath/forward.jsp )
  	dispatcher.forward(request,response);
  	
  	//forward_ret.jsp 로 요청을 전달
  %>
  ```

  `forward_ret.jsp`

  ```jsp
  <%@ page language="java" contentType="text/html; charset=UTF-8"
      pageEncoding="UTF-8"%>
      
  <%
  	//서버에 전달된 parameter 를 꺼낸다. 
  	String name = request.getParameter("name");
  	String age = request.getParameter("age");
  	
  %>
  <!DOCTYPE html>
  <html>
  <head>
  <meta charset="UTF-8">
  <title>Insert title here</title>
  </head>
  <body>
  포워드 결과입니다.<br>
  요청 URL 부분이 변경되지 않고 request 객체도 유지됩니다.<br>
  <hr></hr>
  
  <!-- 표현식 -->
  <%="forward_ret.jsp 에서 request 파라미터 확인" %><br>
  <%= "이름" + name %><br>
  <%= "나이" + age %>
  
  </body>
  </html>
  ```



:star: 브라우저에 요청은 forward.jsp 이지만 `disfatcher.forward()` 를 통해 객체를 forward_ret.jsp 경로로 모두 전달하는 과정 인데

 서버는 forward.jsp 와 forward_ret.jsp 의 처리를 모두 하였다.



**:100: Forward 요약**

* 요청 전달 처리
  * 요청을 구분하여 처리할 서블릿을 결정하는 경우
  * f처리를 여러 단계의 서블릿으로 구분하여 필요한 단계로 바로 이동하는 경우
  * 브라우저에 표시되는 경로를 숨기고 싶은 경우
  * 요청시 생성된 requset,response 객체의 값을 유지할경우



***



* REDIRECT 동작 방식

`main.jsp`

```jsp
	<form action="forward.jsp" method="get">
		이름: <input type="text" name="name" /><br>
		나이: <input type="text" name="age" />
		<input type="submit" value="포워딩요청" />
	</form>
	
	<hr></hr>
	
	<form action="redirect.jsp" method="get">
		이름: <input type="text" name="name"/><br>
		나이: <input type="text" name="age" />
		<input type="submit" value="리디렉트요청" />
	</form>
```

`redirect.jsp`

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
    
<%
	String name = request.getParameter("name");
	String age = request.getParameter("age");
	System.out.println("redirect.jsp에서 request 파라미터 확인");
	System.out.println("이름 : "+ name);
	System.out.println("나이 : "+ age);
	System.out.println("redirect_ret 으로 다시 요청하라고 응답해줌");
	response.sendRedirect("redirect_ret.jsp");
	
%>
```

`redirect_ret.jsp`

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
    
<%
	String name = request.getParameter("name");
	String age = request.getParameter("age");
%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
리디렉트 결과 <br>
브라우저에서 새로 요청한 것이므로<br>
요청 URL 부분이 변경되고 request 객체도 새로 생성된다. (값 유지가 안된다)<br>

<%= "redirect_ret.jsp 에서 request 파라미터 확인" %><br>
<%= "이름 : " + name %><br>
<%= "나이 : " + age %>
</body>
</html>

```



:star:리디렉트는  redirect.jsp 에서 `response`객체의 ` sendRedirect()` 를 사용하여 브라우저에서 **<u>새로운 요청을 함</u>**



**:100: redirect 요약**

* 다시요청
  * 요청을 검증 하여 알맞은 페이지로 요청을 하도록 처리하려는 경우에사용
  * 에러 또는 예외 처리에 대한 결과 페이지를 처리하려는 경우
  * 브라우저 주소 창에 경로가 표시됨(redirect 페이지 경로로 표시)
  * 새로운 요청이므로 request, response 객체는 새로 생성
