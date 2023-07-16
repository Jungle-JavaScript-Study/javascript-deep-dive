### CH. 18 함수와 일급 객체

- 다음과 같은 조건을 만족하는 객체를 ******************일급 객체******************라 한다.
    1. 무명의 리터럴로 생성할 수 있다. ( 런타임에 생성이 가능하다. )
    2. 변수나 자료구조(객체, 배열 등)에 저장할 수 있다.
    3. 함수의 매개변수에 전달할 수 있다.
    4. 함수의 반환값으로 사용할 수 있다.
    
    ```jsx
    // 1. 함수는 무명의 리터럴로 생성할 수 있다.
    // 2. 함수는 변수에 저장할 수 있다.
    // 런타임(할당 단계)에 함수 리터럴이 평가되어 함수 객체가 생성되고 변수에 할당된다.
    const increase = function (num) {
      return ++num;
    };
    
    const decrease = function (num) {
      return --num;
    };
    
    // 2. 함수는 객체에 저장할 수 있다.
    const auxs = { increase, decrease };
    
    // 3. 함수의 매개변수에게 전달할 수 있다.
    // 4. 함수의 반환값으로 사용할 수 있다.
    function makeCounter(aux) {
      let num = 0;
    
      return function () {
        num = aux(num);
        return num;
      };
    }
    
    // 3. 함수는 매개변수에게 함수를 전달할 수 있다.
    const increaser = makeCounter(auxs.increase);
    console.log(increaser()); // 1
    console.log(increaser()); // 2
    
    // 3. 함수는 매개변수에게 함수를 전달할 수 있다.
    const decreaser = makeCounter(auxs.decrease);
    console.log(decreaser()); // -1
    console.log(decreaser()); // -2
    ```
    
