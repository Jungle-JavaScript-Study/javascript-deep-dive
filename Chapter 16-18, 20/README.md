# 16장 프로퍼티 어트리뷰트

### Q1. 데이터 프로퍼티의 프로퍼티 어트리뷰트 4개

<details>
<summary>정답</summary>

데이터 프로퍼티는 키와 값으로 구성된 일반적인 프로퍼티로, 
<br/>
- 프로퍼티 값에 접근하면 반환되는 값인 `[[Value]]`
- 값의 변경 가능 여부를 나타내는 `[[Writable]]`,
- 열거 가능 여부를 나타내는 `[[Enumerable]]`,
- 재정의 가능 여부를 나타내는 `[[Configurable]]`이 있습니다.

</details>

<br/>


### Q2. 프로퍼티가 생성될 때 데이터 프로퍼티의 각 프로퍼티 어트리뷰트는 어떤 값으로 초기화되나요?

<details>
<summary>정답</summary>

`[[Value]]`의 값은 프로퍼티 값으로 초기화되며 나머지는 true로 초기화됩니다.

</details>

<br/>


### Q3. 접근자 프로퍼티의 프로퍼티 어트리뷰트 4개

<details>
<summary>정답</summary>

접근자 프로퍼티는 다른 데이터 프로퍼티의 값을 읽거나 저장할 때 사용하는 접근자 함수로 구성된 프로퍼티로, 
<br/>
- 접근자 프로퍼티를 통해 프로퍼티 값을 읽을 때 호출되는 접근자 함수인 `[[Get]]`
- 접근자 프로퍼티를 통해 프로퍼티 값을 저장할 때 호출되는 접근자 함수인 `[[Set]]`
- 열거 가능 여부를 나타내는 `[[Enumerable]]`,
- 재정의 가능 여부를 나타내는 `[[Configurable]]`이 있습니다.

</details>

<br/>


### Q4. JavaScript에서 객체의 변경을 방지하는 메서드에는 어떤 게 있나요?

<details>
<summary>정답</summary>

-  프로퍼티의 추가를 금지하는 `Object.preventExtensions`
- 객체를 밀봉해 읽기와 쓰기만 가능하게 하는 `Object.seal`
- 객체를 동결해 읽기만 가능하게 하는 `Object.freeze` 메서드가 있습니다.

</details>

<br/>

### Q4-1. 위 메서드를 사용해 변경을 방지한 객체의 중첩 객체는 변경이 가능한가요?

<details>
<summary>정답</summary>

ㅇㅇ 위 메서드들은 중첩 객체까지는 영향을 주지 못하기 때문에 중첩 객체는 변경이 가능합니다.
<br/>
객체의 중첩 객체까지 변경이 불가능하게 하려면 객체를 값으로 갖는 모든 프로퍼티에 대해 재귀적으로 변경을 방지하는 메서드를 호출해야 합니다.

</details>

<br/>

# 17장 생성자 함수에 의한 객체 생성

### Q5. 생성자 함수는 어떤 함수인가요?

<details>
<summary>정답</summary>

new 연산자와 함께 호출하여 객체(인스턴스)를 생성하는 함수입니다.

</details>

<br/>

### Q6. 생성자 함수에 의해 생성된 객체를 부르는 용어는 무엇인가요?

<details>
<summary>정답</summary>

인스턴스

</details>

<br/>

### Q7. 객체를 생성할 때, 객체 리터럴을 사용하지 않고 생성자 함수로 생성하는 것이 더 유리한 상황은 언제인가요?

<details>
<summary>정답</summary>

프로퍼티 구조가 동일한 객체 여러 개를 생성할 때는 생성자 함수를 사용하는 것이 더 간편합니다.

</details>

<br/>

### Q8. 생성자 함수를 정의하는 방법을 설명해주세요.

<details>
<summary>정답</summary>

일반 함수와 동일한 방법으로 정의하고 new 연산자와 함께 호출합니다.

</details>

<br/>

### Q9. 생성자 함수를 new 연산자 없이 호출하면 어떻게 동작하나요?

<details>
<summary>정답</summary>

일반 함수로 동작합니다.

</details>

<br/>

### Q9-1. JavaScript의 빌트인 생성자 함수인 String, Number, Boolean 생성자 함수를 new 연산자 없이 호출하면 어떻게 동작하나요?

<details>
<summary>정답</summary>

객체가 아닌 문자열, 숫자, 불리언 값을 반환합니다.

</details>

<br/>

### Q10. 생성자 함수로서 호출할 수 있는 함수와 그럴 수 없는 함수는 어떻게 구분되나요?

<details>
<summary>정답</summary>

함수 정의 방식에 따라 구분됩니다. 
<br/>
함수 선언문, 함수 표현식, 클래스는 생성자 함수로서 호출될 수 있는 constructor이고,
<br/>
ES6의 메서드 축약 표현으로 작성된 메서드, 화살표 함수는 non-constructor입니다.

</details>

<br/>

### Q11. 생성자 함수 내부의 this에 값이 최초로 바인딩 되는 시점은 언제이고, 어떤 값이 바인딩 되나요?

<details>
<summary>정답</summary>

생성자 함수 몸체의 코드가 실행되는 런타임 이전에 암묵적으로 생성된 빈 객체가 this에 바인딩됩니다.

</details>

<br/>



### Q12. 생성자 함수 내부의 this는 무엇을 가리키나요?

<details>
<summary>정답</summary>

생성자 함수가 생성할 인스턴스를 가리킵니다.

