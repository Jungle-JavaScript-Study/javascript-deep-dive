## 1. strict mode의 필요성
### 암묵적 전역 implicit global

```js
function foo() {
  x = 10;
}
foo();

console.log(x);

```

- 선언하지 않은 변수에 값을 할당하면 암묵적으로 전역 객체에 프로퍼티로 동적으로 생성하고 전역 변수처럼 사용할 수 있게 된다. 이러한 현상을 암묵적 전역이라고 한다.
- 오류를 발생시킬 가능성이 크다.
- 이러한 잠재적인 오류를 발생시키기 어려운 개발 환경을 만들어 주기 위해 ES5부터 strict modee가 추가되었다.

<br/>

## 2. strict mode
- JS 언어의 문법을 좀 더 엄격히 적용하여 오류를 발생시킬 가능성이 높거나
- JS 엔진의 최적화 작업에 문제를 일으킬 수 있는 코드에 대해 명시적인 에러를 발생시킨다.
- ES6에서 도입된 클래스와 모듈은 기본적으로 strict mode가 적용된다.

<br/>

## 3. strict mode 적용하는 방법
### JavaScript
- 전역의 선두 또는 함수 몸체의 선두에 `'use strict';`를 추가한다.
- 전역의 선두에 추가하면 스크립트 전체에 strict mode가 적용된다.
- 외부 라이브러리를 사용하는 경우, 라이브러리가 non-strict mode인 경우도 있기 때문에 전역에 strict mode를 적용하는 것은 바람직하지 않다.
  - 즉시 실행 함수로 스크립트 전체를 감싸서 스코프를 구분하고 즉시 실행 함수의 선두에 strict mode를 적용해야 한다.
- strict mode가 적용된 함수가 참조할 함수 외부의 컨텍스트에 strict mode를 적용하지 않으면 문제가 발생할 수 있다.
  - 마찬가지로 즉시 실행 함수로 감싼 스크립트 단위로 적용하는 것이 바람직하다.


### React
- React에서 제공하는 StrictMode 태그를 사용하여 감싼 영역에 strict mode가 적용된다.
https://react.dev/reference/react/StrictMode

### Next.js
- Next.js 13.4부터는 기본적으로 Strict Mode가 활성화된다.
- next.config.js에서 reactStrictMode의 값을 변경해 설정할 수 있다.
https://nextjs.org/docs/app/api-reference/next-config-js/reactStrictMode

<br/>

## 4. strict mode가 발생시키는 에러
- 선언하지 않은 변수(암묵적 전역)을 참조하면 ReferenceError가 발생한다.
- delete 연산자로 변수, 함수, 매개변수를 삭제하면 SyntaxError가 발생한다.
- 중복된 매개변수 이름을 사용하면 SyntaxError가 발생한다.
- with문을 사용하면 SyntaxError가 발생한다.

<br/>

## 5. strict mode 적용에 의한 변화
### JavaScript
- 함수를 일반 함수로서 호출했을 때 this에 바인딩 되는 값이 전역 객체가 아닌 undefined가 바인딩된다.
- 매개변수로 전달 받은 인수를 재할당하여 변경해도 arguments 객체에는 반영되지 않는다.

### React
- 컴포넌트가 추가로 한 번 더 렌더링되어 불순한 렌더링에 의해 발생하는 버그를 찾는 데 도움을 준다.
- useEffect가 추가로 한 번 더 실행되어 Effect 정리가 누락되어 발생하는 버그를 찾는 데 도움을 준다.
- deprecated된 API를 사용하고 있지는 않은 지 확인한다.
https://react.dev/reference/react/StrictMode
