# JavaScript

## π€ μλ°μ€ν¬λ¦½νΈ μ΄λ²€νΈ λ±λ‘, μ λ¬ λ°©μ, μ΄λ²€ν μ νλ₯Ό λ©μΆλ λ²?

### μ΄λ²€νΈ λ±λ‘

`addEventListener`λΌλ μΉ APIλ₯Ό ν΅ν΄μ μ΄λ²€νΈ λ±λ‘μ ν  μ μμ΅λλ€.

### μ΄λ²€νΈ λ²λΈλ§

> μ΄λ²€νΈ μ ν λ°©μμ€μ νλμλλ€.

μ΄λ²€νΈ λ²λΈλ§μ νΉμ  μμμμ μ΄λ²€νΈκ° λ°μνλ©΄ ν΄λΉ μ΄λ²€νΈκ° λ μμμ νλ©΄ μμλ€λ‘ μ λ¬λλ μλ°μ€ν¬λ¦½νΈ νΉμ±μλλ€.

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
// μ΄λ²€νΈ λ±λ‘
const divs = document.querySelectorAll('div');
divs.forEach(function(div) {
	div.addEventListener('click', logEvent);
});

function logEvent(event) {
	console.log(event.currentTarget.className);
}
```

λ§μ½ μμ κ°μ΄ μ½λ©μ΄ λμ΄μμ λ `three`λ₯Ό ν΄λ¦­νλ©΄ `three`, `two`, `one` μμλλ‘ μ΄λ²€νΈκ° νλμ© λ°μν©λλ€. ν΄λΉ μμλ `three`μ λΆλͺ¨μμκ° μ΄λ²€νΈ λ±λ‘μ΄ λ€ λμ΄μμ΄μ λ°μνλ κ²μλλ€. λ±λ‘μ΄ λμ΄μλ€λ©΄ μ΄λ²€νΈ μ νλ λμ§λ§, λ±λ‘λ μ΄λ²€νΈκ° μμΌλ μ€νμ λμ§ μμ΅λλ€.

### μ΄λ²€νΈ μΊ‘μ²λ§

> μ΄λ²€νΈ λ²λΈλ§κ³Ό λ°λλλ κ²μΌλ‘ μμ μμμμ νμ μμλ‘ μ΄λ²€νΈκ° μ νλλ λ°©μμλλ€.

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
		capture: true // default κ°μ falseμλλ€.
	});
});

function logEvent(event) {
	console.log(event.currentTarget.className);
}
```

μμ κ°μ΄ μμ λ `addEventListener`μ μμ±μΌλ‘ `capture` μμ±μ `true`λ‘ μ£Όκ²λλ©΄ λ²λΈλ§μ΄ μλ μΊ‘μ²λ§μΌλ‘ λμν©λλ€.

ν΄λΉ κ²½μ°μλ `three`λ₯Ό ν΄λ¦­ν΄λ `one` - `two` - `three` μμλ‘ μ΄λ²€νΈλ₯Ό μ νν΄ λκ°λλ€.

### event.stopPropagation()

> μ΄λ²€νΈ μ νλ₯Ό λ©μΆκ³  μΆμ λ μ¬μ©ν  μ μλ μΉ APIμλλ€.

μ΄λ²€νΈλ‘ λκ²¨μ£Όλ μ½λ°± ν¨μμ λ£μ΄μ μ¬μ©ν  μ μμ΅λλ€.

```js
function logEvent(event) {
	event.stopPropagation();
}
```

μμ κ°μ΄ μ¬μ©νκ² λλ©΄ λ²λΈλ§μΌ λλ `three`λ§, μΊ‘μ²λ§μΌ λλ `one` λ§ μ°νκ² λ©λλ€.

#### μΆκ° (preventDefaultμμ μ°¨μ΄μ )

`stopPropagtaion`μ μ΄λ²€νΈ μ ν(λ²λΈλ§, μΊ‘μ²λ§)μ λ©μΆκ³  μΆμ λ μ¬μ©νλ μΉ APIμλλ€.

`event.preventDefault`λ ν΄λΉ μ΄λ²€νΈλ₯Ό λΆμ°©ν μμ κΈ°μμ κΈ°λ³Έμ μΈ μ΄λ²€νΈ(μ²΄ν¬ λ°μ€μ μ²΄ν¬, formμμ buttonμ΄ μμ λ μλμ μΌλ‘ submit μ΄λ²€νΈκ° μΌμ΄λλ κ²)λ€μ μΌμ΄λμ§ μλλ‘ νλ μ­ν μ ν©λλ€.

