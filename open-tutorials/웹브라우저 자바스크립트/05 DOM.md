# DOM
- Document Object Model
- 웹페이지(문서)를 자바스크립트로 제어하기 위한 객체 모델
- window 객체의 document 프로퍼티를 통해서 사용
- window 객체가 창을 의미한다면 document 객체는 윈도우에 로드된 HTML 문서를 의미한다고 할 수 있다

## 제어 대상을 찾기
- 항상 다음과 같은 순서로 문서를 제어한다
1. 제어의 대상 찾기
2. 대상에 대한 작업

### document.getElementsByTagName
- 태그 이름으로 대상 Element(태그 객체) 찾기

```
// HTML
<li>HTML</li>
<li>CSS</li>
<li>JavaScript</li>

// JS
var lis = document.getElementsByTagName('li'); // 태그가 li인 Element들을 담은 유사 배열을 리턴
for (var i = 0; i < lis.length; i++)
    lis[i].style.color = 'red';
```

```
// HTML
<ul>
    <li>HTML</li>
    <li>CSS</li>
    <li>JavaScript</li>
</ul>

<ol> // ol 태그 안의 li만 제어하고 싶을땐
    <li>HTML</li>
    <li>CSS</li>
    <li>JavaScript</li>
</ol>

// JS
var ol = document.getElementsByTagName('ol');
var lis = ol[0].getElementsByTagName('li'); // 태그가 li인 Element들을 담은 유사 배열을 리턴
for (var i = 0; i < lis.length; i++)
    lis[i].style.color = 'red';
```

### document.getElementsByClassName
- 클래스 명으로 Elements 찾기

```
// HTML
<ul>
    <li class="active">HTML</li>
    <li class="active">CSS</li>
    <li>JavaScript</li>
</ul>

// JS
var lis = document.getElementsByClassName('active');
for (var i = 0; i < lis.length; i++)
    lis[i].style.color = 'red';
```

### document.getElementById
- id값으로 Element 찾기
- id는 유일하므로 Elements가 아닌 Element
- 성능이 가장 좋고, 가장 자주 쓰인다

```
// HTML
<ul>
    <li id="active">HTML</li>
    <li>CSS</li>
    <li>JavaScript</li>
</ul>

// JS
var li = document.getElementById('active');
li.style.color = 'red';
```

### document.querySelector
- 선택자를 인자로 받아서 그 선택자에 해당되는 Element 객체를 찾아서 리턴
- 하나의 Element만 지정

```
// HTML
<ul>
    <li>HTML</li> // red
    <li class="active">CSS</li> // blue
    <li>JavaScript</li>
</ul>

// JS
var li = document.querySelector('li');
li.style.color = 'red';
var activeLi = document.querySelector('.active');
activeLi.style.color = 'blue';
```

### document.querySelectorAll
- 선택자를 인자로 받아서 그 선택자에 해당되는 Element 객체들을 모두 찾아서 리턴

```
// HTML
<ul>
    <li>HTML</li> // red
    <li class="active">CSS</li> // red
    <li>JavaScript</li> // red
</ul>

// JS
var lis = document.querySelectorAll('li');
for (var name in lis)
    lis[name].style.color = 'red';
```