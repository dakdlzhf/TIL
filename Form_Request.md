## :rocket: Form 태그에 입력된 값과 정보를 확인해보자



###	HTTP 프로토콜 을 이용하여 요청하고 서버에서 처리하는 과정

* 클라이언트에서 서버에 요청을 하고 -> 톰캣 서버에서 요청을 처리할때  request 객체의 함수를 몇가지 알아보자

  * form.jsp 파일 ( 브라우저에서 form 태그에 입력한다면  )

    ```javascript  
    <body>
    	<form action="requestParameter.jsp">
    		<input type="text" name="name" placeholder="문자열 입력">
    		<input type="submit" value="전송">
    	</form>
    </body>
    
    ```

  * requestParameter.jsp 파일 

  ```javascript
  
  <body>
  
      클라이언트IP : <%= request.getRemoteAddr() %><br>
  	요청정보 길이 : <%= request.getContentLength() %><br>
  	요청정보 인코딩 : <%= request.getCharacterEncoding() %><br>
  	요청 정보 문서타입 : <%= request.getContentType() %><br>
  	요청 정보 전송 방식: <%= request.getMethod() %><br>
  	요청 URL : <%= request.getRequestURL() %><br>
  	요청 URI : <%= request.getRequestURI() %><br>
  	컨텍스트 경로 : <%= request.getContextPath() %><br>
  	서버이름 : <%= request.getServerName() %><br>
  	서버포트 : <%= request.getServerPort() %><br>
  
  </body>
  ```

requestParameter.jsp  에 요청이 들어오면 request 객체에 정보를 을 꺼내사용할수있는데,

위에 코드와 같이 ip 주소 인코딩,전송방식 URL 등 의 정보를 확인해볼수있다.



* 만약 form 에 데이터를 입력하고 입력한 값을 꺼내사용할때 한글이 깨진다면 ( 알수없는 문자로 표시되면 인코딩 문제 이다)
  * <% %> 스크립트릿 안에서 request.setCharacterEncoding("utf-8"); 설정을해주면

 			request 객체안에 저장되는 데이터들을 한글로 바꿔서 보여준다.

* form 태그안에 input 태그 name 을 설정해야 <% %> 스크립트 안에서 꺼내 사용할수있는데,

  * String name = request.getParameter(" adress ");

    ```javascript
    <%
      String address = request.getParameter(" address ");
    %>
    <body>
    제 주소는 <%= address %> 입니다
    
    </body>
    ```

    

* input 속성의 name 중 address 라는 name 을 갖고있는 input 의 데이터를 String address 에 담아 표현식으로 사용한것이다.

