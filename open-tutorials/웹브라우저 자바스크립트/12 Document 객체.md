# Document 객체
- document 객체는 window 객체의 프로퍼티이므로 정확히는 window.document이나, 생략해서 사용한다
- document 객체의 최상위 자식들은 2개로, 첫번째 자식은 doctype이며, 두번째 자식은 나머지 html 문서 전체이다

```
console.log(document.childNodes); // NodeList(2) [<!DOCTYPE html>, html]
console.log(document.childNodes.length); // 2
console.log(document.childNodes[0]); // <!doctype html>
console.log(document.childNodes[1]); // <html>...</html>
```

## 주요 API

### 노드 생성 API
- document 객체의 주요 임무는 새로운 노드를 생성해 주는 역할이다
	- createElement()
	- createTextNode()

### 문서 정보 API
- document 객체는 문서 그 자체를 나타내기 때문에 문서의 정보에 관한 내용도 프로그래밍적으로 제공한다
	- title
	- URL
	- referrer
	- lastModified

```
console.log(document.title);
```