</details>

<br/>

### Q12-1. 생성자 함수를 new 연산자 없이 호출했을 때 함수 내부의 this는 무엇을 가리키나요?

<details>
<summary>정답</summary>

전역 객체 window를 가리킵니다.

</details>

<br/>

### Q13. 생성자 함수가 생성자 함수로서 호출되었는지 확인하는 방법을 설명해주세요.

<details>
<summary>정답</summary>

함수 내부에서 new.target을 사용해서 확인할 수 있습니다.
<br/>
생성자 함수로서 호출되면 new.target은 함수 자신을 가리키고,
<br/>
일반 함수로서 호출되면 undefined입니다.

</details>

<br/>

# 18장 함수와 일급 객체

### Q14. 일급 객체가 되는 조건 4개

<details>
<summary>정답</summary>

- 무명의 리터럴로 생성 가능
- 변수나 자료구조(객체, 배열 등)에 저장 가능
- 함수의 매개변수에 전달 가능
- 함수의 반환값으로 사용 가능


</details>

<br/>

### Q14-1. 일급 객체는 어떤 객체를 의미하나요?

<details>
<summary>정답</summary>

일급 객체란 다른 객체들에게 적용 가능한 연산을 모두 지원하는 객체를 말합니다.

</details>

<br/>

### Q15. 함수 호출 시 매개변수의 개수보다 인수를 초과하여 전달한 경우 초과된 인수를 어떻게 확인할 수 있나요?

<details>
<summary>정답</summary>

함수 내부에서 지역 변수처럼 사용할 수 있는 arguments 객체를 통해 확인할 수 있습니다.
<br/>
모든 인수는 암묵적으로 arguments 객체의 프로퍼티로 보관됩니다.

</details>

<br/>

### Q15-1. 위 질문의 답이 되는 기능의 활용 방안을 설명해주세요.

<details>
<summary>정답</summary>

arguments 객체는 
<br/>
매개변수 개수를 확정할 수 없는 가변 인자 함수를 구현할 때 활용할 수 있습니다.

</details>

<br/>

### Q16. arguments 객체의 length 프로퍼티와 함수 객체의 length 프로퍼티는 각각 무엇의 개수를 가리키나요?

<details>
<summary>정답</summary>

arguments 객체의 length 프로퍼티는 인자의 개수를,
<br/>
함수 객체의 length 프로퍼티는 매개변수의 개수를 가리킵니다.

</details>

<br/>

### Q17. prototype 프로퍼티가 없는 함수는 어떤 함수인가요?

<details>
<summary>정답</summary>

non-constructor 함수에는 prototype 프로퍼티가 없습니다.

</details>

<br/>

### Q17-1. prototype 프로퍼티는 무엇을 가리키나요?

<details>
<summary>정답</summary>

생성자 함수가 생성할 인스턴스의 프로토타입 객체를 가리킵니다.

</details>

<br/>

# 20장 strict mode

### Q18. JavaScript에서 strict mode를 적용하는 방법을 설명해주세요.

<details>
<summary>정답</summary>

전역의 선두 또는 함수 몸체의 선두에 `'use strict';`를 추가합니다.

</details>

<br/>

### Q18-1. strict mode가 발생시키는 에러 4개

<details>
<summary>정답</summary>

- 선언하지 않은 변수(암묵적 전역)을 참조하면 ReferenceError가 발생합니다.
- delete 연산자로 변수, 함수, 매개변수를 삭제하면 SyntaxError가 발생합니다.
- 중복된 매개변수 이름을 사용하면 SyntaxError가 발생합니다.
- with문을 사용하면 SyntaxError가 발생합니다.

</details>

<br/>

### Q18-2. strict mode 적용에 의한 변화 2개

<details>
<summary>정답</summary>

- 함수를 일반 함수로서 호출했을 때 this에 바인딩 되는 값이 전역 객체가 아닌 undefined가 바인딩됩니다.
- 매개변수로 전달 받은 인수를 재할당하여 변경해도 arguments 객체에는 반영되지 않습니다.

</details>

<br/>

### Q19. 프로젝트에서 사용한 라이브러리 혹은 프레임워크에서 strict mode를 설정하는 방법을 설명해주세요.
(React or Next.js 중 사용한 것 기준으로 설명해주세요.)

<details>
<summary>정답</summary>

**React**
<br/>
React에서 제공하는 StrictMode 태그를 사용하여 감싼 영역에 strict mode가 적용됩니다.
<br/>
https://react.dev/reference/react/StrictMode
<br/>
<br/>

**Next.js**
<br/>
Next.js 13.4부터는 기본적으로 Strict Mode가 활성화됩니다.
<br/>
next.config.js에서 reactStrictMode의 값을 변경해 설정할 수 있습니다.
<br/>
https://nextjs.org/docs/app/api-reference/next-config-js/reactStrictMode
</details>

<br/>

### Q19-1. react에서 strict mode를 사용하면 (개발 환경에서) 어떤 동작이 활성화되나요?

<details>
<summary>정답</summary>

- 컴포넌트가 추가로 한 번 더 렌더링되어 불순한 렌더링에 의해 발생하는 버그를 찾는 데 도움을 줍니다.
- useEffect가 추가로 한 번 더 실행되어 Effect 정리가 누락되어 발생하는 버그를 찾는 데 도움을 줍니다.
- deprecated 된 API를 사용하고 있지는 않은 지 확인합니다.
https://react.dev/reference/react/StrictMode

</details>

<br/>
