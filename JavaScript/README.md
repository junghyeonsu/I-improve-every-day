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

## 🤔 자바스크립트가 멀티 스레드 형식으로 동작하게 하는 것?

스레드는 프로세스 내의 실행되는 흐름의 단위입니다.
자바스크립트는 우선 싱글 스레드 형식으로 동작합니다.
그래서 자바스크립트는 한 순간에 하나의 동작밖에 처리를 하지 못합니다.

만약 어떤 동작이 엄청나게 시간이 오래걸리는 동작이라면 해당 동작이 완료될 때 까지 기다려야 하기 때문에 멈춰있는 것 처럼 느껴질 수도 있습니다.

그래서 자바스크립트는 비동기 작업을 통해 긴 작업들을 기다리지 않고 다음 작업들을 수행할 수 있게 합니다.

만약 자바스크립트가 멀티 스레드로 되어있다면, 우리 JS 개발자들은 동시성, 교착 상태와 같은 여러 문제들을 생각하면서 개발 했을겁니다. 하지만 싱글 스레드로 동작하고 비동기로 무거운 동작들을 넘길 수 있게 해줌으로 인해서 개발자들은 복잡한 동시성 문제를 생각하지 않고도 웹 사이트를 만들 수 있습니다.

### 참고

- [개발 공부/Java script
자바스크립트는 왜 싱글 스레드를 선택했을까? 프로세스, 스레드, 비동기, 동기, 자바스크립트 엔진, 이벤트루프](https://miracleground.tistory.com/entry/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EB%8A%94-%EC%99%9C-%EC%8B%B1%EA%B8%80-%EC%8A%A4%EB%A0%88%EB%93%9C%EB%A5%BC-%EC%84%A0%ED%83%9D%ED%96%88%EC%9D%84%EA%B9%8C-%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4-%EC%8A%A4%EB%A0%88%EB%93%9C-%EB%B9%84%EB%8F%99%EA%B8%B0-%EB%8F%99%EA%B8%B0-%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%97%94%EC%A7%84-%EC%9D%B4%EB%B2%A4%ED%8A%B8%EB%A3%A8%ED%94%84)

## 🤔 requestAnimationFrame에 대해서 말해주세요

`requestAnimationFrame`은 브라우저에게 다음 리페인트가 실행되기 전에 해당 애니메이션을 업데이트하는 함수를 호출하게 합니다.

```js
function callback() {
	/* 리페인트 전에 업데이트 되길 원하는 애니메이션 */

	/* requestAnimationFrame 콜백함수가 다시 requestAnimationFrame 호출해야 합니다. */
	window.requestAnimationFrame(callback);
}

// 등록
window.requestAnimationFrame(callback);

// 해제
window.cancelAnimationFrame(callback);
```

### requestAnimationFrame 특징

- 최신 브라우저에서는 해당 탭이 백그라운드로 넘어갔을 때는 동작하지 않도록합니다. (성능최적화)
- 1초에 60번 호출이 기준입니다. 혹은 디스플레이의 Hz를 따릅니다. (그 이상은 인간이 느끼지 못합니다. 그래서 최대한의 부드러움과 최대한의 성능을 이끌어낼 수 있습니다.)
- 다수의 애니메이션에도 각각 타이머 값을 생성 및 참조하지 않고 내부의 동일한 타이머 참조합니다.

### 참고

- [window.requestAnimationFrame() | MDN](https://developer.mozilla.org/ko/docs/Web/API/Window/requestAnimationFrame)
