# Frontend

## 🤔 Critical Rendering Path ?

> 읽은 글들
> [MDN](https://developer.mozilla.org/ko/docs/Web/Performance/Critical_rendering_path)

중요 렌더링 경로 (Critical Rendering Path)는 브라우저가 HTML, CSS, Javascipt를 화면에 픽셀로 변화하는 일련의 단계를 말하며 이를 최적화하는 것은 렌더링 성능을 향상시킵니다. 중요 렌더링 경로는 Document Object Model (DOM), CSS Object Model (CSSOM), 렌더 트리 그리고 레이아웃을 포함합니다. (MDN)

브라우저에서 HTML 받고, CSS 읽고, JS 읽고 웹 사이트가 유저의 이벤트에 반응하기 까지 (인터렉션이 가능하기 전까지)의 과정들을 중요 렌더링 경로라고합니다. (쉽게 말해서 브라우저에서 웹 사이트를 띄우기 까지의 경로라고 보면 됩니다.)

웹 성능을 개선하기 위해서는 이 **중요 렌더링 경로**를 개선해야 합니다. 사실 이 과정 사이에서는 엄청나게 많은 과정들이 있고, 개선 방법이 있습니다.

대표적으로 HTML을 파싱이 일어날 때 중간에 HTML 파싱을 막는 동작이 있을 수 있습니다. (HTML 파싱을 막는 리소스를 **블록 리소스**라고 부릅니다.) 블록 리소스는 페인트 과정을 지연시키므로, HTML 파싱을 막는 상황이 발생하지 않도록 해야 하는데, CSS를 불러오는 link 태그를 head 태그 아래에 위치시킨다던가, JS를 불러오는 script 태그를 body의 제일 아래에 위치시키는 방법이 대표적입니다.
