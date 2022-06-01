# HTML

## 🤔 innerHTML vs innerText vs textContent

- `innerHTML`

해당 Element의 HTML, XML을 읽어오거나, 설정할 수 있습니다.
정확하게 어떤 마크업으로 되어있는지, 공백이나 줄 띄움을 전부 보고싶다면 해당 속성을 이용하면 됩니다.


- `innerText`

해당 Element 내에서 사용자에게 보여지는 텍스트를 읽거나 설정할 수 있습니다.
그래서 만약 `display: none` 된 요소가 있다면 해당 요소는 읽을 수 없습니다.

`innerText`는 단순한 플레인 텍스트로 긁어옵니다.


- `textContent`

`innerHTML`과 `innerText`는 Element의 속성이라면, `textContent`는 Node의 속성입니다.

`innerText`와는 다르게 `<script>`, `<style>`로 숨겨진 텍스트까지 읽어옵니다.
그래서 만약 해당 요소에 `display: none` 된 요소가 있어도 해당 텍스트를 전부 읽어옵니다.

`innerText`는 렌더링된 모양을 기준으로 긁어오지만, `textContent`는 그렇지 않습니다.
