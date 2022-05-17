# :rocket: AJAX  (Asyncronous Java Script And Xml)



* AJAX 는 비동기 자바스크립트 를 뜻하며, 비동기적 자바스크립트 의 동작기술들을 통틀어 AJAX 라고도 부르게되고있다.

* AJAX 를 대표하는 API 중 XMLHttpRequest 와 Fetch 가있지만 오늘은 Fetch API 에 대해서만 알아보겠다.

  

  ## :tomato: `Fetch API `

  

* 기존의 XHR 객체를 이용한 AJAX 는 복잡하기도하고 가독성이 현저하게 떨어진다.
  * 그래서 등장한것이 Fetch API 로 (ES2015)에서 표준이 되었다.

* `Fetch API` 를 사용하면  `XMLHttpRequest(XHR)` 과 유사한 네트워크 요청이 가능하다

* Fetch API 가 `Promise`를 사용하기때문에 훨씬 코드가 간결해지고 사용하기 편리 하다

  * Fetch 는 반환값이 Promise이다 

    ```javascript
    fetch( resource, init )
      .then( callback )
      .catch( callback )
    ```

    * fetch( 요청경로 ,URL,경로)

    * init (optional) 설정 객체

      ```javascript
      const init = {
        method: "POST",
      	body: JSON.stringify(data),
      	headers: {
          "Content-Type": "application/json"
        },
      	credentials : "same-origin"
      }
      ```

      * fetch 에 요청경로를 입력하고 필요의경우에는  설정객체 init 을 입력한다.
      * 그 결과로 `Response` 인스턴스가 반환된다.  `.then` 에서 response 가 그결과이다.
      * 상태를 나타내는 `status` (상태 에맞는 정수 ) 와 `statusText` ( 상태에 맞는 텍스트 ) 가 있고 요청에 대한 헤어 정보를 담은 header , 응답내용을 담은 body가있다.
      * 위의 코드를 살펴보면 fetch 요청 후, 첫번째 then에서 상태 코드가 200일 경우 `response.json()`을 리턴하며, 상태 코드가 다를 경우에는 상태 문자를 출력합니다. 두번째 then으로 넘겨지게 되면 이제 첫번째 then에서 넘겨받은 값을 출력하게 됩니다.

```javascript
// data.json : {name: "Jhon", age: 29}

fetch('/src/data.json')
  .then(response => {
    // 첫번째 then
    if(response.status === 200){
      return response.json()
    } else {
      console.log(response.statusText);
    }
  })
  .then(jsonData => {
    // 두번째 then
    console.log(jsonData); // Object {name: "Jhon", age: 29}
  })
  .catch(err => {
    console.log(err)
  })
```

* Response 객체의 body 값을 추출해내기 위해서는 타입에 따라 아래와 같은 메소드를 사용해야 합니다.
  * arrayBuffer()
  * blob()
  * json()
  * text()
  * formData()

위 메소드들은 모두 Promise를 반환합니다. 그리고 이 Promise가 resolve되어 다음 then에서는 실제 값을 다룰 수 있게 됩니다.



### Fetch API 이전에 많이사용했던 `XHR` ( XMLHttpRequest) 를 간단하게만 살펴보겠다.

* `XHR`은 전통적인 Event 기반으로 동작한다. `document.addEventListener`와 비슷하다. `XHR`은 응답을 받을 때, state를 바꾸는 이벤트를 발생시키고, 이를 `onreadystatechange`를 통해 감지하게 된다.

```javascript
let xhr = new XMLHttpRequest();
xhr.open('GET', 'http://domain/service');

// request state change event
xhr.onreadystatechange = function() {

  // request completed?
  if (xhr.readyState !== 4) return;

  if (xhr.status === 200) {
    // request successful - show response
    console.log(xhr.responseText);
  }
  else {
    // request error
    console.log('HTTP error', xhr.status, xhr.statusText);
  }
};

// start request
xhr.send();
```

## :100: 요약

#### Fetch API

- Promise 기반 => *현재 비동기 처리 프로그래밍 방식과 잘 어울림*
- 이미 잘 명세된 API가 제공됨으로써 브라우저간의 불일치가 없음
- `XHR` 에는 있지만 Specification에 논의되지 않은 몇몇 유용한 기능이 없음 => *(setTimeout, abort, progress)*
- 나중에 추가 지원을 받을 수 있음

***

#### XMLHttpRequest API

- 이벤트 기반 => *현재 Promise 기반과는 많이 다름*
- 초기 API 구현 때, 브라우저 간의 불일치가 존재
- 이 브라우저간 차이를 메꾸기 위해 jQuery 사용 시작 => *jQuery가 크로스 브라우징 이슈에 나름 큰 솔루션을 제공*

