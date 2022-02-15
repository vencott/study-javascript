# jQuery 객체

## 특성
- $('') 는 jQuery 함수이며 이 함수의 반환값은 jQuery 객체이다
- jQuery 객체는 파라미터와 대응되는 Element들에 대한 정보를 가지고 있으면서 동시에 그 Element들을 제어할 수 있는 메소드나 프로퍼티를 가진 객체이다

```
var li = $('li'); // jQuery 객체 반환
console.log(li);
```

- jQuery 객체의 메소드나 프로퍼티들로 제어 시, jQuery 객체의 모든 Element에 대해서 적용되며, 이를 암시적 반복이라고 한다
- jQuery 메소드는 대체로 두개의 인자를 넘기면 설정(set)이고 하나의 인자만 넘기면 가져오기(get)이다
- 설정할 때는 모든 Element에 대해서 실행되지만, 가져오기 할 때는 유사배열의 제일 첫번째 인자에 해당하는 값만 가져온다

```
var li = $('li');
li.css('text-decoration', 'underline'); // underline 적용 (SET)
li.css('text-decoration'); // "underline solid ..." (GET) --> li[0]의 정보
```

## Element 정보
- jQuery 객체는 유사배열 객체이다
- 그러므로 jQuery 객체의 각 Element 정보를 조회할 때는 배열의 인자에 접근하듯이 한다
- 아무 인자도 설정하지 않으면 기본값으로 첫번째 Element를 가져온다

```
var li = $('li');
li.css('textDecoration'); // default : 0번째
li[0].css('textDecoration'); // 0번째
li[1].css('textDecoration'); // 1번째
li[2].css('textDecoration'); // 2번째

for (var i = 0; i < li.length; i++) // length 프로퍼티 사용 가능(유사배열객체)
    console.log(li[i].constructor); // function HTMLLIElement() { [native code] }
```

- 이때 조회하는 것들은 jQuery 객체가 아닌 DOM 객체이므로 .css() 와 같은 메소드를 사용하지 못한다
- 이를 해결하기 위해선 DOM 객체를 직접 제어하는 방법과 새롭게 jQuery 객체를 얻어오는 방법이 있다

```
for (var i = 0; i < li.length; i++)
    li[i].style.textDecoration = 'underline'; // 각각은 DOM 객체이므로 jQeury 객체 메소드 사용 x

for (var i = 0; i < li.length; i++)
    $(li[i]).css('text-decoration', 'underline'); // 또는 jQuery 함수에 Element 객체를 전달해서 이에 대한 jQuery 객체를 다시 얻어낸 다음 jQuery 메소드를 사용한다
```

- jQuery 함수의 인자
	1. css 선택자를 넘긴다
	2. DOM 객체를 직접 넘긴다

```
$('#id');
$(document.getElementById('id'));
```

## map()

```
var li = $('li');
li.map(function (index, elem) {
    console.log(index, elem);
    $(elem).css('color', 'red');
});
```

- map()은 인자로 함수를 받는다
- map()이 Element들을 하나하나 순회하며 해당 함수를 호출한다
- 함수 호출 시에 첫번째 인자로 index를, 두번째 인자로 DOM 객체를 넘겨준다

## API
- https://api.jquery.com