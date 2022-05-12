## :robot:  split () 함수 사용하기



* split()  함수는,
  문자열을 'separator'로 잘라서,
  'limit' 크기 이하의 배열에 잘라진 문자열을 저장하여 리턴합니다.

  separator

  - 필수 아님
  - 문자열을 잘라 줄 구분자 (문자열 또는 정규식)
  - 값이 입력되지 않으면 문자열 전체를 배열에 담아서 리턴합니다.

  limit

  - 필수 아님
  - 최대 분할 갯수



### :bookmark_tabs:  split( ) 사용예



```javascript
const str = "apple banana orange";

const arr = str.split();

console.log(arr); // apple banana orange
console.log(arr.length); // 1
```

* 파라미터를 입력하지않을경우 문자열 전체를 길이 1 인 배열로 리턴합니다.



###  :bookmark_tabs:  split('  ') 사용예



```javascript
const arr = str.split(' '); // 공백 ,스페이스를 지정하면 공백을 구분자로 하여 배열로 리턴
console.log(arr.length) // 3
console.log(arr[0]) //apple
console.log(arr[1]) //banana
console.log(arr[2]) //orange
```



### :bookmark_tabs:  split('/') 사용예



```javascript
const str = '기획자/설계자/개발자/디자이너';
const arr = str.split('/');
console.log(arr.length) //4
console.log(arr[0]) //기획자
console.log(arr[1]) //설계자
console.log(arr[2]) //개발자
console.log(arr[3]) //디자이너
```



### :bookmark_tabs:  limit 값 지정하기



```javascript
const str = "apple,banana,orange";

const arr = str.split(",", 2);

document.writeln(arr.length); // 2
document.writeln(arr[0]); // apple
document.writeln(arr[1]); // banana
document.writeln(arr[2]); // undefined
```