- 일급 객체로서 함수가 가지는 가장 큰 특징은 일반 객체와 같이 함수의 매개변수에 전달할 수 있으며, 함수의 반환값으로 사용할 수도 있다는 것이다.
→ 함수형 프로그래밍을 가능케 하는 자바스크립트의 장점 중 하나이다.
- 함수와 일반 객체의 차이
1. 일반객체는 호출할 수 없지만 함수 객체는 호출할 수 있다.
2. 함수 객체는 일반 객체에는 없는 함수 고유의 프로퍼티를 소유한다.
- 함수 객체의 프로퍼티
    
    ![arguments, caller, length, name, prototype 프로퍼티는 모두 함수 객체의 데이터 프로퍼티다.](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/990e7faf-f4fc-4a77-9ae3-04a1dacac9ba/Untitled.png)
    
    arguments, caller, length, name, prototype 프로퍼티는 모두 함수 객체의 데이터 프로퍼티다.
    
    ```jsx
    function square(number) {
      return number * number;
    }
    
    console.log(Object.getOwnPropertyDescriptors(square));
    /*
    {
      length: {value: 1, writable: false, enumerable: false, configurable: true},
      name: {value: "square", writable: false, enumerable: false, configurable: true},
      arguments: {value: null, writable: false, enumerable: false, configurable: false},
      caller: {value: null, writable: false, enumerable: false, configurable: false},
      prototype: {value: {...}, writable: true, enumerable: false, configurable: false}
    }
    */
    
    // __proto__는 square 함수의 프로퍼티가 아니다.
    console.log(Object.getOwnPropertyDescriptor(square, '__proto__')); // undefined
    
    // __proto__는 Object.prototype 객체의 접근자 프로퍼티다.
    // square 함수는 Object.prototype 객체로부터 __proto__ 접근자 프로퍼티를 상속받는다.
    console.log(Object.getOwnPropertyDescriptor(Object.prototype, '__proto__'));
    // {get: ƒ, set: ƒ, enumerable: false, configurable: true}
    ```
    
    - arguments 프로퍼티
        - arguments 프로퍼티 값은 arguments 객체이다.
        arguments 객체는 함수 호출 시 전달된 인수(argument)들의 정보를 담고 있는 순회 가능한(iterable) 유사 배열 객체이며, 함수 내부에서 지역 변수처럼 사용된다.
        - 함수를 정의할 때 선언한 매개변수는 함수 몸체 내부에서 변수와 동일하게 취급한다.
        → 함수가 호출되면 함수 몸체 내에서 암묵적으로 매개변수가 선언되고 undefined로 초기화된 이후 인수가 할당된다.
        - arguments 객체는 인수를 프로퍼티 값으로 소유하며 프로퍼티 키는 인수의 순서를 나타낸다.
        arguments 객체의 callee 프로퍼티는 호출되어 arguments 객체를 생성한 함수, 즉, 자기 자신을 가리키고 arguments 객체의 length 프로퍼티는 인수의 개수를 가리킨다.
        - arguments 객체는 매개변수 개수를 확정할 수 없는 ********************************가변 인자 함수********************************를 구현할 때 유용하다. 
        → ES6 에서는 Rest 파라미터를 도입했다.
        ( Rest 파라미터의 도입으로 모던 자바스크립트에서는 arguments 객체의 중요성이 이전 같지 않다. )
            
            ```jsx
            function sum() {
              let res = 0;
            
              // arguments 객체는 length 프로퍼티가 있는 유사 배열 객체이므로 for 문으로 순회할 수 있다.
              for (let i = 0; i < arguments.length; i++) {
                res += arguments[i];
              }
            
              return res;
            }
            
            console.log(sum());        // 0
            console.log(sum(1, 2));    // 3
            console.log(sum(1, 2, 3)); // 6
            ```
            
            ```jsx
            // ES6 Rest parameter
            function sum(...args) {
              return args.reduce((pre, cur) => pre + cur, 0);
            }
            
            console.log(sum(1, 2));          // 3
            console.log(sum(1, 2, 3, 4, 5)); // 15
            ```
            
    - caller 프로퍼티
        - caller 프로퍼티는 ECMAScript 사양에 포함되지 않는 비표준 프로퍼티다.
        → 표준화 될 예정도 없어서, 사용하지 말고 참고만.
        **함수 객체의 caller 프로퍼티는 함수 자신을 호출한 함수를 가리킨다.**
    - length 프로퍼티
        - 함수 객체의 length 프로퍼티는 함수를 정의할 때 선언한 매개변수의 개수를 가리킨다.
            
            ```jsx
            function foo() {}
            console.log(foo.length); // 0
            
            function bar(x) {
              return x;
            }
            console.log(bar.length); // 1
            
            function baz(x, y) {
              return x * y;
            }
            console.log(baz.length); // 2
            ```
            
        - arguments **객체의 length 프로퍼티는 인자(argument)의 개수를 가리키고**, 함수 객체의 **length 프로퍼티는 매개변수(parameter)의 개수를 가리킨다.**
    - name 프로퍼티
        - 함수 객체의 name 프로퍼티는 함수 이름을 나타낸다.
        - name 프로퍼티는 ES5 와 ES6에서 동작을 달리한다.
        → 익명함수 표현식에서 (ES5에서는) name 프로퍼티는 빈 문자열을 값으로 가짐.
        (ES6에서는) 함수 객체를 가리키는 식별자를 값으로 가짐.
            
            ```jsx
            // 기명 함수 표현식
            var namedFunc = function foo() {};
            console.log(namedFunc.name); // foo
            
            // 익명 함수 표현식
            var anonymousFunc = function() {};
            // ES5: name 프로퍼티는 빈 문자열을 값으로 갖는다.
            // ES6: name 프로퍼티는 함수 객체를 가리키는 변수 이름을 값으로 갖는다.
            console.log(anonymousFunc.name); // anonymousFunc
            
            // 함수 선언문(Function declaration)
            function bar() {}
            console.log(bar.name); // bar
            ```
            
    - _ _ proto _ _ 접근자 프로퍼티
        - 모든 객체는 [[Prototype]] 이라는 내부 슬롯을 가진다. 
        [[Prototype]] 내부 슬롯은 객체지향 프로그래밍의 상속을 구현하는 프로토타입 객체를 가리킨다.
        - _ _ proto _ _ 프로퍼티는 [[Prototype]] 내부 슬롯이 가리키는 프로토타입 객체에 접근하기 위해 사용하는 접근자 프로퍼티이다.
        → [[Prototype]] 내부 슬롯에도 직접 접근할 수 없으며, _ _proto_ _ 접근자 프로퍼티를 통해 간접적으로 프로토타입 객체에 접근할 수 있다.
            
            ```jsx
            const obj = { a: 1 };
            
            // 객체 리터럴 방식으로 생성한 객체의 프로토타입 객체는 Object.prototype이다.
            console.log(obj.__proto__ === Object.prototype); // true
            
            // 객체 리터럴 방식으로 생성한 객체는 프로토타입 객체인 Object.prototype의 프로퍼티를 상속받는다.
            // hasOwnProperty 메서드는 Object.prototype의 메서드다.
            console.log(obj.hasOwnProperty('a'));         // true
            console.log(obj.hasOwnProperty('__proto__')); // false
            ```
            
            - hasOwnProperty 메서드
    - prototype 프로퍼티
        - prototype 프로퍼티는 생성자 함수로 호출할 수 있는 함수 객체(constructor)만이 소유하는 프로퍼티이다.
        non-constructor에는 prototype 프로퍼티가 없다.
            
            ```jsx
            // 함수 객체는 prototype 프로퍼티를 소유한다.
            (function () {}).hasOwnProperty('prototype'); // -> true
            
            // 일반 객체는 prototype 프로퍼티를 소유하지 않는다.
            ({}).hasOwnProperty('prototype'); // -> false
            ```