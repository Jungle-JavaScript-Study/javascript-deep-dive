# 39.7장 ~ DOM

### Q1. HTML 어트리뷰트와 DOM 프로퍼티의 차이 (관리하는 상태 관점에서)

<details>
<summary>정답</summary>

- HTML 어트리뷰트의 역할은 HTML 요소의 초기 상태를 지정하는 것으로, HTML 어트리뷰트의 값은 HTML 요소의 초기 상태를 의미하며 변하지 않습니다.
- 사용자가 입력한 최신 상태는 HTML 어트리뷰트에 대응하는 요소 노드의 DOM 프로퍼티가 관리합니다.

</details>

<br/>

### Q2. 요소 노드의 최신 상태뿐만 아니라 초기 상태도 관리해야 하는 이유는?

<details>
<summary>정답</summary>

- 웹페이지를 처음 표시하거나 새로고침할 때 초기 상태를 표시해야 하기 때문입니다.

</details>

<br/>

### Q3. 사용자 정의 어트리뷰트를 만드는 방법

<details>
<summary>정답</summary>

- data 어트리뷰트와 dataset 프로퍼티를 사용합니다.
- data 어트리뷰트는 data- 접두사 다음에 임의의 이름을 붙여서 사용합니다.
- 이 어트리뷰트의 값은 dataset 프로퍼티로 취득할 수 있습니다.

</details>

<br/>

### Q4. HTMLElement.prototype.style 프로퍼티를 통해 width 프로퍼티에 값을 할당할 때 `단위를 생략하면` 어떻게 작동하나요?

```js
$div.style.width = '100';
```

<details>
<summary>정답</summary>

- 해당 CSS 프로퍼티가 적용되지 않습니다.
- 단위 지정이 필요한 CSS 프로퍼티의 값은 반드시 단위를 지정해야 합니다.

</details>

<br/>

### Q5. HTML 요소에 인라인, 클래스, 상속 등을 통해 적용된 모든 CSS 스타일을 참조하는 방법은?

<details>
<summary>정답</summary>

- `window.getComputedStyle` 메서드를 사용하면,
인수로 전달한 요소 노드에 적용되어 있는 평가된 스타일을 CSSStyleDeclaration 객체에 담아 반환합니다.

</details>

<br/>

### Q6. HTML과 DOM 표준은 어디서 만드나요?

<details>
<summary>정답</summary>

- WHATWG
- https://zdnet.co.kr/view/?no=20190531184644
  
</details>

<br/>

# 40장 이벤트

### Q7. 이벤트 드리븐 프로그래밍이란?

<details>
<summary>정답</summary>

<br/>

- 브라우저에서는 이벤트와 이벤트 핸들러를 통해 사용자와 애플리케이션이 상호작용 할 수 있는데,
이와 같이 프로그램의 흐름을 이벤트 중심으로 제어하는 프로그래밍 방식을 이벤트 드리븐 프로그래밍이라고 합니다.

</details>

<br/>

### Q8. 마우스 이벤트 타입 중 mouseenter와 mouseover의 차이

<details>
<summary>정답</summary>

<br/>

- mouseenter는 이벤트가 버블링되지 않고, mouseover는 버블링됩니다.

</details>

<br/>

### Q9. 값 변경 이벤트 타입 중 input과 change의 차이 (발생 시점 관점에서)

<details>
<summary>정답</summary>

<br/>

- 사용자가 입력을 하고 있을 때는 input 이벤트가 발생하고,
- 사용자 입력이 종료되어 값이 변경되면 change 이벤트가 발생합니다.

</details>

<br/>

### Q10. event listener란?

<details>
<summary>정답</summary>

<br/>

- event listener === event handler
- 이벤트 핸들러는 이벤트가 발생했을 때 브라우저에 호출을 위임한 함수로, 이벤트가 발생하면 브라우저에 의해 호출됩니다.

</details>

<br/>

### Q11. 이벤트 핸들러를 등록하는 방법 3가지

<details>
<summary>정답</summary>

<br/>

- 이벤트 핸들러 어트리뷰트 값으로 함수 호출문 등의 문을 할당하는 방법
- 이벤트 핸들러 프로퍼티에 함수를 바인딩하는 방법
- addEventListener 메서드를 사용해 매개변수로 이벤트 핸들러를 전달하는 방법

</details>

<br/>

### Q12. 이벤트 핸들러를 제거하는 방법 2가지

<details>
<summary>정답</summary>

<br/>

- addEventListener 메서드로 등록한 이벤트 핸들러는 removeEventListenr 메서드로 제거합니다.
- 이벤트 핸들러 프로퍼티 방식으로 등록한 이벤트 핸들러는 프로퍼티에 null을 할당합니다.

</details>

<br/>

### Q13. event propagation이란?

<details>
<summary>정답</summary>

<br/>

- DOM 트리 상에서 존재하는 DOM 요소 노드에서 발생한 이벤트는 DOM 트리를 통해 전파되는데 이를 이벤트 전파(event propagation)라고 합니다.

</details>

<br/>

### Q14. 이벤트 전파 3단계와 각 단계가 전파되는 순서는?

<details>
<summary>정답</summary>

<br/>

- 캡처링 - 타깃 - 버블링 단계로 전파됩니다.

</details>

<br/>

### Q15. capturing phase와 bubbling phase의 차이는?

<details>
<summary>정답</summary>

<br/>

- 캡처링 단계는 이벤트가 상위 요소에서 하위 요소 방향으로 전파되는 것이고
- 버블링 단계는 이벤트가 하위 요소에서 상위 요소 방향으로 전파되는 것입니다.

</details>

<br/>

### Q16. event delegation이란?

<details>
<summary>정답</summary>

<br/>

- 이벤트 위임은 여러 개의 하위 DOM 요소에 동일한 이벤트 핸들러를 등록해야 할 때, 각각 등록하는 대신 하나의 상위 DOM 요소에 이벤트 핸들러를 등록하는 방법입니다.

</details>

<br/>

### Q17. 이벤트 핸들러를 호출할 때 인수로 this를 전달하면 this는 무엇을 가리키나요?

<details>
<summary>정답</summary>

<br/>

- 이벤트를 바인딩한 DOM 요소

</details>

<br/>

### Q18. 이벤트 핸들러 프로퍼티 방식과 addEventListener 메서드 방식으로 이벤트 핸들러를 등록한 경우, 인수를 전달하는 방법

<details>
<summary>정답</summary>

<br/>

- 이벤트 핸들러 내부에서 함수를 호출하면서 인수를 전달하거나
- 이벤트 핸들러를 반환하는 함수를 호출하면서 인수를 전달합니다.

</details>