`event.preventDefault`μ νΈμΆνλ€κ³  ν΄μ ν΄λΉ μ΄λ²€νΈλ₯Ό λΆμ¬μ€ μμμμ μ΄λ²€νΈ μ νκ° λ©μΆμ§λ μμ΅λλ€. κ·Έλ¦¬κ³  `EventTarget.dispatchEvent()`κ³Ό κ°μ μ»€μ€ν μ΄λ²€νΈλ‘ μ λ¬νλ μ΄λ²€νΈ λν λ§νμ§ μμ΅λλ€.

### event delegation (μ΄λ²€νΈ μμ)

> νμ μμμ μ λΆ μ΄λ²€νΈλ₯Ό λΆμ΄λ κ²μ΄ μλλΌ μμ μμμ μ΄λ²€νΈλ₯Ό λΆμ¬λκ³  νμ μμλ₯Ό μ μ΄νλ λ°©μμ μ½λ© ν¨ν΄

λ§μ½ λ¦¬μ€νΈλ₯Ό λ§λ λ€κ³  νλ©΄ `li`μ λͺ¨λ  ν΄λ¦­ μ΄λ²€νΈλ₯Ό λΆμ΄λ μμΌλ‘ μ½λ©μ ν  μ μμ΅λλ€. νμ§λ§ κ·Έλ κ² νλ©΄ λ¦¬μ€νΈ μμ΄νμ΄ μλ‘ μΆκ° λμμ λ ν΄λΉ μμ΄νλ μ΄λ²€νΈλ₯Ό λ€μ λΆμ¬μ£Όμ΄μΌ νλλ° κ½€λ λ²κ±°λ‘­μ΅λλ€.

κ·Έλμ λΆλͺ¨μΈ `ul`(or `ol`)μ ν΄λ¦­ μ΄λ²€νΈλ₯Ό λΆμ΄κ³ , νμ μμμΈ `li`λ€μ μ μ΄ν  μ μμ΅λλ€. λ§μ½ ν΄λ¦­ν `li`μ μ λ³΄λ₯Ό κ°μ§κ³  μ€κ³  μΆλ€λ©΄ μλ°μ€ν¬λ¦½νΈ DOM APIμ€μμ `closest` λ©μλλ₯Ό μ νμ©νλ©΄ ν΄λ¦­ν `li`μ κ²°κ³Όλ₯Ό κ°μ Έμ¬ μ μμ΅λλ€.

### μ°Έκ³ 

