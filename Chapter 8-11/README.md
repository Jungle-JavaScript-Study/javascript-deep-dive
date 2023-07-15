Q1. if … else 문과 삼항 조건 연산자의 차이점에 대해서 설명하시오.

<details>
<summary>정답</summary>
    - 둘 다 조건문을 만들어내지만, 
    if … else 문은 **표현식이 아닌 문**이고,
    삼항 조건 연산자는 **표현식**이다.
    따라서, 삼항 조건 연산자 표현식은 값처럼 사용할 수 있기 때문에 **변수에 할당할 수 있다**.
    
    ```jsx
    var num = 2;
    var kind = num ? (num > 0 ? '양수' : '음수' ) : '영';
    
    console.log(kind); // 양수
    ```
</details>

Q2. 아래 예제에 대한 결과를 답하고, 이유를 설명하시오.

```jsx
var month = 11;
var monthName;

switch (month) {
case 1: monthName = 'January';
case 2: monthName = 'February';
case 3: monthName = 'March';
case 4: monthName = 'April';
case 5: monthName = 'May';
case 6: monthName = 'June';
case 7: monthName = 'July';
case 8: monthName = 'August';
case 9: monthName = 'September';
case 10: monthName = 'October';
case 11: monthName = 'November';
case 12: monthName = 'December';
default: monthName = 'Invalid month';
}

console.log(monthName); // ??
```
<details>
<summary>정답</summary>
  
    - 폴스루(fall through) 현상으로 인해, **‘Invalid month’** 가 출력된다.
    break 문이 없기때문에 case 문으로 실행 흐름이 이동하여 monthName 에 ‘November’가 할당된 후 switch문을 탈출하지 않고
    ‘December’가 할당되고 ‘Invalid month’가 재할당 된다.
</details>

Q3. 레이블 문이 무엇인지 설명하시오.
<details>
<summary>정답</summary>
  
    - 레이블 문은 **식별자가 붙은 문**이다.
</details>
<details>
<summary>꼬리 질문</summary> 
    
Q3-1. 레이블 문은 어떤 경우에 쓰나요 ?
<details>
<summary>정답</summary>
	
        - 중첩된 for문 외부로 탈출할 때 유용하지만, 
        레이블 문을 사용하면 코드가 복잡해지고 가독성이 나빠져서, 일반적으로는 권장하지 않는다.
</details>
</details>

Q4. 자바스크립트 엔진이 불리언이 아닌 값을 불리언 타입으로 암묵적으로 변환시킬 때, false 로 변환되는 값을 3가지 이상 말해보세요.
<details>
<summary>정답</summary>
	
    - `false`, `undefined`, `null`, `0`, `-0`, `NaN`, `‘’(빈 문자열)`
</details>

Q5. 아래의 예제의 결과를 말하고, 이유를 설명하시오.

```jsx
'Cat' && 'Dog' // -> ??? // 1
'Cat' || 'Dog' // -> ??? // 2
```
<details>
<summary>정답</summary>
	
    1. ‘Dog’ ,  논리곱 연산자(&&)는 논리 연산의 결과를 결정하는 두 번째 피연산자를 반환한다.
    2. ‘Cat’ ,  논리합 연산자(||)는 논리 연산의 결과를 결정한 첫 번째 피연산자를 반환한다.
</details>

Q6. 객체란 무엇인가요 ?
<details>
<summary>정답</summary>
	
    - 0개 이상의 프로퍼티로 구성된 집합으로, 다양한 타입의 값(원시 값 또는 다른 객체)를 하나의 단위로 구성한 복합적인 자료구조이다.
</details>
<details>
<summary>꼬리 질문</summary> 
    &nbsp;&nbsp;Q6-1. 자바스크립트에서 객체를 생성하는 방법을 3가지 이상 말해주세요.
<details>
<summary>정답</summary>
        - 객체 리터럴
        - Object 생성자 함수
        - 생성자 함수
        - Object.create 메서드
        - 클래서(ES6)
</details>

Q6-2. 프로퍼티와 메서드에 대해서 설명해주세요.
<details>
<summary>정답</summary>
	
        - 프로퍼티(property) : 객체의 상태를 나타내는 값(data)
            - 프로퍼티는 키와 값으로 구성된다.
        - 메서드: 프로퍼티(상태 데이터)를 참조하고 조작할 수 있는 동작
            - 객체에 묶여있는 함수를 메서드라고 한다.
</details>
</details>


Q7. 아래와 같은 예제의 결과에 대한 설명을 하시오.

```jsx
var person = {
	name = 'Ahn'
};

person.age = 27;
console.log(person); // -> ??? // 1
delete person.age;
delete person.address;

console.log(person); // -> ??? // 2
```
<details>
<summary>정답</summary>
    1. `{ name: “Ahn”, age: “27” }`
        - 존재하지 않는 프로퍼티에 값을 할당하면, age 프로퍼티가 동적으로 생성된다.
    2. `{ name: “Ahn” }` 
        - delete 연산자는 객체의 프로퍼티를 삭제한다.
        존재하지 않는 프로퍼티를 삭제하면 **아무런 에러 없이 무시된다.**
</details>

Q8. 자바스크립트에서 변수에 원시 값과 객체를 할당할 때 각각 메모리에 저장되는 값은 무엇인가요?
<details>
<summary>정답</summary>
	
    - 원시값을 할당한 변수는 원시 값 자체가 저장된다.
    - 객체를 할당하면 객체가 저장된 메모리(힙영역)를 참조하는 주소값이 저장된다.
</details>
<details>
<summary>꼬리 질문</summary>     
    Q8-1. 원시 값과 객체의 참조에 대해서 설명해주세요.
<details>
<summary>정답</summary>
	
        - 원시 값은 값 자체가 복사되어 독립적인 새로운 변수가 만들어진다.
        - 객체는 참조하는 주소값이 복사되므로, 같은 객체를 참조하는 새로운 변수가 만들어진다. - 이 두 변수는 하나의 같은 객체를 **공유**하게 된다.
</details>
    
Q8-2. 여러 개의 식별자가 하나의 객체를 공유 할 때 생길 수 있는 문제점은 무엇이 있나요 ?
<details>
<summary>정답</summary>
 
        - 한 식별자가 객체의 속성을 변경하면, 그 변경사항을 공유하므로, 
        의도치 않게 다른 식별자를 통해 객체가 변경되는 부작용이 발생할 수 있다.
</details>
<details>
<summary>꼬리 질문</summary> 
        - Q8-2-1. 이런 문제를 피하려면 어떻게 해야하나요 ?
<details>
<summary>정답</summary>
                - 객체를 복사할 때 깊은 복사(deep copy)를 하면 된다.
                - ex> 라이브러리 lodash 에서 제공하는 ‘_.cloneDeep’ 함수를 이용하는 방법이 있다.
                
                ```jsx
                const _ = require('lodash');
                
                let obj1 = { name: "John", age: 30, func: () => console.log('Hello') };
                let obj2 = _.cloneDeep(obj1);
                console.log(obj1 === obj2); // false
                console.log(obj1.age === obj2.age); // false
                ```
</details>
</details>
</details>

