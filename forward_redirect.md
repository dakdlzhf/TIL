## `Redirect`

* 웹 컨테이너는 sendRedirect() 메소드가 호출되면 브라우저에 응답을 보낸다
* 브라우저에서 웹 컨테이너의 응답을 받은후 새로운 요청을 하기때문에 요청속성으로 저장되어있는 setAttribute 객체는 소멸된다
* 예를들어 a.jsp 에서 request 객체에 setAttribute 속성값 ,데이터를 담아서 리다이렉트로 b.jsp 로 전달해도 받을수없다
* 추가적으로 발생한 왕복처리 때문에 forward 보다 느리며, URL 에 파라미터가 보임으로 중요한 정보를 담아서 보내지 않길 권장함.



## `Forward`

* forward 를 사용하면 다른자원으로 (jsp,servlet) 요청을 보내어 처리해도 클라이언트에는 이사실을 알리지않는다 ( 웹 컨테이너 내에서 처리한다)
* 클라이언트와 통신 없이 **<u>웹 컨테이너 내에서만 처리</u> **되기때문에 Redirect 보다 빠르다.
* forward 후에도 Request 객체에 속성값 ,데이터를 꺼내사용할수있다 .
* URL 변화가 없음으로 Client Application 이 일치하지 않을수 있다.
* **<u>한번의 요청으로 Request 를 여러 웹 컨테이너에서 데이터를 공유해야할때</u>** ( 인증처리,권한부여 처리등 ) 사용한다.

