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

