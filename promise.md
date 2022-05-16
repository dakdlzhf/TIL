## Promise 

* `promise` 

  * 객체가 비동기 작업이 맞이할 미래의 완료, 실패 의 결과를 '약속'(프로미스)을 반환합니다.

    [promise MDN 보러가기](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise)

* `Promise` 는 다음 중 하나의 상태를 가집니다.

  - 대기(*pending)*: 이행하지도, 거부하지도 않은 초기 상태.

  - 이행(*fulfilled)*: 연산이 성공적으로 완료됨.

  - 거부(*rejected)*: 연산이 실패함.





(1) Promise 생성, 사용

 	

```javascript
const promise = new Promise((resolve, reject) =>{ 

  });
```



1) Promise 생성자에서 excutor 콜백함수는 또다른 resolve(정상수행 후 결과전달), reject(문제가 생기면 호출) 
    콜백함수를 받는다.
2) Promise는 시간이 걸리는 비동기 처리를 구현할 수 있다.
3) **Promise를 생성하면 executor 콜백함수가 자동으로 실행된다. (※)**
4) Promise를 생성하여 비동기 처리를 구현 후 resolve(), reject() 콜백 함수를 호출하여 그결과를 전달한다.
5) Promise 사용하는 곳에서 결과를 then, catch, finally 등으로 받을 수 있다.



###  :rocket: **사용 예제**

1) `Producer` : 제공자

```javascript
const promise = new Promise((resolve,reject)=>{
    console.log('doing something');
    setTimeout(()=>{
        resolve('study');
    },2000)
});
```



2) Cunsumers : 사용자 는 then(성공시), catch(거부시) , finally(무조건실행) 

```javascript
  promise
    .then((value)=>{console.log(value)})
    .catch((error)=>{console.log(error)})
    .finally(()=>{
        console.log('finally 실행')
    });
```



:triangular_flag_on_post: Promise 는 객체를 만들어서 promise 를 반환하고 사용자가 콜백함수의 매개변수로 결과값에 접근할수 있다.

then 메서드는 값 또는 promise 객체가 전달된다.

