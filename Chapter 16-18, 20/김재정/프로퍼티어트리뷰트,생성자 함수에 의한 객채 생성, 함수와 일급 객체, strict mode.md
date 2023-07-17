**16.1 내부 슬롯과 내부 메서드**

내부 슬롯(internal slot)과 내부 메서드(internal method)은 객체의 내부적인 동작을 정의하는데 사용되는 내부적인 구성 요소입니다.

- 메서드
    
    **내부 슬롯 (Internal Slots):**
    
    1. [[Prototype]]: 객체의 프로토타입에 대한 참조를 저장합니다.
    2. [[Extensible]]: 객체가 확장 가능한지 여부를 나타내는 불리언 값을 저장합니다.
    3. [[GetPrototypeOf]]: 객체의 프로토타입을 가져오는 동작을 수행합니다.
    4. [[SetPrototypeOf]]: 객체의 프로토타입을 설정하는 동작을 수행합니다.
    5. [[Get]]: 객체의 속성 값을 가져오는 동작을 수행합니다.
    6. [[Set]]: 객체의 속성 값을 설정하는 동작을 수행합니다.
    7. [[HasProperty]]: 객체가 특정 속성을 가지고 있는지 여부를 확인하는 동작을 수행합니다.
    8. [[Delete]]: 객체의 속성을 삭제하는 동작을 수행합니다.
    
    **내부 메서드 (Internal Methods):**
    
    1. [[Call]]: 객체가 함수처럼 호출될 때 실행되는 동작을 수행합니다.
    2. [[Construct]]: 객체가 생성자 함수로서 호출될 때 실행되는 동작을 수행합니다.
    3. [[GetPrototypeOf]]: 객체의 프로토타입을 가져오는 동작을 수행합니다.
    4. [[SetPrototypeOf]]: 객체의 프로토타입을 설정하는 동작을 수행합니다.
    5. [[Get]]: 객체의 속성 값을 가져오는 동작을 수행합니다.
    6. [[Set]]: 객체의 속성 값을 설정하는 동작을 수행합니다.
    7. [[HasProperty]]: 객체가 특정 속성을 가지고 있는지 여부를 확인하는 동작을 수행합니다.
    8. [[Delete]]: 객체의 속성을 삭제하는 동작을 수행합니다.
    9. [[OwnPropertyKeys]]: 객체의 고유한 속성 키들을 가져오는 동작을 수행합니다.

**16.2 프로퍼티 어트리뷰트와 프로퍼티 디스크립터 객체**

자바스크립트 엔진은 프로퍼티를 생성할 때 프로퍼티의 상태를 나타내는 **프로퍼티 어트리뷰트**를 기본값으로 자동정의 한다.

프로터피 어트리뷰트는 JS엔진이 관리하는 내부 상태 값인 내부슬롯(value, write, Enumerable,Configurable)이다.

따라서 프로퍼티 어트리뷰트에 직접 접근할 수 없지만 Object.getOwnpropertyDescriptor 메서드를 사용하여 프로퍼티 디스크립터 객체를 간접적으로 확인할 수 있다.

**16.3 데이터 프로퍼티와 접근자 프로퍼티**

데이터 프로퍼티 : 키와 값으로 구성된 일반적인 프로퍼티다. 지금까지 살펴본 모든 프로퍼티는 데이터 프로퍼티다.

1. **value**: 속성의 값입니다.
2. **writable**: 속성의 값이 변경 가능한지 여부를 나타내는 불리언 값입니다.
3. **enumerable**: 속성이 열거 가능한지 여부를 나타내는 불리언 값입니다.
4. **configurable**: 속성이 재정의 가능한지 여부를 나타내는 불리언 값입니다.

접근자 프로퍼티 : 자체적으로는 값을 갖지 않고 다른 데이터 프로퍼티의 값을 읽거나 저장할 때 호출되는 접근자 함수로 구성된 프로퍼티다.

1. **enumerable**: 속성이 열거 가능한지 여부를 나타내는 불리언 값입니다.
2. **configurable**: 속성이 재정의 가능한지 여부를 나타내는 불리언 값입니다.
3. **get**: 속성의 getter 함수입니다.
4. **set**: 속성의 setter 함수입니다.

```jsx
const obj = {};

Object.defineProperty(obj, 'myProperty', {
  value: 42,
  writable: false,
  enumerable: true,
  configurable: true
});

console.log(obj.myProperty); // 42
obj.myProperty = 50; // Error: Cannot assign to read only property
```

접근자 프로퍼티는 자체적으로 값을 가지지 않으며 다만 데이터 프로퍼티의 값을 읽거나 저장할때 관여한다.

**16.4 프로퍼티 정의**

