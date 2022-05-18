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


