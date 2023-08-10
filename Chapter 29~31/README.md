## Ch 29~31 질문리스트

#### Q-1. Math.max()는 왜 Math.min()보다 작은가요?

```javascript
Math.max(); // -infinity
Math.min(); // infinity
Math.max() < Math.min(); // true
```

<details><summary>정답
</summary>

max, min메소드가 단순히 최댓,최솟값을 나타내는게 아니라 인자로 받은 것 중에 최댓값, 최솟값을 반환합니다.

max의 인자값에 아무것도 없다면 아무 것도 없는 것 중에 가장 큰 것은 javascript가 인지하는 수 중 최솟값인 -infinity가 될 것이고, min의 경우에는 최솟값이 javascript가 인지하는 수 중 최댓값인 infinity가 될 것입니다.

</details>

#### Q-2. 왜 0.1 + 0.2 === 0.3은 false인가요?

```javascript
0.1 + 0.2; // 0.30000000000000004
```

<details><summary>정답
</summary>

JavaScript는 소수를 처리할 때 부동소수점을 이용하여 근사치를 표현합니다

따라서 소수점 계산도 근사치를 표현할 뿐 0.3 이라는 정확한 계산을 하지 못합니다.

</details>
<details><summary>꼬리질문
</summary>

#### 위 문제의 해결방법에 대해 설명해 보세요

<details><summary>정답
</summary>

Number.prototype.toFixed([digits])을 이용해 digits(소수점 몇번째자리 까지 표시할 것인지 정할 수)을 정해 근사값으로 처리(고정소수점표기, 이하 반올림)

</details>

</details>

#### Q-3. 정규식 표현식은 무엇인가요?

<details><summary>정답
</summary>

정규 표현식은 일정하나 패턴을 가진 문자열의 집합을 표현하기 위해 사용하는 형식 언어(formal language)입니다.

</details>

#### Q-4. 정규식 표현식을 알아야 하는 이유는 무엇일까요?

<details><summary>정답
</summary>

복잡한 문자열 패턴을 일치시키고 추출하는데 사용되어, 데이터 유효성 검사, 텍스트 분석, 문자열 대체 등 다양한 상황에서 효율적인 텍스트 처리를 가능하게 하기 때문입니다.

</details>

<details><summary>꼬리질문
</summary>

#### 정규 표현식은 JS에만 있는것일까요?

<details><summary>정답
</summary>

JAVA, Python 등 다른 프로그래밍언어에서도 사용하고 언어 별로 문법도 다릅니다.
그렇기 때문에 자신이 사용하는 프로그래밍 언어에서 정해져있는 정규식표현을 공부할 필요가 있습니다.

</details>

</details>

#### Q-5. 정규 표현식의 생성 방법을 설명해주세요

<details><summary>정답
</summary>
정규 표현식 객체는 정규 표현식 리터럴과 RegExp 생성자 함수를 사용해 생성할 수 있습니다.

```javascript
const pattern = /abc/gi; //리터럴 표현식
```

```javascript
const patternStr = 'abc';
const flags = 'gi';
const dynamicPattern = new RegExp(patternStr, flags); // 생성자 함수
```

</details>

#### Q-6. JS 정규 표현식은 문자열을 대상으로 패턴 매칭 기능을 제공하는데 어떤 자료구조를 이용하여 기능을 제공할까요?

<details><summary> 정답
</summary>
JavaScript의 정규 표현식은 내부적으로 NFA (Nondeterministic Finite Automaton)와 유사한 자료구조를 사용하여 문자열 패턴 매칭 기능을 제공합니다.

NFA는 문자열의 각 위치에서 가능한 다음 상태들의 집합을 나타내며, 입력 문자열을 한 문자씩 읽으면서 이러한 상태 전이를 따라가면서 패턴 매칭을 수행합니다. JavaScript의 정규 표현식 엔진은 이와 유사한 방식으로 동작하며, 입력 문자열을 순차적으로 탐색하면서 패턴에 매치되는지를 결정합니다.

</details>