```jsx
const obj = {};

Object.defineProperties(obj, {
  propertyName1: {
    value: value1,
    writable: true
  },
  propertyName2: {
    value: value2,
    enumerable: true
  }
});
```

새로운 프로퍼티를 추가하면서 어트리뷰트를 명시적으로정의하거나 재정의 하는것을 말한다.

프로퍼티 정의를 통해 객체에 새로운 속성을 추가하거나 기존 속성을 수정하여 객체의 동작을 제어할 수 있습니다.

**16.5 객체변경방지**

객체의 변경을 방지하는 다양한 메서드를 제공한다.

1. 객체 확장 금지
    1. 확장이 금지된 객체는 프로퍼티 추가가 금지된다.
    2. object.ptreventExtrnsisons
    3. 삭제는 가능하다.
2. 객체 밀봉
    1. 밀봉된 객체는 읽기와 쓰기만 가능하다. 즉, 재정의 금지를 의미한다.
    2. object.isSealed여부로 확인할 수 있다.
3. 객체동결
    1. 읽기만 가능한 가장 수준높은 방지
    2. isFrozen네서드로 가능하다

불변 객체의 경우 얕은 변경 방지로 직속 프로퍼티만 변경이 방지되고 중첩객체까진 영향을 주지 못한다.

**17.1 object 생성자 함수**

생성자 함수란 new 연산자와 함께 호출하여 객체(인스턴스)를 생성하는 함수이다.

**17.2 생성자 함수**

```jsx
const person = {
  name: 'John',
  age: 30,
  greet: function() {
    console.log(`Hello, my name is ${this.name}.`);
  }
};

console.log(person.name); // John
person.greet(); // Hello, my name is John.

// 문제점 1: 메서드의 중복 생성
const person2 = {
  name: 'Jane',
  age: 25,
  greet: function() {
    console.log(`Hello, my name is ${this.name}.`);
  }
};

console.log(person2.name); // Jane
person2.greet(); // Hello, my name is Jane.

console.log(person.greet === person2.greet); // false
```

**기존 객체 리터럴에 의한 객체 생성 방식의 문제점** : 동일한 프로퍼티를 갖는 객체를 여러 생성해야 하는 경우 매번 같은 프로퍼티를 기술해야하기 때문에 비효울적이다.

**생성자 함수에 의한 객체 생성 방식의 장점 :** 객체를 생성하기 위한 템플릿처럼 생성자 함수를 사용하여 프로퍼티 구조가 동일한 객체 여러 개를 간편하기 생성할 수 있다.

new 연산자와 함께 호출하면 해당 함수는 생성자 함수로 동작한다.

**생성자 함수의 인스턴스 생성 과정**

- 생성자 함수 몸체에서 수행해야하는 일은 인스턴스를 생성하고 생성된 인스턴스를 초기화 해야한다.
- 인스턴스 생성과 this바인딩
    - 해당 처리는 함수 몸체의 코드가 한 줄씩 실행되는 런타임 이번에 실행된다.
- 인스턴스 초기화
- 인스턴스 반환

생성자 함수 내부에서 명시적으로 this가 아닌 다른 값을 반환하는 것은 생성자 함수의 기본 동작을 훼손한다. 따라서 생성자 함수 내부에서 return을 생략해야한다.

**내부 메서드 [[call]] [[construct]]**

일반 객체는 호출할 수 없지만 함수는 호출할 수 있다.

함수가 일반 함수로서 호출되면 함수 객체의 내부 메서드call이 호출되고 new일 경우 Construct가 호출된다.

Construct를 갖는 함수 객체를 constructor라고 하며 가지지 않는 함수를 non-constructor라고 한다.

모든 함수객체는 호출할 수 있지만 모든 함수 객체를 생성자 함수로서 호출할 수 있는것은 아니다.

함수 선언문과 함수 표현식으로 정의된 함수만이 constructor

ES6의 화살표 함수와 메서드 축약 표현으로 정의된 함수는 non-constructor다.

