# :star2:Cookie

* Cookie : 쿠키는 서버에서 생성해서 브라우저에게 응답에 포함시켜 준다
  * Cookie 의 생성과정
    1) 브라우저에서 서버로 자원을 요청
    2) 서버에서 쿠키 생성 및 응답에 포함시켜 준다
    3) 브라우저는 응답받은 쿠키를 저장소에 저장
    4) 해당 사이트로 요청시 쿠키를 포함해서 전송
    5) 요청에서(Request Header ) cookie 정보를 확인할수있다.

:star:  makeCookie.jsp ( 쿠키 생성)

```jsp
<%
	
Cookie cookie1 = new Cookie("name", "HGD");
Cookie cookie2 = new Cookie("age", "20");

//서버콘솔로 확인해본다.
System.out.println("name: "+ cookie1.getValue());
System.out.println("age: "+ cookie2.getValue()); 

//응답에 cookie 를 포함시킨다.
response.addCookie(cookie1); 
response.addCookie(cookie2);
	
%>
```



:star:  viewCookie.jsp ( 쿠키 보기 )

```jsp
<body>
	<h2>쿠키 목록</h2>
	<%
	Cookie[] cookies = request.getCookies(); //배열로 반환
		for (Cookie cookie : cookies) {
	%>
    
    <!-- 표현식 -->
	<%=cookie.getName()%> : <%= cookie.getValue() %><br>
    
	<%
		}
	%>

</body>
```



브라우저HTML

```html
쿠키 목록
name : HGD
age : 20
JSESSIONID : 6F9BBBB7438AD5F25F1C7FD4CB02BEAC
```



:star: modifyCookie.jsp (쿠키 수정)

```jsp
<%
	/*
		쿠키의 값을 수정
		해당쿠키의 이름을 찾아서 값을 변경해주면된다
	*/
	Cookie[] cookies = request.getCookies();
	if (cookies != null && cookies.length > 0) {
		for (int i = 0; i < cookies.length; i++) {
			if (cookies[i].getName().equals("name")) {
		Cookie cookie = new Cookie("name", "KKA");
		response.addCookie(cookie);
			}
		}
	}
	%>
```



:star: deleteCookie.jsp (쿠키 삭제)

```jsp
	<%
	Cookie[] cookies = request.getCookies();
	if (cookies != null && cookies.length > 0) {
		for (int i = 0; i < cookies.length; i++) {
			if (cookies[i].getName().equals("name")) {
		Cookie cookie = new Cookie("name", ""); //name 의 (key) 같으면 값이 대체된다 여기서  값을 비워버리는거랑은 상관없고,
		cookie.setMaxAge(0); // cookie 에 유지시간은 0 으로 주고
		response.addCookie(cookie); // 그쿠키를 브라우저의 response 에 추가하면 브라우저에서 삭제 된다.
			}
		}
	}
	%>
```



:star2: 브라우저의 저장소  => 개발자도구에 Application => Storage => 쿠키 에서 확인할수 있다.

​	요청 경로 는localhost:8080/jspEx/cookie/makeCookie.jsp 인데, 이 cookie 정보는

​	localhost:8080/jspEx/cookie 이후의 주소에는 cookie 정보를 제공한다. 

​	만약 www.naver.com 같이 완전히 다른주소라면 cookie 정보는 확인할수 없게된다 .

* 쿠기의 구성요소
  * 이름 : 쿠키 이름
  * 값 :이름에 연결된값
  * 유효시간 : 초단위 시간,날짜를 지정해도가능 ( 설정하면 해당시간동안 유지,설정하지않는다면 세션이유지하는동안만 유지) 
    * ***브라우저를 닫기전까지!!***
  * 도메인 : 쿠키를 생선한 사이트
  * 경로 :  쿠키를 전송할 요청 URL ( 일반적으로 최상위 경로 Context Path  하위 경로까지 )



:heavy_exclamation_mark: 쿠키에 최대크기도 제한이되어있고, 데이터를 문자열로 바꿔서 저장된다.

​	
***
## :star: Cookie 유효시간설정

cookie 를 생성하고 cookie 에 유효시간을 설정해보자

쿠키는 유효시간이 지나면 다시 사용되지 못하며, 브라우저에 저장되는 쿠키는 유효시간이 존재한다.

쿠키의 유효 시간을 따로 설정하지않는다면 '세션 쿠키' 라고 불려지는데 브라우저를 닫기전까지 유지가된다.

하지만 쿠키의 유효시간을 따로 설정한다면 설정한 시간만큼은 브라우저를 닫더라도 유지가된다.



```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
    
    
<%
	Cookie cookie3 = new Cookie("oneH","oneH");
	cookie3.setMaxAge(60*60); 
	response.addCookie(cookie3);
%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>유효시간이 지정된 쿠키 생성</title>
</head>
<body>
유효시간이 1시간 짜리 쿠키 생성
</body>
</html>
```

