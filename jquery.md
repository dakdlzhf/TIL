## ๐  Jquery 

์ค์น

* jQuery ๋ค์ด๋ก๋ : https://jquery.com/download/

  * ์ค์น์

    ```javascript
       <script src="../scripts/jquery-3.6.0.js"></script>
    ```

  * cnd ์ฌ์ฉ์

    ```javascript
    <script src="https://code.jquery.com/jquery-3.5.0.js"></script>
    ```

    

*  vs code ์์ jquery ๋ฅผ ์ฌ์ฉ์ 
  * ํ๊ฒฝ์ค์ ์์ html ์๋ ฅํ html.json ๋ด์ฉ์์ด๋ ๊ฒ๋ฐ๊พธ๋ฉด !! + ์ํฐ ๋๋ฅด๋ฉด jquery์ธํ์ด๋๋ค

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



### ๊ธฐ๋ณธ์ ์ธ class , id ๋ฅผ ์ถ๊ฐํ๊ณ  ์ญ์ ํ๋ ๋ฐฉ๋ฒ

1. `class` ์ถ๊ฐํ๊ธฐ

```javascript
// ๋ฌธ๋ฒ
$('#element').addClass('[class ๋ช]');

// ์์
$el.addClass('prd_select');
```

1. `class` ์ญ์ ํ๊ธฐ

```javascript
// ๋ฌธ๋ฒ
$('#element').removeClass('[class ๋ช]');

// ์์
$el.removeClass('prd_select');
```

1. `id` ์ถ๊ฐํ๊ธฐ

```javascript
// ๋ฌธ๋ฒ
$('#element').attr('id', '[id ๋ช]');

// ์์
$el.attr('id', 'wrapBackground');
```

1. `id` ์ญ์ ํ๊ธฐ

```javascript
// ๋ฌธ๋ฒ
$('#element').removeAttr('id', '[id ๋ช]');

// ์์
$el.removeAttr('id', 'wrapBackground');
```

***

### :star: $("ํ๊ทธ :empty")

* ํ๊ทธ์ text ๊ฐ ๋น์ด์๋ element ์ css ๋ก style์ ๋ณ๊ฒฝํ๊ณ  text ๋ฅผ ์ถ๊ฐํด๋ณด์



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

### :star: nth-child() ์ eq() ์ ์ฐจ์ด์ 

* $( "ul li:nth-child(2)" ).append( "<span> - 2nd!</span>" )
  *    ul ํ๊ทธ ์์ ์์ ํ๊ทธ li  2๋ฒ์งธ  ํ๊ทธ์ 2nd! ๋ฌธ์์ด์ ์ถ๊ฐํ๋ค

* $( "ul li" ).eq(2).append( "<span> - 3nd!</span>" )
  *  ul ํ๊ทธ ์์ ์์ํ๊ทธ li ์ 3๋ฒ์งธ ํ๊ทธ์ 3nd! ๋ฌธ์์ด์ ์ถ๊ฐํ๋ค
    * .eq( 2 ) ๋ index ๋ฒํธ๋ก ์ฌ์ฉ๋์ด eq( ) ๋ฅผ์ฌ์ฉํ ๋ ์์๋ฅผ 0๋ถํฐ ์๊ฐํด์ผํ๋ค.  

โ	`์์ `

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

## :star: jquery ํํฐ ๊ธฐ๋ฅ๋ค



jquery ์์ ํน์  ์๋ฆฌ๋จผํธ๋ฅผ ์ ํํ ๋ ํฐ๋ฒ์์์ ์์ ๋ฒ์๋ก ํํฐ๋ง ํ๋ ๊ฒฝ์ฐ ์ฐ๋ฉด์ข๋ค

* .first() 
  * ์ผ์นํ๋ ์์ ์งํฉ์ ์งํฉ์ ์ฒซ ๋ฒ์งธ ์์๋ก ์ค์ธ๋ค.
     ์ธ์๊ฐ ์๋ ํจ์์ด๋ค.

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



* even() ์ง์ / odd() ํ์ ํํฐ
  * ์ผ์นํ๋ ์์ ์งํฉ์ 0๋ถํฐ ๋ฒํธ๊ฐ ์ง์ ๋ ์งํฉ์ ์ง์/ํ์๋ก ์ค์ธ๋ค.

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
* $(":has(ํ๊ทธ)") 
* $(":parent)
* 

**:100: 4๊ฐ์ง ๊ธฐ๋ฅ๋ค์ ์ฝ๋์ ์ฃผ์์ ์ดํด๋ณด์**



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
            $("td:parent").fadeTo(1500,0.2); //fadeTo ๋ฉ์๋ = 1.5์ด ๋์ 0.2ํฌ๋ช๋ ๋ก ๋ณ๊ฒฝ ์์น๋ 0~1์ด๋ค
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
<!-- header/contain/has/parent ํํฐ: $(":header")   : h1 ~ h6๊น์ง์ headingํ๊ทธ-->
<h1>Header 1</h1>
<p>Contents 1</p>
<h2>Header 2</h2>
<p>Contents 2</p>

<hr>
</hr>
<!-- $(":contains(text)")  : ํน์  text๋ฅผ ํฌํจํ๊ณ  ์๋ ํ๊ทธ -->
<div>John Resig</div>
<div>George Martin</div>
<div>Malcom John Sinclair</div>
<div>J. Ohn</div>

<hr>
</hr>
<!-- $(":has(ํ๊ทธ)")      : ํน์  ํ๊ทธ๋ฅผ ํฌํจํ๊ณ  ์๋ ํ๊ทธ  -->

<div>
    <p>Hello in a paragraph</p>
</div>
<div>Hello again! (with no paragraph)</div>
<!-- $(":parent) : ํ๋ ์ด์์ ์์ ๋ธ๋(์์ ๋๋ ํ์คํธ)๊ฐ ์๋ ๋ชจ๋  ์์๋ฅผ ์ ํํ๋ค. -->
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