[new.target](http://new.target) → constructor인지 확인하는 메서드 (Es6이후에 지원되며 다른 방법으론 스코프 세이브 생성자 패턴이 있다.)

**18.1 일급객체**

일급객체의 조건

1. 무명의 리터럴로 선언 가능
2. 자료 구조에 할당 가능
3. 함수의 변환값으로 사용 가능
4. 함수의 매개변수로 사용 가능

일반 객체와 같이 함수의 매개변수에 전달할 수 있으며 함수의 반환값으로 사용할 수 있다.

**18.2 함수 객체의 프로퍼티**

argument 프로퍼티

이 객체는 함수 호출 시 전달된 인수들의 정보를 담고 있습니다. **`arguments`** 객체는 함수 내부에서 자동으로 생성되며, 함수 내에서 **`arguments`**를 통해 접근할 수 있습니다.

**`arguments`** 객체는 다음과 같은 주요한 속성과 메서드를 가지고 있습니다:

1. **`arguments.length`**: **`arguments`** 객체에 전달된 인수의 개수를 나타내는 속성입니다.
    
    ```jsx
    function sum() {
      console.log(arguments.length);
    }
    
    sum(1, 2, 3); // 3
    sum(4, 5); // 2
    ```
    
2. **`arguments[index]`**: **`arguments`** 객체에 전달된 인수에 접근하기 위한 인덱스를 사용하여 해당 인수에 접근할 수 있습니다. **`index`**는 0부터 시작합니다.
    
    ```jsx
    function concatenate() {
      console.log(arguments[0] + ' ' + arguments[1]);
    }
    
    concatenate('Hello', 'world'); // Hello world
    concatenate('OpenAI'); // OpenAI undefined
    
    ```
    
    인덱스를 사용하여 **`arguments`** 객체의 특정 인수에 접근할 수 있습니다. 그러나 **`arguments`** 객체는 실제 배열이 아니므로 배열 메서드와 속성을 직접적으로 사용할 수는 없습니다.
    
3. **`arguments`와 `...args`**: **`arguments`** 객체는 유사 배열 객체이므로 배열 메서드나 배열 기능을 사용하기 위해서는 변환해야 합니다. ES6부터는 Rest 파라미터를 사용하여 **`...args`**와 같은 형태로 인수들을 배열로 받을 수 있습니다.
    
    ```jsx
    function sum(...args) {
      console.log(args.reduce((total, num) => total + num, 0));
    }
    
    sum(1, 2, 3); // 6
    sum(4, 5, 6); // 15
    
    ```
    
    Rest 파라미터를 사용하여 인수들을 배열로 받아올 수 있으며, 배열 메서드를 적용할 수 있습니다.
    

**`arguments`** 객체는 함수 내에서 유용하게 활용될 수 있지만, 일반적으로는 Rest 파라미터나 기타 방법을 사용하여 인수를 처리하는 것이 더 권장됩니다. Rest 파라미터를 사용하면 코드의 가독성과 유지 보수성이 향상되고, 더욱 명확하고 직관적인 방식으로 인수를 다룰 수 있습니다.

caller 프로퍼티

함수 자신을 호출하는 함수

length 프로퍼티

객체는 인자의 개수를 가르키고 함수 는 매개변수릐 개수를 가르킨다.

name 프로퍼티

함수의 이름을 나타낸다.

**proto 접근자 프로퍼티**

접근자 프로퍼티를 통해 간접접으로 프로퍼티의 접근 가능하다

prototype 프로퍼티

일반 객체와 생성자 함수로 호출할 수 없는 non-constructor에는 prototype프로퍼티가 없다.

**20.1 strict mode란?**

암묵적 전역으로 인해 개발자의 의도와는 상관없이 오류를 발생시키는 원인이 될 가능성이 크다.

**20.2 strict mode의 적용**

**20.3 전역에 strict mode를 적용하는 것은 피하자**

전역에 strict mode를 적용하는 것은 모든 스크립트 및 모든 함수에 영향을 주므로, 코드의 예기치 않은 동작을 일으킬 수 있습니다. 특히, 다른 라이브러리나 코드와 상호작용하는 경우 전역 strict mode가 충돌이 발생할 수 있습니다. 전역 strict mode의 적용은 조심스럽게 고려되어야 하며, 대신 모듈 시스템을 사용하여 모듈 단위로 strict mode를 적용하는 것이 좋습니다.

**20.4 함수 단위로 strict mode 를 적용하는것도 피하자**

함수 단위로 strict mode를 적용하는 것은 코드의 가독성과 유지 보수성을 저하시킬 수 있습니다. 일부 함수에만 strict mode를 적용하는 경우, 그 함수와 연관된 코드를 이해하고 유지 보수하는 데 어려움이 있을 수 있습니다. 또한, strict mode가 적용되지 않은 함수에서 사용하는 변수나 함수와의 호환성 문제가 발생할 수 있습니다. 대신 모듈 시스템을 사용하여 모듈 단위로 strict mode를 적용하고, 모든 함수가 일관된 strict mode 환경에서 실행되도록 하는 것이 좋습니다.

**20.5 strict mode가 발생시키는 에러**

1. 암묵적 전역
2. 변수 함수 매개변수 삭제
3. 매개변수 중복
4. whith사용

**20.6 strict mode 적용에 의한 변화**

1. 일반함수의 this에 undefinde가 바인딩 된다. 생성자 함수가 아닌 일반 함수 내부에서는 this를 사용할 필요가 없기 때문이다.
2. argument객체 - 전달된 인수를 재할당 하여 변경해도 argument객체에 반영되지 않는다 (객체는 제외)
