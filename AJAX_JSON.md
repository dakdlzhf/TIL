## :rocket: 동기처리 와 비동기처리 

### Synchronous

* **동기방식**은 설계가 매우 간단하고 직관적이지만 결과가 주어질 때까지 아무것도 못하고 대기해야 하는 단점이 있고, 
  * A 라는 일처리가 끝나야 B 처리를 할수있다.

### Asynchronous

* 비동기는 동시에 일어나지 않는다를 의미합니다. 요청과 결과가 동시에 일어나지 않을거라는 약속입니다. 
* **비동기방식**은 동기보다 복잡하지만 결과가 주어지는데 시간이 걸리더라도 그 시간 동안 다른 작업을 할 수 있으므로 자원을 효율적으로 사용할 수 있는 장점이 있습니다

- 요청한 그 자리에서 결과가 주어지지 않음
- 노드 사이의 작업 처리 단위를 동시에 맞추지 않아도 된다.
  * 만약 A , C 라는 처리는 1초가 걸리고 , B 처리하는시간은 3초가 걸린다고하면 A처리 -> C 처리 ->3초후 B 처리 완료

## XMLHttpRequest 객체 의 생성

1) XMLHttpRequest  객체는 JavaScript 에 의해 생성된다

2) XMLHttpRequest 객체는 웹 서버에 요청을 보낸다

3) 서버가 요청을 처리한다

4) 서버가 웹페이지에 응답을 보낸다

5) XMLHttpRequest 객체가 서버의 응답을 담고있다.

6) XMLHttpRequest 객체가 JavaScript 에게 전달해주고 JavaSciprt 가 응답을 읽는다

   * XMLHttpRequest 객체 안에 함수중

     * open ()  - ***:star:요청의 초기화*** , GET / POST 방식을 선택하고 접속할 URL 입력
       * open(전달방식, URL주소, 동기여부);

     * send () - 웹서버에 ***:star:요청을 전송***  한다.

       * send();    // GET 방식
       * send(문자열); // POST 방식

     * Chrome, IE7+, Firefox, Safari, and Opera 브라우저는 XMLHttpRequest를
          내장하고 있지만 코드로 확인 후 생성해도좋다

       ```javascript
       let xmlHttp;
       if(window.XMLHttpRequest){
       	xmlHttp = new XMLHttpRequest(); 
       }else{
       	xmlHttp = new ActiveXObject("Microsoft.XMLHTTP");
       }
       ```

       - 해당 브라우저가 XMLHttpRequest 객체가 있다면 생성하고
       - 해당 브라우저에 XMLHttpRequest  객체가 없다면 else 처럼  생성

## :ballot_box_with_check:  onreadystatechange Event !!

* onreadystatechange Event는 비동기 상태의 요청에 대한 응답시점을 인식시켜준다.

* onreadystatechange Event는 callback함수가 연결되어 readystate값이 변경되면
    자동으로 callback함수가 호출된다.

  ```javascript
   let xhttp;
              if (window.XMLHttpRequest) {
                  xhttp = new XMLHttpRequest();
              } else {
                  // code for IE6, IE5
                  xhttp = ActiveXObject("Microsoft.XMLHTTP");
              }
  
  xhttp.onreadystatechange = function ( 로직 ) {}
  ```

  

  

## readyState 

* readyState 프로퍼티 는 XMLHttpRequest 객체의 현재 상태를 나타내는데, 이프로퍼티가 XMLHttpRequest 의 현재 상태에 따라 아래의 주기처럼 변한다.

1) **UNSENT (숫자 0) : XMLHttpRequest 객체가 생성됨.**

2) **OPENED (숫자 1) : open() 메소드가 성공적으로 실행됨.**

3. **HEADERS_RECEIVED (숫자 2) : 모든 요청에 대한 응답이 도착함.**
   * 이때부터 응답받은 status 값이 Header 에 포함되어 온다. 

4. **LOADING (숫자 3) : 요청한 데이터를 처리 중임.**

5. **DONE (숫자 4) : 요청한 데이터의 처리가 완료되어 응답할 준비가 완료됨.**

```javascript
switch (httpRequest.readyState) {

    case XMLHttpRequest.UNSET:
        currentState += "현재 XMLHttpRequest 객체의 상태는 UNSET 입니다.<br>";
        break;

    case XMLHttpRequest.OPENED:
        currentState += "현재 XMLHttpRequest 객체의 상태는 OPENED 입니다.<br>";
        break;

    case XMLHttpRequest.HEADERS_RECIEVED:
        currentState += "현재 XMLHttpRequest 객체의 상태는 HEADERS_RECEIVED 입니다.<br>";
        break;

    case XMLHttpRequest.LOADING:
        currentState += "현재 XMLHttpRequest 객체의 상태는 LOADING 입니다.<br>";
        break;

    case XMLHttpRequest.DONE:
        currentState += "현재 XMLHttpRequest 객체의 상태는 DONE 입니다.<br>";
        break;

}
document.getElementById("status").innerHTML = currentState;
```



:star: <u> readyState 의 상태를 Switch 문으로 작성하여 HTML 에 표기하여 확인할수도</u>

​      <u>javaSciprt console.log 로도 확인 가능 하다.</u>







		## status

* status 프로퍼티는 서버로부터 도착한 응답의 상태 값을 나타낸다 그값은 

  	 1) 서버로부터 도착한 응답의 상태값을 나타낸다.
  	 2)  200(OK): 요청 정상 처리
  	 3) 403(Forbidden): 접근 거부
  	 4) 404(Not Found): 페이지 없음
  	 5) 500(Internal Server Error): 서버 오류 발생



## :rocket: JSON

JSON.stringify = 객체를 JSON 으로 바꿔서 직렬화시킨다

* 직렬화 Object -> JSON
  * 서버와 클라이언트가 연결하여 데이터를 주고받을때
    * 클라이언트에서 서버로 객체를 전송할때는 JSON의 문자열로 변환해서 보낸다 

JSON.parse = JSON 을 객체로 바꿔서 사용한다.

* 역직렬화 JSON -> Object , parse(json)
  * 직렬화된 JSON 은 바로 사용할수없다
  * 클라이언트가 서버로부터 JSON의 문자열 데이터를 받아서 객체로 변환해서 사용한다.

### code  

* rabbit 이라는 변수에 객체를 생성하여 직렬화를 해보겠다.



```javascript
const rabbit = {
  name: "tori",
  color: "white",
  size: null,
  age:20,
  birthdate: new Date(),
  jump: () => {
    // 멤버 메서드 는 JSON에 제외된다.
    console.log(`${name} can jump!`);
  },
};

```



* console.log	

```javascript
{"name":"tori","color":"white","size":null,"age":20,"birthdate":"2022-05-13T07:09:30.695Z"}
```

위에 콘솔출력 결과 처럼 메소드는 직렬화과 되지않는다 !

* 데이터를 사용하기위해 JSON 파일을 반대로 역직렬화 를 해보겠다.

  ```javascript
  let obj = JSON.parse(json);
  console.log(obj);
  ```

* console.log

```
{name: 'rab', color: 'white', size: null, age: 20, birthdate: '2022-05-13T07:09:30.695Z'}
```

* 사용할수있는 JavaScript 에서 사용 할수있는 object 형태로 바뀌었다 ~

### :100: 요약

* 문자열 JSON 데이터를 -> JSON.parse() 하여 실제 Object 로 파싱한후 사용한다!
* object 데이터를 서버에 보낼때에는 JSON.stringify() 하여 문자열 JSON 으로 변경하여 보낸다.

