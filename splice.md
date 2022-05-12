## :rocket:  splice () 함수 사용하기

### Array.prototype.splice()

splice 함수는 배열의 기존요소들을 추가/삭제/교체 하거나 변경할수 있다.



### :cactus: splice(start[, deleteCount[, item1[, item2[, ...]]]])

**start: 배열의 변경을 시작할 인덱스.**

- **음수**를 지정한 경우: 배열의 끝에서부터 요소를 센다.
- **배열의 길이보다 큰 수**를 지정한 경우: 실제 시작 인덱스는 배열의 길이로 설정
- **절대값이 배열의 길이보다 큰 경우**: 0으로 세팅

 

**deleteCount: 배열에서 제거할 요소의 수.**

- **생략** / 값이 **array.length - start****보다 큰 경우**: start부터의 모든 요소를 제거.
- **0 이하의 수**를 지정: 어떤 요소도 제거되지 않는다.

 

**item1, item2, ... : 배열에 추가할 요소.**

- **지정하지 않는 경우**: splice()는 요소 제거만 수행한다.

 

**반환값:** **제거한 요소를 담은 배열.**

- 아무 값도 제거하지 않았으면 빈 배열을 반환한다.



### :bookmark_tabs:  splice 사용예

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script>
        let arr = [0,1,2,3,4,5];
        let arr2 ;
        function start(){
          arr.splice(6,0,7); // 배열크기보다큰 6인덱스에 삭제 없이 7을 넣으면 뒤에서 추가된다
          console.log(arr);
          arr2 = arr.splice(3); //앞에서 3번째 요소뒤 모두를 arr2 에 저장하고 arr은 3만남긴다
          console.log(arr);  // [ 1, 2, 3]
          console.log(arr2); //[ 3, 4, 5, 7]
          arr3 = arr2.splice(-2,1);  // 뒤에서부터 2번째 1요소를 삭제 
          console.log(arr2); // [ 3, 4, 7 ]
          console.log(arr3); //[ 5 ]
          arr2.splice(1,0,'a','b','c'); // index 1부터 삭제없이 'a','b','c' 를 추가한다
          console.log(arr2); // [3, 'a', 'b', 'c', 4, 7]
            
           //------------------------------------------------------
           //   splice(0, 0, element)는 배열 맨 앞에 요소를 추가합니다.
            const array = [1, 2, 3];

            arr.splice(0, 0, 'A');
            console.log(arr); //[ 'A', 1, 2, 3 ]

            arr.splice(0, 0, 'B');
            console.log(arr); //[ 'B', 'A', 1, 2, 3 ]

            arr.splice(0, 0, 'C');
            console.log(arr); //[ 'C', 'B', 'A', 1, 2, 3 ]
        }
    </script>
</head>
<body onload="start()">
    
</body>
</html>
```

