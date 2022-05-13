### :star: DOM 을 이용하여 태그를 생성하고 삭제해보자 !!

* 우선 코드를 보자

## Sciprt Code



```javascript
<script>
        let count = 1;
        function addF() {
            let div = document.getElementById('textHolder'); //div 태그에 접근
            let p = document.createElement('p'); //p태그를 생성

            let inputTag = document.createElement('input'); //input 태그를 생성
            inputTag.setAttribute("type", "file"); //속성을준다
            inputTag.setAttribute("name", "file"); //속성을준다
            p.innerHTML = `파일선택  ${count} : `; // 문자와 변수를 함께 사용하기위해 template literal 사용

            div.appendChild(p); //부모 태그에 appendChild 사용하여 p 태그 추가
            p.appendChild(inputTag); // p 태그 에 다시 appendChild 하여 input 태그 추가
            count++; // count 증가 
        }
        function deleteF() {

            let div = document.getElementById('textHolder');      //부모태그를 선택하고
            let p = document.getElementsByTagName('p');   //p태그 를 찾아서 배열로 반환받는다.
            if(count != 1){ //         count 가 1 보다 내려가면 안되기때문에 조건문 하나를 주고
                div.removeChild(p[count - 2]); //count 는 1부터시작하지만 이미+1 이됬으니 -2 를 해서  index 0을 추출한다.
                                               //반환된 변수 p 는 배열이기때문에 index 로 접근 한다.
                if (count > 1) { // 삭제를했으니 count 값을 다시  -1 해주되 버튼을계속누를수있으니,1보단 클때만 감소하게 조건문 을 추가한다.
                    count--;
                }
            }
        }
    </script>
```

## Body Code

```javascript
<body>
    <input type="button" name="btnAdd" value="파일선택추가" onclick="addF(`${count}`)">
    <input type="button" name="btndelete" value="파일선택삭제" onclick="deleteF()">
    <br>
    <div id="textHolder">

    </div>
</body>
```



### :star2:  addF 함수



1. 우선 addF 함수 를 만든후 HTM 에 div 태그 안 자식 태그 를 만들기전에 div 태그 에 id 를 정의해주고 script 에서 dom조작을 위해 

   getElementById 로 접근한다.

2. div 태그안에 필요한 p 태그는 createElement 를 이용하여 생성 한다

3. input 태그도 마찬가지로 생성 후 속성 또한 setAttribute 를 이용하여 조작해준다. 

4. 이때 p 태그에는 innerHTML 을 이용하여 문자열을 입력하는데 count 변수를 동적으로 이용하기위해 template literal 을 이용하였다.

5. addF 함수 끝에는 button 태그 클릭시 내부적으로count 값을 하나증가시켜주는데 이 count 는 나중에 index 를 이용하여 접근할 때 필요한 값이다.



### :star2:  deleteF 함수

1) 부모태그인 div 를 선택한다
2) getElementsByTagName 를 이용하여 p 태그를  p 변수에 배열로 반환받는다 :question: ( getElementsByTagName 를사용하면 찾은 태그들을 배열로 반환 한다 ! )

3) 부모태그인 div 태그에 removeChild 를 이용하여 자식태그를 삭제할 준비를한다
4) 삭제할태그는 count 를 index 로 이용하여 p [ count + 2]  를 해준다  (:question: +2 를 해주는이유는 코드에 주석처리 해놓았다.)
5) 삭제하였으니 count 를 감소해준다 



***

빠트린 부분들은 코드에 주석을 달아놨으니 참고하면된다~

### :rocket:  이렇게 하면 button 의 파일추가 와 파일 삭제 버튼을 누르면 브라우저에 HTML 이 동적으로 

###         생성되고, 삭제되고를 확인할수 있다. ~!

