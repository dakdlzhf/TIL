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
                //지금 상태가 pendding 상태이다.
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

:white_check_mark:  Callback Hell  코드를 Promise 로 리팩토링 하는 과정을 살펴 본다



*  Promise 를 사용하지않고 콜백함수로 처리를 할경우 체이닝이 길어지고, 나중에 디버깅이 힘들어진다.

```javascript
class UserStorage {
    loginUser(id,password, onSuccess, onError){ //로그인 확인
        setTimeout(()=>{ //서버역할, 어느정도 시간을 걸리게한다.
            if (
                (id === 'study' && password === 'aistudy') ||
                (id === 'coder' && password === 'academy')
            ) {
                onSuccess(id);
            } else {
                onError(new Error('not found'))
            }
        }, 2000)
    }
    getRoles(user, onSuccess, onError){ //사용자 역할 받아오기
        setTimeout(() => { //서버역할, 어느정도 시간을 걸리게한다.
            if(user === 'study' ){
                onSuccess({ name : 'study', role : 'admin'});
            } else {
                onError(new Error('no access'))
            }
        },1000)
 
    }
}
 
const userStorage = new UserStorage();
const id = prompt('enter your id');
const password = prompt('enter your password');
userStorage.loginUser(
    id, 
    password, 
    user => {
        userStorage.getRoles(
            user,
            userWithRole => {
                alert(`hello ${userWithRole.name}, you have a ${userWithRole.role} role`);
            },
            error => {
                console.log(error);
            }
        );
    }, 
    error => { console.log(error)}
);
```

:heavy_exclamation_mark: Promise 사용 후

```javascript
	class UserStorage {
    loginUser(id,password){
        return new Promise((resolve, reject) => {
            setTimeout(()=>{
                if (
                    (id === 'study' && password === 'aistudy') ||
                    (id === 'coder' && password === 'academy')
                ) {
                    resolve(id);
                } else {
                    reject(new Error('not found'))
                }
            }, 2000);
 
        });  
    }
    getRoles(user) {
        return new Promise((resolve, reject) => {
            setTimeout(() => {
                if(user === 'study' ){
                    resolve({ name : 'study', role : 'admin'});
                } else {
                    reject(new Error('no access'))
                }
            },1000);
        });
 
    }     
 
}
 
const userStorage = new UserStorage();
const id = prompt('enter your id');
const password = prompt('enter your password');
userStorage
    .loginUser(id, password) //로그인 성공하면 id 전달
    .then(userStorage.getRoles) //id의 역할을 전달
    .then(user => alert(`Hello ${user.name}, you have a ${user.role} role`)) //역할 확인
    .catch(console.log); //문제발생시 오류출력
```

 Promise 를 사용함으로써 코드의 가독성이 좋아지고 좀더 직관적으로 코드를 해석할수 있어진다.

## Promise 의 특성을 이용해보자!!!

* Promise 는 미래의 성공값,실패값 을 약속한다고했다 . 

  * 그값을 then 메서드로 resolve , reject 에 접근하여 값을 확인할수있다고 했었다 

    ? 그러면 async 함수로 Promise 를반환받은후 --> 그것을 then 대신 await 을사용 한다면? 

  :heart_eyes:  독립적인 처리기능을 순차적으로 하는대신 병렬 처리로 더빠르게 실행할수 있는 코드를 만들수 있지않을까 ????

:heavy_exclamation_mark:  병렬처리 전 코드

```:heavy_check_mark:
async function pickFruits() {
   try {
     const apple = await getApple();
     const banana = await getBanana();
     return `${apple} + ${banana}`;
  } catch {
     console.log(new Error('error')); 
   }
 }
```

:heavy_exclamation_mark: 병렬처리 코드~

```javascript
 async function pickFruits() {
   const applePromise = getApple(); //Promise 리턴, 바로 promise 실행
   const banaaPromise = getBanana(); //Promise 리턴, 바로 promise 실행
   const apple = await applePromise;
   const banana = await banaaPromise;
   return `${apple} + ${banana}`;
 }
```

개발자 도구로 네트워크 처리 속도로 정확히 확인도 가능하지만 체감상 더빠르게 처리가되는걸 확인할수 있다.!



:heavy_check_mark: 병렬처리를 좀더 개선한 코드 ( 알아두면 좋다 )

* **Promise.all( [ ] )**

```javascript
function pickFruits(){
    return Promise.all([getApple(),getBanana()])
    .then((frutis)=>frutis.join('+'));
}
pickFruits().then(console.log);
```

  ***열 형태로 함수를 넣어주면 반복문을 돌린것 처럼  배열로 병렬처리를 한다.***



* **Promise.race( [ ] )**

  ```javascript
  async function getApple() {
    await delay(2000);  // 2초
    return "apple";
  }
  async function getBanana() {
    await delay(1000);  // 1초
    return "banana";
  }
  
  function pickOnlyOne() {
    return Promise.race([getApple(), getBanana()]);
  }
   
  pickOnlyOne().then(console.log);
  
  // getBnana 의 resolve 가 출력된다!
  ```

  

  *  먼저 수행되는 처리결과를 하나만 가져온다! 

