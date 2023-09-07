### 49장 제너레이터와 async/await
---

Q1. 제너레이터(Generator)란 무엇이며 어떻게 동작하나요?


<details><summary> 정답
</summary>
코드 블록의 실행을 일시 중지 했다가 필요한 시점에 재개할 수 있는 특수한 함수 입니다.
</details>


Q2. 제너레이터와 일반 함수의 차이점은 무엇인가요?

<details><summary> 정답
</summary>
- 제너레이터 함수는 함수 호출자에게 함수 실행의 제어권을 양고할 수 있습니다.
- 제너레이터 함수는 함수 호출자와 함수의 상태를 주고받을 수 있습니다.
- 제너레이터 함수를 호출하면 제너레이터 객체를 반환합니다.
</details>

Q3. 제너레이터 함수를 선언할 때 어떤 키워드를 사용하나요?

<details><summary> 정답
</summary>
function* 키워드를 사용하여 제너레이터 함수를 선언합니다.
</details>

Q4. 제너레이터 객체의 세 개의 메서드 (next,return,throw)를 호출하면 어떻게 동작하나요?

```javascript
function* generateNumbers() {
  yield 1;
  yield 2;
  yield 3;
  yield 4;
  yield 5;
}

const numberGenerator = generateNumbers();

console.log(numberGenerator.next().value); // 1
console.log(numberGenerator.next().value); // 2
console.log(numberGenerator.next().value); // 3
console.log(numberGenerator.next().value); // 4
console.log(numberGenerator.next().value); // 5
console.log(numberGenerator.next().value); // undefined
```
❓ 위의 코드에서 generateNumbers 함수는 제너레이터 함수로 선언되었습니다. 
<details><summary> 정답
</summary>
next() 메서드:
**next()** 메서드는 제너레이터 함수 내의 다음 yield 문까지 실행하고, 해당 yield 문에서 반환된 값을 가지고 있는 객체를 반환합니다.
각 next() 호출마다 제너레이터 함수가 실행되며, yield 문까지 실행되고 해당 yield 문에서 반환된 값을 value 프로퍼티로 가지고 있는 객체가 반환됩니다.
done 프로퍼티는 제너레이터 함수가 끝났을 때 true가 됩니다.
return() 메서드:

**return()** 메서드는 제너레이터 함수를 종료하고, 제너레이터의 마지막 yield 문에서 지정된 값을 반환합니다.
제너레이터 함수를 종료하므로 이후의 next() 호출은 더 이상 값을 생성하지 않습니다.
throw() 메서드:

**throw()** 메서드는 제너레이터 함수 내에서 예외를 발생시킵니다. 이것은 제너레이터 함수의 실행을 중단하고 예외를 던집니다.
제너레이터 함수 내에서 try...catch 블록을 사용하여 예외를 처리할 수 있습니다.
</details>

Q5. async/await 키워드는 어떤 목적으로 도입되었나요?

<details><summary> 정답
</summary>
제너레이터를 사용해서 비동기 처리를 동기처리처럼 동작하도록 구현했지만 코드가 무척이나 장황해지고 가독성도 나빠졌습니다. 이를 해결하기 위해 ES8에서는 제너러이터보다 간단하고 가독성 좋게 비동기 처리를 동기 처리처럼 동작할 수 있도록 구현할 수 있는 async/await가 도입되었습니다.
</details>

Q6. 어떤 종류의 함수에서 사용되나요?

<details><summary> 정답
</summary>
async함수에서 사용됩니다.
</details>

Q7. async 함수는 어떤 값을 반환하나요? 어떤 상황에서 값을 반환하지 않을 수 있나요?


<details><summary> 정답
</summary>
async 함수는 항상 Promise 객체를 반환합니다. 하지만 함수 내부에서 명시적으로 값을 반환하지 않으면 암묵적으로 undefined를 반환합니다.

```javascript
async function asyncFunction1() {
  // 아무 값도 반환하지 않음
}

async function asyncFunction2() {
  return 42; // 값을 반환
}

const promise1 = asyncFunction1();
const promise2 = asyncFunction2();

promise1.then((result) => {
  console.log("asyncFunction1의 결과:", result); // asyncFunction1의 결과: undefined
});

promise2.then((result) => {
  console.log("asyncFunction2의 결과:", result); // asyncFunction2의 결과: 42
});
```
</details>

Q8. async 함수 내에서 다른 비동기 함수를 호출할 때 어떤 예외 처리 방법을 사용해야 하나요?

