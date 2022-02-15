# Element 객체

```
var t = document.getElementById('active');
```

- 위 코드에서 t는 HTMLLIElement이다
- HTMLLIElement는 HTMLElement의 자식이며 다른 태그들도 HTMLElement의 자식이다
- HTMLElement의 부모는 Element이다
- DOM은 Markup Language들을 제어하기 위한 규격이기 때문에 HTMLElement가 따로 존재하는 것이다(XML, SVG, XUL...)
- Element의 부모는 Node이며 계층 구조를 이해하는 것이 중요하다

```
Node
	Document
		HTMLDocument

	CharacterData
		Text
			Comment

	Element
		HTMLElement
			HTMLLIElement
			HTMLHeadElement

	Attr
```

## 식별자 API

### Element.tagName
- 수정이 불가능하다

```
console.log(document.getElementById('active').tagName); // LI
```

### Element.id
- id는 문서에서 단 하나의 태그만 그 id를 가질 수 있다
- 단 하나의 Element를 식별하는 유일한 식별자
- 수정 가능

```
var active = document.getElementById('active');
console.log(active.id); // active
active.id = 'deactive';
console.log(active.id); // deactive
```

### Element.className
- 태그의 class 속성을 조회하거나 변경
- 다소 불편하다


```
var active = document.getElementById('active');
active.className = 'important current';
console.log(active.className); // important current
active.className += " readed";
console.log(active.className); // important current readed
```

### Element.classList
- DOMTokentList 반환(유사배열)
- 클래스들을 토큰 형태로 표현(spacebar를 기준으로 파싱)


```
var active = document.getElementById('active');
console.log(active.classList); // DOMTokenList

for (var i = 0; i < active.classList.length; i++)
    console.log(active.classList[i]); // hello world

active.classList.add('hi');
for (var i = 0; i < active.classList.length; i++)
    console.log(active.classList[i]); // hello world hi

active.classList.remove('hello');
for (var i = 0; i < active.classList.length; i++)
    console.log(active.classList[i]); // world hi

active.classList.toggle('hello');
for (var i = 0; i < active.classList.length; i++)
    console.log(active.classList[i]); // toggle class 'hello'
```

## 조회 API
- document.getElementsBy* 를 통해서 조회
- document는 문서 전체를 의미하는 객체
- Element 객체의 조회 메소드는 해당 Element의 하위 Element를 대상으로 조회를 수행

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
var list = document.getElementsByClassName('marked');

console.group('document');
for (var i = 0; i < list.length; i++)
    console.log(list[i].textContent); // html DOM BOM
console.groupEnd();

console.group('active');
var active = document.getElementById('active');
var list = active.getElementsByClassName('marked');
for (var i = 0; i < list.length; i++)
    console.log(list[i].textContent); // DOM BOM
console.groupEnd();
```

## 속성 제어 API

### 속성 제어
- Element.getAttribute()
- Element.setAttribute()
- Element.hasAttribute()
- Element.removeAttribute()

```
var t = document.getElementById('target');
console.log(t.getAttribute('href')); // https://www.naver.com
t.textContent = '다음';
t.setAttribute('href', 'http://www.daum.net');

t.setAttribute('title', 'opentutorials.org');
console.log(t.hasAttribute('title')); // true
t.removeAttribute('title');
console.log(t.hasAttribute('title')); // false
```

### 속성과 프로퍼티
- 모든 엘리먼트의 속성은 JS 객체의 속성과 프로퍼티로 제어가 가능하다

```
var t = document.getElementById('target');

t.setAttribute('class', 'important'); // 속성 방식

t.className = 'important'; // 프로퍼티 방식
```

- 하지만 property 방식의 이름 실제 HTML 속성 이름과 이 다른 경우가 있으므로 조심하자

```
attribute 방식(HTML) / property 방식

class / className
readonly / readOnly
rowspan / rowSpan
colspan / colSpan
usemap / userMap
frameborder / frameBorder
for / htmlFor
maxlength / maxLength
```

- 또한 속성 방식과 프로퍼티 방식의 값이 다른 경우가 있으므로 주의하자

```
var t = document.getElementById('target');
// <a id='target' href='/demo1.html'>demo1</a>(상대경로)

console.log('속성 방식', t.getAttribute('href')); // ./demo1.html(상대경로, 써있는 그대로)

console.log('프로퍼티 방식', t.href); // http~~~~~/demo.html(전체경로)
```