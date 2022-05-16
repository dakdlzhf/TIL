# :rocket:  Dom 을 조작해보자

\- W3C에서 표준을 제작하고 있다.



* DOM은 HTML 문서의 객체 기반 표현방식이다
* DOM은 구조화된 nodes와 property 와 method 를 갖고 있는 objects로 문서를 표현한다. 
* 웹 페이지는 일종의 문서(document)다. 이 문서는 웹 브라우저를 통해 그 내용이 해석되어
   웹 브라우저 화면에 나타나거나 HTML 소스 자체로 나타나기도 한다. 
* HTML 문서의 내용과 구조를 객체 모델로 변환시켜 다양한 컨트롤이 가능한 장점이있다.
* Ajax를 사용하여 서버로부터의 응답 결과를 전송받아 브러우저의 HTML상에 출력할 때에
   DOM 모델을 이용한다.
* DOM은 Object들을 Tree 처럼 생성합니다.
*  DOM 은 동일한 문서를 표현하고, 저장하고, 조작하는 방법을 제공한다. 
* DOM은 동적으로 HTML 태그를 생성할때 필요하다.
* DOM은 HTML 문서로부터 생성되지만 항상 동일하진않다
  * DOM이 원본 HTML 소스와 다를수 있다
    
    

* Dom은 HTML 문서의 내용을 볼수있는 인터페이스 역활이며, 동시에 동적 인 수정도가능하다

## 요약정리

DOM은 HTML 문서에 대한 인터페이스입니다. 첫째로 뷰 포트에 무엇을 렌더링 할지 결정하기 위해 사용되며,
둘째로는 페이지의 콘텐츠 및 구조, 그리고 스타일이 자바스크립트 프로그램에 의해 수정되기 위해 사용됩니다.
DOM은 원본 HTML 문서 형태와 비슷하지만 몇 가지 차이점이 있습니다.

- 항상 유효한 HTML 형식입니다.

- 자바스크립트에 수정될 수 있는 동적 모델이어야 합니다.

- 가상 요소를 포함하지 않습니다. (Ex. `::after`)

- 보이지 않는 요소를 포함합니다. (Ex. `display: none`)

  

### 자바스크립트로 Element 에 접근 사용하기

```javascript
    <p id="intro">Hello World!</p>
    <p id="demo"></p>

    <script>
        var myElement = document.getElementById("intro");
        document.getElementById("demo").innerHTML =
             myElement.innerHTML+ " 홍길동";
    </script>

```

output

```
Hello World!

Hello World! 홍길동
```



### :star2:  Form 에 접근해보는 사용하기



```javascript
<!DOCTYPE html>
<html>
<body>
    <!-- 첫번째 폼 1 -->
<form id="frm1" action="form_action.asp">
  First name: <input type="text" name="fname" value="Donald"><br>
  Last name: <input type="text" name="lname" value="Duck"><br><br>
  <input type="submit" value="Submit">
</form> 
    <!-- 두번째 폼 2 -->
<form id="frm2" action="form_action.asp">
    First name: <input type="text" name="fname" value="Donald2"><br>
    Last name: <input type="text" name="lname" value="Duck2"><br><br>
    <input type="submit" value="Submit2">
  </form> 
 
 
<button onclick="myFunction()">Try it</button>
 
<p id="demo"></p>
 
<script>
    // form 태그에안 element 에 접근하여 value 값들을 갖고오자
    // 1) 함수를 한개 만든다
    // 2) dom 을 조작 , document.forms  form 중 form 의 id 로 구분한다
    // 3) 선택된 form 안에 elements 중 index 로 접근한다
function myFunction() {
    var x = document.forms["frm2"]; 
    var text = "";
    var i;
    for (i = 0; i < x.length ;i++) {
        text += x.elements[i].value + "<br>";
    }
    document.getElementById("demo").innerHTML = text;
}
</script>
 
</body>
</html>
```
### :star: TIP



* document.all VS document.getElementById , document.getElementsByTagName

  * 결론적으로 document.all 은 모든 HTML,HEAD ,TITLE 태그까지 모두 참조하기떄문에 느리다.
  * 대체로.document.getElementById  와 document.getElementsByTagName를 사용하여 유일한 id 값만 골라서 참조하는것이 좋다고 생각든다. 또한 W3C 에서 표준으로 정한 탐색 스크립트이기에 브라우저 호환성이 보장된다! 
  * document.getElementsByTagName 은  document.getElementById  와 쌍대산맥 ? 을이루는 유명한 문법이지만 두가지 차이점이 존재한다
    1) 하나 이상의 요소 즉 요소의 배열을 반환한다. getElementsByName 이 반환하는 요소가 단 1개라도 배열 접근 형식 element[0] 을 해야한다.
    2) 요소에 부여된 ID 가 아닌 태그에 기반한다 getElementById 가 요소에 부여된 ID 를 기반으로 탐색한다면 getElementsByTagName 은 요소의 태그명에 기반한다 (div,sapn,img)  와같은 요소태그 !

  

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






