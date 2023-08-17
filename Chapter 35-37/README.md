## 35장 스프레드 문법
#### **Q_1. spread 문법을 사용할 때의 이점은 무엇이며 rest 문법과 다른 점은 무엇인가요?**

<details><summary>정답
</summary>
  ES6의 spread 문법은 함수형 패러다임에서 코딩할 때 매우 유용합니다.

  왜냐하면 Object.create, slice나 라이브러리 함수를 사용하지 않고도 배열이나 객체의 복사본을 쉽게 만들 수 있기 때문입니다.

이 언어 기능은 Redux나 Rx.js를 사용하는 프로젝트에서 많이 사용됩니다.

Rest 구문과 Spread 구문은 배열이나 객체를 다룰 때 사용되는 ES6 문법의 특징입니다. 두 구문은 비슷해 보이지만, 사용하는 목적과 작동 방식이 다릅니다.

Rest: 여러 개의 개별 요소들을 -> 하나의 배열 또는 객체로 모음.<br>
Spread: 하나의 배열이나 객체를 -> 여러 개의 개별 요소들로 퍼뜨림.<br>

이 두 문법은 코드를 더 간결하고 직관적으로 만들어주며,<br> 다양한 프로그래밍 상황에서 유용하게 사용됩니다.

</details>

## 36장 디스트럭처링 할당
#### **Q_2. 구조 분해 할당(Destructuring assignment)이란?**

<details><summary> 정답
</summary>
구조화된 배열과 같은 이터러블 또는 객체를 destrurcturing 하여 1개 이상의 변수에 개별적으로 할당하는 것입니다.
</details>

#### **Q_3. 배열 디스트럭처링과 객체 디스트럭처링의 기본 차이점을 설명해주세요.**
<details><summary> 정답
</summary>

배열 디스트럭처링은 배열 내부의 요소를 순서대로 추출합니다(할당기준 인덱스), 반면 객체 디스트럭처링은 객체의 키를 기반으로 값을 추출합니다(할당기준 프로퍼티 키).
</details>

#### **Q_4. 아래 코드값을 예측해보세요**
```javascript
const { x, y, ...rest } = { x: 10, y: 20, z: 30, w: 40 };
console.log(x, y, rest);
```
<details><summary> 정답
</summary>

출력: 10 20 { z: 30, w: 40 }
</details>

#### **Q_5. 디스트럭처링 할당을 사용하여 함수의 파라미터를 받는 경우, 어떤 장점이 있나요?**
<details><summary> 정답
</summary>

좀 더 간단하고 가독성좋게 표현할 수 있습니다.
대표적으로 함수의 파라미터가 많아졌을 때, 디스트럭처링을 사용하면 파라미터의 순서에 구애받지 않고 원하는 값을 추출할 수 있습니다. 또한, 함수 내부에서 객체의 특정 속성만을 쉽게 참조할 수 있습니다.
</details>



## 37장 set과 map

#### **Q_6. set 이란?**

<details><summary>정답
</summary>
set객체는 중복되지 않는 유일한 값들의 집합이며 수학접 집합을 구현하기 위한 자료구조입니다.
</details>

#### **Q_7.다음 코드의 결과를 말씀해주세요**
```javascript
const set = new set();
set.add(1).add(2).add(2);
console.log(set);
````
<details><summary>정답
</summary>
set객체에 중복된 요소의 추가는 허용되지 않습니다. 이때 에러가 발생하기 않고 무시됩니다.
</details>

#### **Q_8. Set과 Map에 반복문을 사용하여 각 요소를 순회하는 방법에 대해 설명해주세요.**

<details><summary>정답
</summary>
Set과 Map 모두 forEach 메서드와 for...of 문을 사용하여 순회할 수 있습니다.
</details>

#### **Q_9. Map / Set객체를 순회하는 순서는?**

<details><summary>정답
</summary>
요소가 추가된 순서를 따릅니다. ECMAScript 사양에 규정되어 있진 않지만 다른 이터러블의 순회와 호환성을 유지하기 위함입니다.
</details>

#### **Q_10. Map과 일반적인 객체(Object)의 차이점을 설명해주세요.**
<details><summary>정답
</summary>
Map은 키-값 쌍을 저장하는데, 키로는 어떠한 자료형도 사용할 수 있습니다(함수, 객체 등 포함). 반면 일반적인 객체는 주로 문자열 키를 사용합니다. 또한,Map은 이터러블인 반면 객체는 그렇지 않고 요소 개수를 확인하는 방법이 다릅니다.</details>

#### **Q_11.Map에 저장된 키-값 쌍을 모두 제거하는 방법은 무엇인가요?**
<details><summary>정답
</summary>
Map 객체의 clear 메서드를 사용하여 모든 키-값 쌍을 제거할 수 있습니다.</details>
