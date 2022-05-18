## 🌠 Jquery 

설치

* jQuery 다운로드 : https://jquery.com/download/

  * 설치시

    ```javascript
       <script src="../scripts/jquery-3.6.0.js"></script>
    ```

  * cnd 사용시

    ```javascript
    <script src="https://code.jquery.com/jquery-3.5.0.js"></script>
    ```

    

*  vs code 에서 jquery 를 사용시 
  * 환경설정에서 html 입력후 html.json 내용을이렇게바꾸면 !! + 엔터 누르면 jquery세팅이된다

```json
{
	// Place your snippets for html here. Each snippet is defined under a snippet name and has a prefix, body and 
	// description. The prefix is what is used to trigger the snippet and the body will be expanded and inserted. Possible variables are:
	// $1, $2 for tab stops, $0 for the final cursor position, and ${1:label}, ${2:another} for placeholders. Placeholders with the 
	// same ids are connected.
	// Example:
	"!!": {
		"prefix": "!!",
		"body": [
				"<!DOCTYPE html>",
				"<html lang='ko'>",
				"<head>",
				"<meta charset='UTF-8'>",
				"<meta name='viewport' content='width=device-width, initial-scale=1.0'>",
				"<title>$1</title>",
				"<style>$2</style>",
				"<script src='https://code.jquery.com/jquery-3.5.0.js'></script>",
				"<script>",
				"$(function () {",
				"$3",
				"});",
				"</script>",
				"</head>",
				"<body>",
				"$4",
				"</body>",
				"</html>",
	 	],
	 	"description": "Log output to console"
	 }
}
```



### 기본적인 class , id 를 추가하고 삭제하는 방법

1. `class` 추가하기

```javascript
// 문법
$('#element').addClass('[class 명]');

// 예시
$el.addClass('prd_select');
```

1. `class` 삭제하기

```javascript
// 문법
$('#element').removeClass('[class 명]');

// 예시
$el.removeClass('prd_select');
```

1. `id` 추가하기

```javascript
// 문법
$('#element').attr('id', '[id 명]');

// 예시
$el.attr('id', 'wrapBackground');
```

1. `id` 삭제하기

```javascript
// 문법
$('#element').removeAttr('id', '[id 명]');

// 예시
$el.removeAttr('id', 'wrapBackground');
```

***

### :star: $("태그 :empty")

* 태그에 text 가 비어있는 element 에 css 로 style을 변경하고 text 를 추가해보자



```javascript
<!DOCTYPE html>
<html lang='ko'>
<head>
<meta charset='UTF-8'>
<meta name='viewport' content='width=device-width, initial-scale=1.0'>
<title></title>
<style></style>
<script src='https://code.jquery.com/jquery-3.5.0.js'></script>
<script>
$(function () {
    $("td:empty").text("Was empty").css("background","rbg(255,200,200)");
});
</script>
</head>
<body>
    <table>
        <tr>
            <td>TD #0</td>
            <td></td>
        </tr>
        <tr>
            <td>TD #2</td>
            <td></td>
        </tr>
        <tr>
            <td></td>
            <td>TD#5</td>
        </tr>
    </table>

</body>
</html>
```


***

### :star: nth-child() 와 eq() 의 차이점

* $( "ul li:nth-child(2)" ).append( "<span> - 2nd!</span>" )
  *    ul 태그 안에 자식 태그 li  2번째  태그에 2nd! 문자열을 추가한다

* $( "ul li" ).eq(2).append( "<span> - 3nd!</span>" )
  *  ul 태그 안에 자식태그 li 에 3번째 태그에 3nd! 문자열을 추가한다
    * .eq( 2 ) 는 index 번호로 사용되어 eq( ) 를사용할때 순서를 0부터 생각해야한다.  

​	`예제`