<details><summary> 정답
</summary>
try-catch 블록을 사용하여 비동기 함수 호출 중 발생할 수 있는 예외를 처리합니다.
</details>
Q9. Promise와 async/await의 차이점은 무엇이며, 언제 어떤 것을 사용해야 하나요? (GPT)

<details><summary> 정답
</summary>
Promise는 콜백 지옥을 피하기 위해 비동기 코드를 조금 더 관리하기 쉽게 만들어 주지만, 
 async/await는 비동기 코드를 동기식처럼 작성할 수 있게 해줍니다. 일반적으로 async/await를 사용하는 것이 가독성과 유지 보수성 면에서 더 좋습니다.
</details>

### 47장 에러처리
---

Q10. 에러 처리의 중요성에 대해 얘기해보세요. 왜 에러를 처리해야 할까요?

<details><summary> 정답
</summary>
에러가 발생하지 않는 코드를 작성하는 것은 불가능 합니다. 따라서 에러는 언제나 발생할 수 있으며 발생한 에러에 대해 대처하지 않고 방치하면 최악의 경우 프로그램이 강제종료 되므로 사용자 경험이 나빠질 수 있습니다.
이를 방지하고 개선하기 위해선 에러처리가 필요합니다.
</details>

Q11. 자바스크립트의 일반적인 에러처리 방식중 한가지만 설명해 보세요

<details><summary> 정답
</summary>
try-catch-finally 블록이며
try는 실행할 코드 catch는 try에서 에러가 발생하면 실행되는 코드블럭 finally는 에러 발생과 상관없이 반드시 실행되는 코드 블럭 입니다.</details>


Q12. JavaScript에서 에러를 어떻게 발생시키고 처리할 수 있나요?
<details><summary> 정답
</summary>
try 코드블록에서 throw문으로 에러 객체를 던져 에러를 발생시킬 수 있으며, try-catch 블록을 사용하여 에러를 처리합니다.</details>

### 48장 모듈
---

Q13. 모듈이란 무엇인가요?
<details><summary> 정답
</summary>
모듈이란 애플리케이션을 구성하는 개별적 요소로서 재사용 가능한 코드 조각을 말합니다.
</details>

Q14. CommonJS, AMD, ES6 등의 모듈 시스템에 대해 설명해보세요.

<details><summary> 정답
</summary> 

CommonJS는 Node.js 환경에서 주로 사용됩니다.<br/>
AMD(Asynchronous Module Definition)는 비동기 모듈 로딩을 지원하며, RequireJS와 함께 사용됩니다.<br/>
ES6 모듈은 독자적인 모듈 스코프를 갖으며, import와 export 문을 사용하여 모듈을 정의하고 가져옵니다.<br/>
</details>

### 49장 Babel과 Webpack을 이용한 ES6 환경 구축
---

Q15. Babel과 Webpack은 각각 어떤 역할을 하는 도구인가요? 
<details><summary> 정답
</summary>

**Babel**: Babel은 최신 JavaScript 코드(ES6+)를 이전 버전의 JavaScript 코드(예: ES5)로 변환하는 도구입니다. 이는 브라우저 호환성을 확보하고 새로운 기능을 사용할 수 있도록 도와줍니다. <br/>
**Webpack**: Webpack은 모듈 번들러로, 여러 모듈과 종속성을 하나로 묶어 최적화된 번들을 생성합니다. 이는 코드 관리와 성능 최적화를 위해 필요합니다.
</details>
Q16. Babel의 "트랜스파일링(Transpiling)"이란 무엇인가요?

<details><summary> 정답
</summary>
트랜스파일링은 하나의 프로그래밍 언어로 작성된 코드를 다른 언어로 변환하는 과정을 의미합니다. Babel을 사용하여 ES6 코드를 ES5로 변환하며, 예를 들어 화살표 함수, 클래스, 모듈 등의 ES6 기능이 ES5로 변환됩니다.

</details>
Q17. Webpack은 어떻게 모듈 번들링을 수행하며, 왜 모듈 번들러가 필요한가요?
<details><summary> 정답
</summary>
웹팩을 사용하면 의존 모듈이 하나의 파일로 번들링 되므로 별도의 모듈 로더가 필요 없어지게 됩니다.
여러개의 자바스크립트 파일을 하나로 번들링될 경우 HTML파일에서 script태그로 여러 개의 자바스크립트 파일을 로드해야하는 번거로움이 사라지게 되기 때문입니다.




