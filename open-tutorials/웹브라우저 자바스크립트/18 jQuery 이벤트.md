# jQuery 이벤트

## DOM vs jQuery

```
// DOM
var target = document.getElementById('pure');
if (target.addEventListener) {
    target.addEventListener('click', function (event) {
        alert('pure');
    })
} else {
    target.attachEvent('onclick', function (event) {
        alert('pure');
    });
}

// jQuery
$('#jquery').on('click', function (event) {
    alert('jQuery');
});
```

## on API 사용법

`.on(events [, selector] [, data], handler(eventObject))`

- 첫번째 인자로 이벤트 종류
- 두번째, 세번째 인자는 생략가능
- 마지막 인자로 핸들러

## 필터링
- 두번째 인자인 selector

```
$('ul').on('click','a, li', function(event) {
	console.log(this.tagName);
})

// 출력결과 : A, LI
```

- ul 태그에 이벤트를 등록했지만, selector 인자로 인해 하위의 a태그, li태그에 대해서 동작하도록 해준다
- 즉, 하위의 여러 항목에 대해 간단하게 이벤트를 등록할 수 있다
- 주의 할 점은 ul 엘리먼트는 이벤트가 발생하지 않는다는 점이다
- 이것은 jQuery에서 이벤트 버블링을 구현하는 방법이기도 하다

### late binding
- jQuery는 존재하지 않는 엘리먼트에도 이벤트를 등록할 수 있는 놀라운 기능을 제공한다

```
<body>
	<script>
    	$('ul').on('click','a, li', function(event){
        	console.log(this.tagName);
    	})
	</script>
	<ul>
    	<li><a href="#">HTML</a></li>
    	<li><a href="#">CSS</a></li>
    	<li><a href="#">JavaScript</a></li>
	</ul>
</body>
```

- 위 코드는 정상적으로 실행되지 않는다
- 그 이유는 ul 엘리먼트가 존재하지 않을 때 이벤트 설치를 하기 때문이다(ul태그가 더 아래 위치)
- jQuery에서는 다음과 같은 방법으로 late binding을 지원한다

```
<body>
	<script>
    	$('body').on('click','a, li', function(event){ // body에 binding
        	console.log(this.tagName);
    	})
	</script>
	<ul>
    	<li><a href="#">HTML</a></li>
    	<li><a href="#">CSS</a></li>
    	<li><a href="#">JavaScript</a></li>
	</ul>
</body>
```

- 우선 존재하는 상위 엘리먼트(body)에 이벤트를 바인딩 해서 하위 항목이 나중에 추가되더라도 이벤트를 동작시킬 수 있다

## 다중 등록
- 하나의 엘리먼트에 여러개의 이벤트 타입을 동시에 등록할 수 있다
- on()의 첫번째 인자에 여러 이벤트 타입을 띄어쓰기로 구분해 전달하면 된다

```
<input type="text" id="target" />
<p id="status"></p>
<script>
    $('#target').on('focus blur', function(e){
        $('#status').html(e.type);
    })
</script>
```

### 이벤트에 따라서 다른 핸들러를 설정하고 싶다면 다음과 같이 코드를 변경한다

- on의 파라미터로 이름이 이벤트 타입인 메소드들을 프로퍼티로 가지는 객체를 넘겨준다

```
$('#target').on({
    'focus': function (e) {
        $('#status').html(e.type);
    },
    'blur': function (e) {
        $('#status').html(e.type);
    }
});
```

- chaining을 이용한다

```
$('#target')
    .on('focus blur', function (e) {
        $('#status').html(e.type);
    })
    .on('blur', function (e) {
        $('#status').html(e.type);
    });
```

## 이벤트 제거

```
var firstHandler = function (e) {
    alert('handler 1');
};

var secondHandler = function (e) {
    alert('handler 2');
};

$('#target').on('focus', firstHandler);
$('#target').on('focus', secondHandler);

$('#target').off('focus', firstHandler); // 특정 이벤트 삭제
$('#target').off('focus'); // 해당 엘리먼트에 등록된 모든 이벤트 삭제
```