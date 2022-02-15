# jQuery 속성 제어 API

## attr 메소드
- DOM에서의 getAttribute, setAttribute에 대응

```
var t = $('#target');
console.log(t.attr('href'));
t.attr('title', 'opentutorials.org');
t.removeAttr('title');
```

## prop 메소드
- DOM의 프로퍼티 방식에 대응

```
<input id='target' type='checkbox' checked='checked' />

var t = $('#target');
console.log(t.attr('checked')); // checked(써있는 그대로)
console.log(t.prop('checked')); // true
```

## jQuery 속성 제어 API의 장점
1. 코드가 간결하다
2. property 방식의 이름은 실제 HTML 속성과 이름이 다른 경우가 많은데, jQuery에서 이를 보정해준다

```
$('#t1').prop('className', 'important'); // property 방식의 원래 이름
$('#t1').prop('class', 'important'); // HTML 속성 이름을 써도 jQuery 자체 보정
```

## jQuery 조회범위 제한
- DOM에서 getElementBy* 메소드는 누가 호출하느냐에 따라 호출자의 하위 Element를 조회의 대상으로 삼았다
- jQuery도 가능하다

### selector context
- jQuery의 조회 범위를 제한하는 방법에서 그 제한된 범위를 selector context 라고 한다
- jQuery 함수의 두번째 인자로 selector context를 넘긴다
- 또는 css 선택자 문법을 따른다

```
// HTML
<ul>
    <li class="marked">html</li>
    <li>css</li>
    <li id="active">JavaScript
        <ul>
            <li>JavaScript Core</li>
            <li class="marked">DOM</li>
            <li class="marked">BOM</li>
        </ul>
    </li>
</ul>


// JS
$('.marked', '#active').css("background-color", 'red'); // 두번째 인자로 selector context 전달
$('#active .marked').css("background-color", 'red'); // css 선택자 문법
```

### find

```
$('#active').find('.marked').css("background-color", "red");

// active와 하위의 항목을 모두 파란색으로 하고, 그중에서 클래스가 marked인 부분의 배경만 빨갛게 하고 싶으면?
$('#active').css('color', 'blue').find('.marked').css("background-color", "red");
```