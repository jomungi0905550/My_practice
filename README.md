# JavaScript 공부 메모

## 10/14 배운 내용 기록

### 쿼리 스트링(Query String)
URL 뒤에 `?`를 붙이고 `키=값` 형태로 데이터를 전달하는 방식이다.

```
https://example.com/search?keyword=coding&page=2
```

- `?` : 쿼리 스트링의 시작을 알리는 기호
- `keyword` : 키(key)
- `coding` : 값(value)
- 여러 개를 보낼 때는 `&`로 연결한다

```js
const params = new URLSearchParams(location.search);
params.get('keyword');   // 'coding'
params.get('page');      // '2'
```

- URL의 쿼리 스트링에서 파라미터(parameter) 값을 읽어올 때 쓰는 코드이다

### form 태그
`method="get"`일 때만 입력한 값을 쿼리 스트링(`?키=값`) 형태로 자동으로 만들어서 서버(`action` 주소)로 전송해 준다.
(`name` 속성이 키가 되고, 입력한 값이 값이 된다.)

### form 안의 button 주의점
- `<button>`의 기본값은 `type="submit"`이라서 form 안에서 누르면 제출된다.
- 제출하지 않고 버튼으로만 사용하려면 `type="button"`을 지정해야 한다.

### a 태그
`href`에 `?키=값`을 붙이면 데이터도 함께 전달할 수 있다.

```html
<a href="detail.html?id=101">
  <img src="notebook.jpg" alt="노트북">
</a>
```

### DOM 요소 선택

| 메서드 | 반환 | 라이브/정적 | 사용 가능 |
|---|---|---|---|
| `document.getElementsByClassName` | HTMLCollection | 라이브 | for, for...of |
| `document.querySelectorAll` | NodeList | 정적(static) | forEach, for, for...of |
| `document.querySelector` | 요소 1개 (없으면 null) | - | - |

- **HTMLCollection**: 유사배열이라 `map`, `filter`, `reduce`를 사용할 수 없다 → 배열로 변환해야 한다
  - `Array.from(collection)` 또는 `[...collection]`
- **라이브(live)**: 요소가 추가/삭제되면 목록 개수가 실시간으로 바뀐다 → 반복 중 수정 시 주의
- **NodeList**: 정적이라 값이 고정되고, `forEach`는 가능하지만 `map`, `filter`는 불가 → 똑같이 배열로 변환해서 사용한다
- `query`가 붙은 메서드만 **CSS 선택자**를 사용할 수 있다

```js
document.getElementsByClassName('item');   // 점 없이 이름만
document.querySelector('.item');           // CSS 선택자라 점 필요
```

### 요소 생성과 클래스 부여
```js
const element_div = document.createElement('div');
element_div.className = 'item';   // 클래스 부여 (기존 클래스는 덮어씀)
```

### data 속성 (dataset)
`value`와 별개로 부가 정보를 담고 싶을 때 `data-이름` 속성을 쓴다.

```html
<input type="text" name="x" value="hello" data-x="x01_txt">
```
```js
const input_x = document.querySelector("input[name='x']");
demo.textContent = input_x.dataset.x;   // 'x01_txt' (data-x의 x 부분)
```

### 동기 / 비동기
- **동기**: 앞 작업이 끝나야 다음 작업을 실행한다. 서버 응답이 늦어지면 전체가 멈추고, 걸리는 시간도 보장되지 않는다.
- **비동기**: 시간이 걸리는 작업을 기다리지 않고 다음 코드를 먼저 실행한다. 통신 작업에서 많이 쓴다.

```js
setTimeout(콜백함수, 시간);   // 시간 단위는 ms (1000 = 1초)
```

### JSON
- 정체는 **문자열**이다. 모양은 JS 객체와 비슷하며, 키도 큰따옴표로 감싼다.
- 보낼 때는 문자열, 받을 때는 객체로 바꿔서 쓴다.
- JSON 형식이 맞아야 변환(파싱)이 가능하다.

```js
JSON.stringify(객체);   // 객체 → JSON 문자열
JSON.parse(json);      // JSON 문자열 → 객체
```

## 복습하면서 새로 알게 된 것
- **요소**: 시작 태그 + 속성 + 내용 + 끝 태그를 전부 합친 덩어리이다.
- `document.createElement('div')`의 인수에는 **태그 이름**을 넣는다.
  - `'item'`처럼 없는 태그 이름을 넣으면 `<item></item>`이 만들어진다.
  - `'.item'`처럼 선택자를 넣으면 오류가 난다.





