### CH. 26 ES6 함수의 추가 기능

- 함수의 구분
    - ES6 이전의 함수는 사용 목적에 따라 명확히 구분되지 않는다.
    즉, **ES6 이전의 모든 함수는 일반함수로서 호출할 수 있는 것은 물론 생성자 함수로서 호출할 수 있다.**
    ( ES6 이전의 모든 함수는 callable 이면서 constructor 이다. )
    - ES6 이전의 모든 함수는 사용 목적에 따라 명확한 구분이 없으므로 호출 방식에 특별한 제약이 없고 생성자 함수로 호출되지 않아도 프로토타입 객체를 생성한다.
    ( 이는 혼란스러우며 실수를 유발할 가능성이 있고 성능에도 좋지 않다. )
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7a513235-c404-4afe-a84d-d214d7d91479/Untitled.png)
        
- 메서드
    - ES6 이전에는 메서드에 대한 명확한 정의가 없었지만, **ES6 사양에서 메서드는 메서드 축약 표현으로 정의된 함수만을 의미한다.**
    - **ES6 사양에서 정의한 메서드는 인스턴스를 생성할 수 없는 non-constructor**다.
    → ES6 메서드는 생성자함수로서 호출할 수 있다.
    → ES6 메서드는 인스턴스를 생성할 수 없으므로 prototype 프로퍼티가 없고 프로토타입도 생성하지 않는다.
    - **ES6 메서드는 자신을 바인딩한 객체를 가리키는 내부 슬롯 [[HomeObject]]를 갖는다.**
        
        ```jsx
        const base = {
          name: 'Lee',
          sayHi() {
            return `Hi! ${this.name}`;
          }
        };
        
        const derived = {
          __proto__: base,
          // sayHi는 ES6 메서드다. ES6 메서드는 [[HomeObject]]를 갖는다.
          // sayHi의 [[HomeObject]]는 sayHi가 바인딩된 객체인 derived를 가리키고
          // super는 sayHi의 [[HomeObject]]의 프로토타입인 base를 가리킨다.
          sayHi() {
            return `${super.sayHi()}. how are you doing?`;
          }
        };
        
        console.log(derived.sayHi()); // Hi! Lee. how are you doing?
        
        const derived = {
          __proto__: base,
          // sayHi는 ES6 메서드가 아니다.
          // 따라서 sayHi는 [[HomeObject]]를 갖지 않으므로 super 키워드를 사용할 수 없다.
          sayHi: function () {
            // SyntaxError: 'super' keyword unexpected here
            return `${super.sayHi()}. how are you doing?`;
          }
        };
        ```
        
        - 이처럼 ES6 메서드는 본연의 기능(super)을 추가하고 의미적으로 맞지 않는 기능(constructor)은 제거했다.
        → 따라서 **메서드를 정의할 때 프로퍼티 값으로 익명 함수 표현식을 할당하는 ES6 이전의 방식은 사용하지 않는 것이 좋다.**
- 화살표 함수
    - 화살표 함수(arrow function)은 function 키워드 대신 화살표 ( ⇒ , fat arrow )를 사용하여 기존의 함수 정의 방식보다 간략하게 함수를 정의할 수 있다.
    ( 표현만 간략한 것이 아니라 내부 동작도 기존의 함수보다 간략하다 )
    → **화살표 함수는 콜백 함수 내부에서 this 가 전역 객체를 가리키는 문제를 해결하기 위한 대안으로 유용하다.**
    - 화살표 함수 정의
        
        ```jsx
        // 함수 정의
        // 화살표 함수는 함수 선언문으로 정의할 수 없고 함수 표현식으로 정의해야 한다.
        const multiply = (x, y) => x * y;
        multiply(2, 3); // -> 6
        
        // 매개변수 선언
        // 매개변수가 여러 개인 경우 소괄호 () 안에 매개변수를 선언한다.
        const arrow = (x, y) => { ... };
        // 매개변수가 한 개인 경우 소괄호 ()를 생략할 수 있다.
        const arrow = x => { ... };
        // 매개변수가 없는 경우 소괄호 ()를 생략할 수 없다.
        const arrow = () => { ... };
        
        // 함수 몸체 정의
        // 함수 몸체가 하나의 문으로 구성된다면 함수 몸체를 감싸는 중괄호 {} 를 생략할 수 있다.
        // 함수 몸체가 여러 개의 문으로 구성된다면 함수 몸체를 감싸는 중괄호 {} 를 생략할 수 없다.
        const sum = (a, b) => {
          const result = a + b;
          return result;
        };
        ```
        
        - 화살표 함수도 즉시 실행 함수로 사용할 수 있다.
        - 화살표 함수도 일급 객체이므로 고차 함수에 인수로 전달할 수 있다.
        ( 이 경우 일반 함수보다 표현이 간결하고 가독성이 좋다. )
    - 화살표 함수와 일반 함수의 차이
        1. 화살표 함수는 인스턴스를 생성할 수 없는 non-constructor 이다.
        2. 중복된 매개변수 이름을 선언할 수 없다.
        3. 화살표 함수는 함수 자체의 this, arguments, super, new.target 바인딩을 갖지 않는다.
        → 화살표 함수 내부에서 this, arguments, super, new.target을 참조하면 스코프 체인을 통해 상위 스코프의 this, arguments, super, new.target을 참조한다.
    - this
        - **화살표 함수는 함수 자체의 this 바인딩을 갖지 않는다. 따라서 화살표 함수 내부에서 this를 참조하면 상위 스코프의 this를 그대로 참조한다. 이를 lexical this 라 한다.**
        - 메서드를 정의할 때에는 ES6 메서드 축약 표현으로 정의한 ES6 메서드를 사용하는 것이 좋다.
    - super
        - 화살표 함수는 함수 자체의 super 바인딩을 갖지 않는다. 따라서 화살표 함수 내부에서 super를 참조하면 this와 마찬가지로 상위 스코프의 super를 참조한다.
    - arguments
        - 화살표 함수는 함수 자체의 arguments 바인딩을 갖지 않는다. 따라서 화살표 함수 내부에서 arguments를 참조하면 this 와 마찬가지로 상위 스코프의 arguments를 참조한다.
        → 따라서 화살표 함수로 가변 인자 함수를 구현해야 할 때는 반드시 Rest 파라미터를 사용해야 한다.
