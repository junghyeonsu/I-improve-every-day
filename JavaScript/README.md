# JavaScript

## 🤔 자바스크립트 이벤트 등록, 전달 방식, 이벤프 전파를 멈추는 법?

### 이벤트 등록

`addEventListener`라는 웹 API를 통해서 이벤트 등록을 할 수 있습니다.

### 이벤트 버블링

> 이벤트 전파 방식중에 하나입니다.

이벤트 버블링은 특정 요소에서 이벤트가 발생하면 해당 이벤트가 더 상위의 화면 요소들로 전달되는 자바스크립트 특성입니다.

```html
<body>
	<div class="one">
		<div class="two">
			<div class="three">
			</div>
		</div>
	</div>
</body>
```

```js
// 이벤트 등록
const divs = document.querySelectorAll('div');
divs.forEach(function(div) {
	div.addEventListener('click', logEvent);
});

function logEvent(event) {
	console.log(event.currentTarget.className);
}
```

만약 위와 같이 코딩이 되어있을 때 `three`를 클릭하면 `three`, `two`, `one` 순서대로 이벤트가 하나씩 발생합니다. 해당 예시는 `three`의 부모요소가 이벤트 등록이 다 되어있어서 발생하는 것입니다. 등록이 되어있다면 이벤트 전파는 되지만, 등록된 이벤트가 없으니 실행은 되지 않습니다.

### 이벤트 캡처링

> 이벤트 버블링과 반대되는 것으로 상위 요소에서 하위 요소로 이벤트가 전파되는 방식입니다.

```html
<body>
	<div class="one">
		<div class="two">
			<div class="three">
			</div>
		</div>
	</div>
</body>
```

```js
const divs = document.querySelectorAll('div');
divs.forEach(function(div) {
	div.addEventListener('click', logEvent, {
		capture: true // default 값은 false입니다.
	});
});

function logEvent(event) {
	console.log(event.currentTarget.className);
}
```

위와 같이 있을 때 `addEventListener`의 속성으로 `capture` 속성을 `true`로 주게되면 버블링이 아닌 캡처링으로 동작합니다.

해당 경우에는 `three`를 클릭해도 `one` - `two` - `three` 순서로 이벤트를 전파해 나갑니다.

### event.stopPropagation()

> 이벤트 전파를 멈추고 싶을 때 사용할 수 있는 웹 API입니다.

이벤트로 넘겨주는 콜백 함수에 넣어서 사용할 수 있습니다.

```js
function logEvent(event) {
	event.stopPropagation();
}
```

위와 같이 사용하게 되면 버블링일 때는 `three`만, 캡처링일 때는 `one` 만 찍히게 됩니다.

### event delegation (이벤트 위임)

> 하위 요소에 전부 이벤트를 붙이는 것이 아니라 상위 요소에 이벤트를 붙여놓고 하위 요소를 제어하는 방식의 코딩 패턴

만약 리스트를 만든다고 하면 `li`에 모든 클릭 이벤트를 붙이는 식으로 코딩을 할 수 있습니다. 하지만 그렇게 하면 리스트 아이템이 새로 추가 되었을 때 해당 아이템도 이벤트를 다시 붙여주어야 하는데 꽤나 번거롭습니다.

그래서 부모인 `ul`(or `ol`)에 클릭 이벤트를 붙이고, 하위 요소인 `li`들을 제어할 수 있습니다. 만약 클릭한 `li`의 정보를 가지고 오고 싶다면 자바스크립트 DOM API중에서 `closest` 메서드를 잘 활용하면 클릭한 `li`의 결과를 가져올 수 있습니다.

### 참고

- [이벤트 버블링, 이벤트 캡처 그리고 이벤트 위임까지 | 캡틴판교](https://joshua1988.github.io/web-development/javascript/event-propagation-delegation/)