- [μ΄λ²€νΈ λ²λΈλ§, μ΄λ²€νΈ μΊ‘μ² κ·Έλ¦¬κ³  μ΄λ²€νΈ μμκΉμ§ | μΊ‘ν΄νκ΅](https://joshua1988.github.io/web-development/javascript/event-propagation-delegation/)
- [Event PreventDefault | MDN](https://developer.mozilla.org/ko/docs/Web/API/Event/preventDefault)

## π€ μλ°μ€ν¬λ¦½νΈκ° λ©ν° μ€λ λ νμμΌλ‘ λμνκ² νλ κ²?

μ€λ λλ νλ‘μΈμ€ λ΄μ μ€νλλ νλ¦μ λ¨μμλλ€.
μλ°μ€ν¬λ¦½νΈλ μ°μ  μ±κΈ μ€λ λ νμμΌλ‘ λμν©λλ€.
κ·Έλμ μλ°μ€ν¬λ¦½νΈλ ν μκ°μ νλμ λμλ°μ μ²λ¦¬λ₯Ό νμ§ λͺ»ν©λλ€.

λ§μ½ μ΄λ€ λμμ΄ μμ²­λκ² μκ°μ΄ μ€λκ±Έλ¦¬λ λμμ΄λΌλ©΄ ν΄λΉ λμμ΄ μλ£λ  λ κΉμ§ κΈ°λ€λ €μΌ νκΈ° λλ¬Έμ λ©μΆ°μλ κ² μ²λΌ λκ»΄μ§ μλ μμ΅λλ€.

κ·Έλμ μλ°μ€ν¬λ¦½νΈλ λΉλκΈ° μμμ ν΅ν΄ κΈ΄ μμλ€μ κΈ°λ€λ¦¬μ§ μκ³  λ€μ μμλ€μ μνν  μ μκ² ν©λλ€.

λ§μ½ μλ°μ€ν¬λ¦½νΈκ° λ©ν° μ€λ λλ‘ λμ΄μλ€λ©΄, μ°λ¦¬ JS κ°λ°μλ€μ λμμ±, κ΅μ°© μνμ κ°μ μ¬λ¬ λ¬Έμ λ€μ μκ°νλ©΄μ κ°λ° νμκ²λλ€. νμ§λ§ μ±κΈ μ€λ λλ‘ λμνκ³  λΉλκΈ°λ‘ λ¬΄κ±°μ΄ λμλ€μ λκΈΈ μ μκ² ν΄μ€μΌλ‘ μΈν΄μ κ°λ°μλ€μ λ³΅μ‘ν λμμ± λ¬Έμ λ₯Ό μκ°νμ§ μκ³ λ μΉ μ¬μ΄νΈλ₯Ό λ§λ€ μ μμ΅λλ€.

### μ°Έκ³ 

- [κ°λ° κ³΅λΆ/Java script
μλ°μ€ν¬λ¦½νΈλ μ μ±κΈ μ€λ λλ₯Ό μ ννμκΉ? νλ‘μΈμ€, μ€λ λ, λΉλκΈ°, λκΈ°, μλ°μ€ν¬λ¦½νΈ μμ§, μ΄λ²€νΈλ£¨ν](https://miracleground.tistory.com/entry/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EB%8A%94-%EC%99%9C-%EC%8B%B1%EA%B8%80-%EC%8A%A4%EB%A0%88%EB%93%9C%EB%A5%BC-%EC%84%A0%ED%83%9D%ED%96%88%EC%9D%84%EA%B9%8C-%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4-%EC%8A%A4%EB%A0%88%EB%93%9C-%EB%B9%84%EB%8F%99%EA%B8%B0-%EB%8F%99%EA%B8%B0-%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%97%94%EC%A7%84-%EC%9D%B4%EB%B2%A4%ED%8A%B8%EB%A3%A8%ED%94%84)

## π€ requestAnimationFrameμ λν΄μ λ§ν΄μ£ΌμΈμ

`requestAnimationFrame`μ λΈλΌμ°μ μκ² λ€μ λ¦¬νμΈνΈκ° μ€νλκΈ° μ μ ν΄λΉ μ λλ©μ΄μμ μλ°μ΄νΈνλ ν¨μλ₯Ό νΈμΆνκ² ν©λλ€.

```js
function callback() {
	/* λ¦¬νμΈνΈ μ μ μλ°μ΄νΈ λκΈΈ μνλ μ λλ©μ΄μ */

	/* requestAnimationFrame μ½λ°±ν¨μκ° λ€μ requestAnimationFrame νΈμΆν΄μΌ ν©λλ€. */
	window.requestAnimationFrame(callback);
}

// λ±λ‘
window.requestAnimationFrame(callback);

// ν΄μ 
window.cancelAnimationFrame(callback);
```

### requestAnimationFrame νΉμ§

- μ΅μ  λΈλΌμ°μ μμλ ν΄λΉ ν­μ΄ λ°±κ·ΈλΌμ΄λλ‘ λμ΄κ°μ λλ λμνμ§ μλλ‘ν©λλ€. (μ±λ₯μ΅μ ν)
- 1μ΄μ 60λ² νΈμΆμ΄ κΈ°μ€μλλ€. νΉμ λμ€νλ μ΄μ Hzλ₯Ό λ°λ¦λλ€. (κ·Έ μ΄μμ μΈκ°μ΄ λλΌμ§ λͺ»ν©λλ€. κ·Έλμ μ΅λνμ λΆλλ¬μκ³Ό μ΅λνμ μ±λ₯μ μ΄λμ΄λΌ μ μμ΅λλ€.)
- λ€μμ μ λλ©μ΄μμλ κ°κ° νμ΄λ¨Έ κ°μ μμ± λ° μ°Έμ‘°νμ§ μκ³  λ΄λΆμ λμΌν νμ΄λ¨Έ μ°Έμ‘°ν©λλ€.

### μ°Έκ³ 

- [window.requestAnimationFrame() | MDN](https://developer.mozilla.org/ko/docs/Web/API/Window/requestAnimationFrame)


## π€ μλ°μ€ν¬λ¦½νΈ μ΄λ²€νΈ λ£¨νμ μ½λ°± νμ λν΄μ

> μλ°μ€ν¬λ¦½νΈλ μ±κΈ μ€λ λμ΄κ³ , νλμ νΈμΆ μ€νλ§μ μ¬μ©νκ³  μμ²­λ€μ΄ λκΈ°μ μΌλ‘ μ²λ¦¬λ©λλ€. κ·Έλμ ν° λ€νΈμν¬ μμ²­μ κΈ°λ€λ¦¬μ§ μκ³  νλ‘κ·Έλ¨μ μννκΈ° μν΄ λΉλκΈ°λ₯Ό μ΄μ©ν΄ μ²λ¦¬ν  μ μμ΅λλ€. λΉλκΈ° μ²λ¦¬λ μ΄λ€μμΌλ‘ μ΄λ£¨μ΄μ§κΉμ?

μ΄λ²€νΈ λ£¨νμ μ½λ°± νμ κ°λμ μ΄μ©ν΄μ λΉλκΈ°λ₯Ό κ΅¬ννκ³  μμ΅λλ€. μκΈ°μ μ§κ³  λμ΄κ°μΌ νλ λΆλΆμ μλ°μ€ν¬λ¦½νΈκ° 'λ¨μΌ μ€λ λ' κΈ°λ°μ μΈμ΄λΌλ λ§μ 'μλ°μ€ν¬λ¦½νΈ μμ§μ΄ λ¨μΌ νΈμΆ μ€νμ μ¬μ©νλ€'λ κ΄μ μμλ§ μ¬μ€μλλ€. μ€μ  μλ°μ€ν¬λ¦½νΈκ° κ΅¬λλλ νκ²½(λΈλΌμ°μ , Node.jsλ±)μμλ μ£Όλ‘ **μ¬λ¬ κ°μ μ€λ λ** κ° μ¬μ©λλ©°, μ΄λ¬ν κ΅¬λ νκ²½μ΄ **λ¨μΌ νΈμΆ μ€νμ μ¬μ©νλ μλ° μ€ν¬λ¦½νΈ μμ§κ³Ό μνΈ μ°λνκΈ° μν΄ μ¬μ©νλ μ₯μΉ** κ° λ°λ‘ 'μ΄λ²€νΈ λ£¨ν'μΈ κ²μλλ€.

μ°λ¦¬κ° μ¬μ©ν `setTimeout`μ΄λ `Promise`κ³Ό κ°μ μ½λκ° μ€νλλ©΄ ν΄λΉ μ½λλ€μ **μ½λ°± ν** λΌλ κ³³μ λ΄κΈ°κ² λκ³ , μ΄ μ½λ°± νμ λ΄κΈ΄ μμλ€μ **μλ°μ€ν¬λ¦½νΈμ μ½ μ€ν**μ΄ λ€ λΉμ΄μ‘λ€λ©΄ **μ΄λ²€νΈ λ£¨ν**μ μν΄μ μ½ μ€νμ μ¬λΌκ°κ³  μ€νμ΄ λ©λλ€.

μ΄ λ μ½λ°± νμλ νμ€ν¬ ν, λ§μ΄ν¬λ‘νμ€ν¬ ν, μ λλ©μ΄μ νλ μμ΄λΌλ μΈ κ°μ§μ νλ‘ μ΄λ£¨μ΄μ Έ μμ΅λλ€. κ°κ°μ νμλ μ°μ μμμ λ΄λ μΌμ΄ λ€λ¦λλ€.

μ°μ μμλ **λ§μ΄ν¬λ‘νμ€ν¬ ν > μ λλ©μ΄μ νλ μs > νμ€ν¬ ν** μμΌλ‘ λμ΅λλ€.

- λ§μ΄ν¬λ‘νμ€ν¬ νμλ `Promise`κ³Ό κ°μ μμλ€μ΄ λ€μ΄κ°λλ€.
- μ λλ©μ΄μ νλ μ νμλ `requestionAnimationFrame`μ λ€μ΄κ° μ½λλ€μ΄ λ€μ΄κ°λλ€.
- νμ€ν¬ νμλ `setTimeout`κ³Ό κ°μ μ½λλ€μ΄ λ€μ΄κ°λλ€.

### μ°Έκ³ 

- [μλ°μ€ν¬λ¦½νΈμ μ΄λ²€νΈ λ£¨ν](https://meetup.toast.com/posts/89)
- [[μ΄λ²€νΈ λ£¨ν(2/2)] μ¬λ¬λΆμ μ΄μ  JSλ₯Ό μκ² λμ΅λλ€ | γγγγππ](https://www.youtube.com/watch?v=S1bVARd2OSE)