- Rest 파라미터
    - 기본 문법
        - Rest 파라미터(나머지 매개변수)는 매개변수 이름 앞에 세개의 점 … 을 붙여서 정의한 매개변수를 의미한다.
        - **Rest 파라미터는 함수에 전달된 인수들의 목록을 배열로 전달받는다.**
            
            ```jsx
            function foo(...rest) {
              // 매개변수 rest는 인수들의 목록을 배열로 전달받는 Rest 파라미터다.
              console.log(rest); // [ 1, 2, 3, 4, 5 ]
            }
            
            foo(1, 2, 3, 4, 5);
            
            // 일반 매개변수와 Rest 파라미터는 함께 사용할 수 있다.
            // 이때 함수에 전달된 인수들은 매개변수와 Rest 파라미터에 순차적으로 할당된다.
            function foo(param, ...rest) {
              console.log(param); // 1
              console.log(rest);  // [ 2, 3, 4, 5 ]
            }
            
            foo(1, 2, 3, 4, 5);
            
            function bar(param1, param2, ...rest) {
              console.log(param1); // 1
              console.log(param2); // 2
              console.log(rest);   // [ 3, 4, 5 ]
            }
            
            bar(1, 2, 3, 4, 5);
            ```
            
        - Rest 파라미터는 이름 그대로 먼저 선언된 매개변수에 할당된 인수를 제외한 나머지 인수들로 구성된 배열이 할당된다.
        → **Rest 파라미터는 반드시 마지막 파라미터여야 한다.**
            
            ```jsx
            function foo(...rest, param1, param2) { }
            
            foo(1, 2, 3, 4, 5);
            // SyntaxError: Rest parameter must be last formal parameter
            
            // Rest 파라미터는 단 하나만 선언할 수 있다.
            function foo(...rest) {}
            console.log(foo.length); // 0
            
            function bar(x, ...rest) {}
            console.log(bar.length); // 1
            
            function baz(x, y, ...rest) {}
            console.log(baz.length); // 2
            
            // Rest 파라미터는 함수 정의 시 선언한 매개변수 개수를 나타내는 함수 객체의 length 프로퍼티에 영향을 주지 않는다.
            function foo(...rest) {}
            console.log(foo.length); // 0
            
            function bar(x, ...rest) {}
            console.log(bar.length); // 1
            
            function baz(x, y, ...rest) {}
            console.log(baz.length); // 2
            ```
            
        
    - Rest 파라미터와 arguments 객체
        - ES6 에서는 rest 파라미터를 사용하여 가변 인자 함수의 인수 목록을 배열로 직접 전달받을 수 있다.
        → 유사 배열 객체인 arguments 객체를 배열로 변환하는 번거로움을 피할 수 있다.
            
            ```jsx
            function sum() {
              // 유사 배열 객체인 arguments 객체를 배열로 변환한다.
              var array = Array.prototype.slice.call(arguments);
            
              return array.reduce(function (pre, cur) {
                return pre + cur;
              }, 0);
            }
            
            console.log(sum(1, 2, 3, 4, 5)); // 15
            
            function sum(...args) {
              // Rest 파라미터 args에는 배열 [1, 2, 3, 4, 5]가 할당된다.
              return args.reduce((pre, cur) => pre + cur, 0);
            }
            console.log(sum(1, 2, 3, 4, 5)); // 15
            ```
            
- 매개변수 기본값
    - 함수를 호출할 때 매개변수의 개수만큼 인수를 전달하는 것이 바람직하지만 그렇지 않은 경우에도 에러가 발생하지 않는다.
    ( 자바스크립트 엔진이 매개변수의 개수와 인수의 개수를 체크하지 않기 때문이다. )
    - 인수가 전달되지 않은 매개변수의 값은 undefined다.
    - 매개변수 기본값은 매개변수에 인수를 전달하지 않은 경우와 undefined를 전달한 경우에만 유효하다.
        
        ```jsx
        function logName(name = 'Lee') {
          console.log(name);
        }
        
        logName();          // Lee
        logName(undefined); // Lee
        logName(null);      // null
        
        // 매개변수 기본값은 함수 정의 시 선언한 매개변수 개수를 나타내는 함수 객체의 length 프로퍼티와 arguments 객체에 아무런 영향을 주지 않는다.
        function sum(x, y = 0) {
          console.log(arguments);
        }
        
        console.log(sum.length); // 1
        
        sum(1);    // Arguments { '0': 1 }
        sum(1, 2); // Arguments { '0': 1, '1': 2 }
        ```