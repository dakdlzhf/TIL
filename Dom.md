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





