## HTTP REQUEST METHOD

* 클라이언트에서 서버로 요청 시 데이터 전달 방식
  * GET 방식 - 요청 URL 에 데이터를 붙여서 전송(얻기)
    * 요청 URL 길이에 제한이 있다.
    * 전송 데이터 노출에 따른 위험이 있다.
  * POST 방식 - HTTP body 에 데이터를 담아서 전송(보내기)
    * 데이터 전송 길이에 대한 제한이 없음 (네트워크 트래픽이 많아질뿐 )
    * HTTP REQUEST BODY에 데이터를 담으므로 노출 안됨 (보안성이랑은 아무상관없다 body 에 담아서보내도 정보를 빼낼수도 있다,  안보화가가능한 프로토콜이 추가되어야만한다 http+ssl = https 443번포트 )



### :star:HTTP format 은 request(요청) 과 response( 응답 ) 을 할때도 

### 	header 와 body 구조로 이루워진다



* **request 요청정보**

  HTTP REQUEST HEADER 

  * `header` 

    * GET 방식의 요청 에관련된 내용을 header 에 담는다.

    * 서버에 보낼때 경로뒤에 데이터를 붙여서 전달.

      1) 요청

      2) Accept

      3) Referer

      4) Accept-Language

      5) User-Agent

      6) Accept-Encoding

      7) Host

      8) DNT

      9) COnnection

      10) Cookie 

          

  HTTP REQUEST BODY 

  * `body`
    * POST 방식 요청 이라면 body 에 보내는 정보를 담아서 전송

* **response 응답정보** 

  * `header` 

    * 응답 코드 status (200, 404 , 500 등등)
    * 브라우저에 응답해줄 추가적인 내용들을 포함해서 표시

    1) 요청
    2) Accept
    3) Referer
    4) Accept-Language
    5) User-Agent
    6) Accept-Encoding
    7) Host
    8) DNT
    9) COnnection
    10) Cookie 

  * `body`
    * html ,text 등 브라우저에 표시될 데이터 내용

:arrow_up_small:  ***위 형식에 맞춰서 클라이언트와 서버가 요청을 주고 받는다는 개념!***

:heavy_exclamation_mark: 클라이언트에서 서버로 요청시 서버로 전달되는 데이터를 `parameter` 라고 한다.

:heavy_exclamation_mark: 서버에서는 클라이언트의 요청으로 전달받은 `parameter` 를 꺼내서 처리 한후 클라이언트에게 `html` 을 응답한다

* ​	내장객체 (request , response , sesstion 등)