```javascript
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>nth-child demo</title>
  <style>
  div {
    float: left;
  }
  span {
    color: blue;
  }
  </style>
  <script src="https://code.jquery.com/jquery-3.5.0.js"></script>
</head>
<body>
 
<div>
  <ul>
    <li>John</li>
    <li>Karl</li>
    <li>Brandon</li>
  </ul>
</div>
<div>
  <ul>
    <li>Sam</li>
  </ul>
</div>
<div>
  <ul>
    <li>Glen</li>
    <li>Tane</li>
    <li>Ralph</li>
    <li>David</li>
  </ul>
</div>
 
<script>
$( "ul li:nth-child(2)" ).append( "<span> - 2nd!</span>" );
$( "ul li" ).eq(2).append( "<span> - 3nd!</span>" );
</script>
 
</body>
</html>
```



***

## :star: jquery 필터 기능들



jquery 에서 특정 엘리먼트를 선택할때 큰범위에서 작은 범위로 필터링 하는 경우 쓰면좋다

* .first() 
  * 일치하는 요소 집합을 집합의 첫 번째 요소로 줄인다.
     인수가 없는 함수이다.

```javascript
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>first demo</title>
  <style>
  .highlight {
    background-color: yellow;
  }
  </style>
  <script src="https://code.jquery.com/jquery-3.5.0.js"></script>
</head>
<body>
 
<ul>
  <li>Look:</li>
  <li>This is some text in a list.</li>
  <li>This is a note about it.</li>
  <li>This is another note about it.</li>
</ul>
 
<script>
$( "ul li" ).first().addClass( "highlight" );
</script>
 
</body>
</html>
```



* even() 짝수 / odd() 홀수 필터
  * 일치하는 요소 집합을 0부터 번호가 지정된 집합의 짝수/홀수로 줄인다.

```javascript
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>even demo</title>
  <style>
  .highlight {
    background-color: yellow;
  }
  .highlight2 {
    background-color: aqua;
  }
  </style>
  <script src="https://code.jquery.com/jquery-3.5.0.js"></script>
</head>
<body>
 
<ul>
  <li>Look:</li>
  <li>This is some text in a list.</li>
  <li>This is a note about it.</li>
  <li>This is another note about it.</li>
</ul>
 
<script>
$( "ul li" ).even().addClass( "highlight2" );
$( "ul li" ).odd().addClass( "highlight" );
</script>
 
</body>
</html>
```



* $(":header") 
* $(":contains(text)")
* $(":has(태그)") 
* $(":parent)
* 

**:100: 4가지 기능들은 코드와 주석을 살펴보자**



```javascript
<!DOCTYPE html>
<hr lang='ko'>

<head>
    <meta charset='UTF-8'>
    <meta name='viewport' content='width=device-width, initial-scale=1.0'>
    <title></title>
    <style></style>
    <script src='https://code.jquery.com/jquery-3.5.0.js'></script>
    <script>
        $(function () {
            //header
            $(":header").css("background-color", "red");
            //contains
            $("div:contains('John')").css("text-decoration", "underline");
            //has
            $("div:has(p)").addClass("test");
            //parent
            $("td:parent").fadeTo(1500,0.2); //fadeTo 메서드 = 1.5초 동안 0.2투명도 로 변경 수치는 0~1이다
        });
    </script>
    <style>
        .test {
            border: 1px inset red;
        }

        td {
            width: 40px;
            background: green;
        }
    </style>
</head>

<hr>
<!-- header/contain/has/parent 필터: $(":header")   : h1 ~ h6까지의 heading태그-->
<h1>Header 1</h1>
<p>Contents 1</p>
<h2>Header 2</h2>
<p>Contents 2</p>

<hr>
</hr>
<!-- $(":contains(text)")  : 특정 text를 포함하고 있는 태그 -->
<div>John Resig</div>
<div>George Martin</div>
<div>Malcom John Sinclair</div>
<div>J. Ohn</div>

<hr>
</hr>
<!-- $(":has(태그)")      : 특정 태그를 포함하고 있는 태그  -->

<div>
    <p>Hello in a paragraph</p>
</div>
<div>Hello again! (with no paragraph)</div>
<!-- $(":parent) : 하나 이상의 자식 노드(요소 또는 텍스트)가 있는 모든 요소를 선택한다. -->
<table border="1">
    <tr>
        <td>Value 1</td>
        <td></td>
    </tr>
    <tr>
        <td>Value 2</td>
        <td></td>
    </tr>
</table>
</body>

</html>
```



*** 










