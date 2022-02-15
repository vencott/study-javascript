# jQuery

## 라이브러리와 jQuery
- 라이브러리 : 자주 사용하는 로직을 재사용할 수 있도록 고안된 소프트웨어
- jQuery : DOM을 내부에 감추고 보다 쉽게 웹페이지를 조작할 수 있도록 돕는 도구

## jQuery의 사용
- 아래와 같이 jQuery( document ).ready(function( $ ) {})로 감싸는 것이 이상적이다

```
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script> // CDN
<script>
    jQuery(document).ready(function ( $ ) {
        $('body').prepend('<h1>Hello world</h1>');
    });
</script>

// $('body') : body태그를 선택하는 부분
// .prepend('<h1>Hello world</h1>'); : element의 앞에 HTML코드 삽입
```

## 제어 대상을 찾기

### 기본문법

```
- $('li').css('color', 'red');
```

- $() 는 jQuery 함수이다
- 이 함수의 인자로 CSS 선택자를 전달한다
- 이 함수가 반환하는 것이 jQuery 객체이다
- .css()는 jQuery 객체의 메소드이다
- jQuery 객체의 메소드는 jQuery 함수의 인자에 해당되는 Element들(전체)에 대해 로직을 실행된다

### 엘리먼트 제어
- 다음 코드들의 위, 아래 코드는 같은 동작을 한다
- jQuery를 사용하면 얼마나 코드량이 줄어드는 지 알 수 있다

```
// 태그
// DOM
var lis = document.getElementsByTagName('li');
for (var i = 0; i < lis.length; i++)
	lis[i].style.color = 'red';

// jQuery
$('li').css('color', 'red');



// 클래스
// DOM
var actives = document.getElementsByClassName('active');
for (var i = 0; i < lis.length; i++)
    actives[i].style.color = 'red';

// jQuery
$('.active').css('color', 'red');



// 아이디
// DOM
var active = document.getElementById('active');
active.style.color = 'red';
active.style.textDecoration = 'underline';

// jQuery
$('#active').css('color', 'red').css('textDecoration', 'underline'); // Chaining
```