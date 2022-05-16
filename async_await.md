## :rocket:  async , await 를 사용해보자

* Promise 사용시 좀더 간편하게 사용할수 있다.
* async function 선언은 AsyncFunction 객체를 반환하며, 비동기 함수를 정의한다.
* 비동기 함수를 사용하는 코드의 구문과 구조는 , 마치 동기함수를 사용하는 것처럼 보인다.
* async 함수에 await 식은 포함되는데, await 은  async 함수를 일지 적으로 정지시키고 전달된  Promise 가 모두 해결된후 async 함수를 이어서 실행하고 완료후 값을 반환한다.
* <u>**await 키워드는 async 함수 내에서만 유효 하다.**</u>
* asynce , await 을 너무 많이사용하면 callback hell 처럼 된다.



:heavy_exclamation_mark: async 사용 예제를 보자

```javascript
async function fetchUser(){
    return 'study';         //  0)
}
const user = fetchUser(); //  1)

user.then(console.log); //  2)

console.log(user); //  3)
```

```javascript
-브라우저 콘솔 출력내용-

Promise {<fulfilled>: 'study'}
[[Prototype]]: Promise
[[PromiseState]]: "fulfilled"
[[PromiseResult]]: "study"


```





* 위 코드를 보면 Promise 를 찾아볼수가 없지만 async 가 붙은 함수는 return 해주는 대상이 Promise 객체이다.

* return 된 'study' 라는 문자열은 Promise 객체의 resolve 가 되는것이고, async 함수를 user 변수에 담아서 콘솔로 확인 해보면 변수 user는 Promise 라고 나오고 , Prototype : Promise , PromiseState : "fulfilled" , PromiseResult : "study" 를 확인할수있다.
  * user 에 then 을 사용할수있는이유는 Promise 니까! resolve 값을 원하면 .then 으로 접근 
  * reject 값을 원한다면  .catch 를 사용하면되겠다.

### ☘️ await 키워드를 사용했을때  좀더 편하게 사용할수있다.

* async 함수만 사용하고  await 키워드를 사용하지않은 예를 보자

  ```javascript
  function delay(ms) {
    return new Promise((resolve) => setTimeout(resolve, ms));
  }
  async function getApple() {
    await delay(1000);
    //throw 'error'
    return "apple";
  }
  async function getBanana() {
    await delay(1000);
    return "banana";
  }
  function pickFruits() {
    return getApple().then((apple) => {
      return getBanana().then((banana) => `${apple} + ${banana}`);
    });
  }
  pickFruits().then(console.log);
  ```

  

Promise 의 then 을 사용하여 결과를 출력하였지만, 보기가좋지않다 await 을 이용해보자



```javascript
function delay(ms) {
  return new Promise((resolve) => setTimeout(resolve, ms));
}
async function getApple() {
  await delay(1000);
  //throw 'error!!!'
  return "apple";
}
async function getBanana() {
  await delay(1000);
  return "banana";
}
// function pickFruits() {
//   return getApple().then((apple) => {
//     return getBanana().then((banana) => `${apple} + ${banana}`);
//   });
// }
// pickFruits().then(console.log);

async function pickFruits(){
    try{

        const apple = await getApple();
        const banana = await getBanana();
        return `${apple} + ${banana}`;

    }catch{
        console.log(new Error('error'));
    }
}
```

await 을 사용하여도 같은 처리가 가능하지만 좀더 직관적인 코드가 되었다! 

