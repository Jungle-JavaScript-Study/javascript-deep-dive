### CH. 17 생성자 함수에 의한 객체 생성

- Object 생성자 함수
    - new 연산자와 함께 Object 생성자 함수를 호출하면 빈 객체를 생성하여 반환한다.
    빈 객체를 생성한 이후 프로퍼티 또는 메서드를 추가하여 객체를 완성할 수 있다.
    - 생성자 함수(constructor)란 new 연산자와 함께 호출하여 객체(인스턴스)를 생성하는 함수를 말한다.
    생성자 함수에 의해 생성된 객체를 인스턴스(instance)라 한다.
    - 자바스크립트는 Object 생성자 함수 이외에도 String, Number, Boolean, Function, Array, Date, RegExp, Promise 등의 빌트인 생성자 함수를 제공한다.
    - 객체를 생성하는 방법은 객체 리터럴을 사용하는 것이 더 간편하다. **Object 생성자 함수를 사용해 객체를 생성하는 방식은 특별한 이유가 없다면 그다지 유용해보이지 않는다.**
        
        ```jsx
        // 빈 객체의 생성
        const person = new Object();
        
        // 프로퍼티 추가
        person.name = 'Lee';
        person.sayHello = function () {
          console.log('Hi! My name is ' + this.name);
        };
        
        console.log(person); // {name: "Lee", sayHello: ƒ}
        person.sayHello(); // Hi! My name is Lee
        
        // String 생성자 함수에 의한 String 객체 생성
        const strObj = new String('Lee');
        console.log(typeof strObj); // object
        console.log(strObj);        // String {"Lee"}
        
        // Number 생성자 함수에 의한 Number 객체 생성
        const numObj = new Number(123);
        console.log(typeof numObj); // object
        console.log(numObj);        // Number {123}
        
        // Boolean 생성자 함수에 의한 Boolean 객체 생성
        const boolObj= new Boolean(true);
        console.log(typeof boolObj); // object
        console.log(boolObj);        // Boolean {true}
        
        // Function 생성자 함수에 의한 Function 객체(함수) 생성
        const func = new Function('x', 'return x * x');
        console.log(typeof func); // function
        console.dir(func);        // ƒ anonymous(x)
        
        // Array 생성자 함수에 의한 Array 객체(배열) 생성
        const arr = new Array(1, 2, 3);
        console.log(typeof arr); // object
        console.log(arr);        // [1, 2, 3]
        
        // RegExp 생성자 함수에 의한 RegExp 객체(정규 표현식) 생성
        const regExp = new RegExp(/ab+c/i);
        console.log(typeof regExp); // object
        console.log(regExp);        // /ab+c/i
        
        // Date 생성자 함수에 의한 Date 객체 생성
        const date = new Date();
        console.log(typeof date); // object
        console.log(date);        // Mon May 04 2020 08:36:33 GMT+0900 (대한민국 표준시)
        ```
        
- 생성자 함수
    - 객체 리터럴에 의한 객체 생성 방식의 문제점
        - 객체 리터럴에 의한 객체 생성 방식은 단 하나의 객체만 생성한다.
        → **동일한 프로퍼티를 갖는 객체를 여러 개 생성해야 하는 경우 매번 같은 프로퍼티를 기술해야 하기 때문에 비효율적이다.**
    - 생성자 함수에 의한 객체 생성 방식의 장점
        - 생성자 함수에 의한 객체 생성 방식은 마치 객체(인스턴스)를 생성하기 위한 템플릿(클래스)처럼 생성자 함수를 사용하여 **프로퍼티 구조가 동일한 객체 여러 개를 간편하게 생성할 수 있다.**
            
            ```jsx
            // 생성자 함수
            function Circle(radius) {
              // 생성자 함수 내부의 this는 생성자 함수가 생성할 인스턴스를 가리킨다.
              this.radius = radius;
              this.getDiameter = function () {
                return 2 * this.radius;
              };
            }
            
            // 인스턴스의 생성
            const circle1 = new Circle(5);  // 반지름이 5인 Circle 객체를 생성
            const circle2 = new Circle(10); // 반지름이 10인 Circle 객체를 생성
            
            console.log(circle1.getDiameter()); // 10
            console.log(circle2.getDiameter()); // 20
            ```
            
            - this
                - this 는 객체 자신의 프로퍼티나 메서드를 참조하기 위한 **************************************************************자기 참조 변수(self-referencing variable)**************************************************************다. 
                **this가 가리키는 값, 즉 this 바인딩은 함수 호출 방식에 따라 동적으로 결정된다.**
                    
                    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d6e2606f-02ac-48ef-b8e7-c50fd47f733c/Untitled.png)
                    
        - 일반 함수와 동일한 방법으로 생성자 함수를 정의하고 **new 연산자와 함께 호출하면 해당 함수는 생성자 함수로 동작한다.**
            
            ```jsx
            // new 연산자와 함께 호출하지 않으면 생성자 함수로 동작하지 않는다.
            // 즉, 일반 함수로서 호출된다.
            const circle3 = Circle(15);
            
            // 일반 함수로서 호출된 Circle은 반환문이 없으므로 암묵적으로 undefined를 반환한다.
            console.log(circle3); // undefined
            
            // 일반 함수로서 호출된 Circle내의 this는 전역 객체를 가리킨다.
            console.log(radius); // 15
            ```
            
    - 생성자 함수의 인스턴스 생성 과정
        - 생성자 함수의 역할은 프로퍼티 구조가 동일한 인스턴스를 생성하기 위한 템플릿(클래스)으로서 동작하여 ****************************************인스턴스를 생성****************************************하는 것과 **********************************************************************************************************************************************************************************생성된 인스턴스를 초기화(인스턴스 프로퍼티 추가 및 초기값 할당)**********************************************************************************************************************************************************************************하는 것이다.
        - 1. 인스턴스 생성과 this 바인딩
            - 암묵적으로 빈 객체가 생성된다 ( 이 빈 객체가 바로 생성자 함수가 생성한 인스턴스다. )
            암묵적으로 생성된 빈 객체(인스턴스) 는 this 에 바인딩된다.
            (이 처리는 함수 몸체에 코드가 한 줄씩 실행되는 런타임 이전에 실행)
        - 2. 인스턴스 초기화
            - 생성자 함수에 기술되어 있는 코드가 한 줄씩 실행되어 this 에 바인딩되어 있는 인스턴스를 초기화한다.
        - 3. 인스턴스 반환
            - 생성자 함수 내부에서 모든 처리가 끝나면 완성된 인스턴스가 바인딩된 this를 암묵적으로 반환한다.
            (만약 this 가 아닌 다른 객체를 명시적으로 반환하면 this가 반환되지 못하고 return 문에 명시한 객체가 반환된다.)
            (명시적으로 원시 값을 반환하면 원시 값 반환은 무시되고 암묵적으로 this 를 반환한다. )
            따라서, **생성자 함수 내부에서 return 문을 반드시 생략해야 한다.**
        
        ```jsx
        function Circle(radius) {
          // 1. 암묵적으로 인스턴스가 생성되고 this에 바인딩된다.
        
          // 2. this에 바인딩되어 있는 인스턴스를 초기화한다.
          this.radius = radius;
          this.getDiameter = function () {
            return 2 * this.radius;
          };
        
          // 3. 암묵적으로 this를 반환한다.
          /* 명시적으로 원시값을 반환하면 원시값 반환은 무시되고 암묵적으로 this가 반환된다.
          return 100;
        	// 명시적으로 객체를 반환하면 암묵적인 this 반환이 무시된다.
        	return {};
        	*/
        }
        
        // 인스턴스 생성. Circle 생성자 함수는 명시적으로 반환한 객체를 반환한다.
        const circle = new Circle(1);
        console.log(circle); // Circle {radius: 1, getDiameter: ƒ}
        ```
        
    - 내부 메서드 [[Call]] 과 [[Construct]]
        - 생성자 함수로서 호출한다는 것은 new 연산자와 함께 호출하여 객체를 생성하는 것을 의미한다.
        - 함수는 객체이므로 일반 객체(ordinary object)와 동일하게 동작할 수 있다.
        (함수 객체는 일반 객체가 가지고 있는 내부 슬롯과 내부 메서드를 모두 가지고 있기 때문이다.)
        - **일반 객체는 호출할 수 없지만 함수는 호출할 수 있다.**
        - 함수로서 동작하기 위해 함수 객체만을 위한 [[Environment]], [[FormalParameters]] 등의 내부 슬롯과 [[Call]], [[Construct]] 같은 내부 메서드를 추가로 가지고 있다.
        - 내부 메서드 [[Call]] 을 갖는 함수 객체를 callable이라 하며, 내부 메서드 [[Construct]]를 갖는 함수 객체를 constructor, [[Construct]]를 갖지 않는 함수 객체를 non-constructor 라고 부른다.
            
            ![모든 함수 객체는 callable 이지만 모든 함수 객체가 constructor 인 것은 아니다.](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f1ce36a0-ec4f-4cbf-bd3d-20ef9190dd1c/Untitled.png)
            
            모든 함수 객체는 callable 이지만 모든 함수 객체가 constructor 인 것은 아니다.
            
    - constructor와 non-constructor의 구분
        - constructor : 함수 선언문, 함수 표현식, 클래스(클래스도 함수다)
        - non-constructor : 메서드(ES6 메서드 축약 표현), 화살표 함수
        
        ```jsx
        // 일반 함수 정의: 함수 선언문, 함수 표현식
        function foo() {}
        const bar = function () {};
        // 프로퍼티 x의 값으로 할당된 것은 일반 함수로 정의된 함수다. 이는 메서드로 인정하지 않는다.
        const baz = {
          x: function () {}
        };
        
        // 일반 함수로 정의된 함수만이 constructor이다.
        new foo();   // -> foo {}
        new bar();   // -> bar {}
        new baz.x(); // -> x {}
        
        // 화살표 함수 정의
        const arrow = () => {};
        
        new arrow(); // TypeError: arrow is not a constructor
        
        // 메서드 정의: ES6의 메서드 축약 표현만을 메서드로 인정한다.
        const obj = {
          x() {}
        };
        
        new obj.x(); // TypeError: obj.x is not a constructor
        ```
        
    - new 연산자
        - 일반 함수와 생성자 함수에 특별한 형식적 차이는 없다.
        따라서 **생성자 함수는 일반적으로 첫 문자를 대문자로 기술하는 파스칼 케이스로 명명하여 일반 함수와 구별할 수 있도록 노력한다.**
        new 연산자와 함께 함수를 호출하면 해당 함수는 생성자 함수로 동작한다.
        - Circle 함수를 new 연산자와 함께 생성자 함수로서 호출하면 함수 내부의 this는 Circle 생성자 함수가 생성할 인스턴스를 가리킨다.
        하지만 Circle 함수를 일반적인 함수로서 호출하면 함수 내부의 this는 전역 객체 window를 가리킨다.
            
            ```jsx
            // 생성자 함수
            function Circle(radius) {
              this.radius = radius;
              this.getDiameter = function () {
                return 2 * this.radius;
              };
            }
            
            // new 연산자 없이 생성자 함수 호출하면 일반 함수로서 호출된다.
            const circle = Circle(5);
            console.log(circle); // undefined
            
            // 일반 함수 내부의 this는 전역 객체 window를 가리킨다.
            console.log(radius); // 5
            console.log(getDiameter()); // 10
            
            circle.getDiameter();
            // TypeError: Cannot read property 'getDiameter' of undefined
            ```
            
    - new.target
        - 함수 내부에서 new.target을 사용하면 new 연산자와 함께 생성자 함수로서 호출되었는지 확인할 수 있다.
        **new 연산자와 함께 생성자 함수로서 호출되면 함수 내부의 new.target은 함수 자신을 가리킨다.
        new 연산자없이 일반 함수로서 호출된 함수 내부의 new.target은 undefined다.**
            
            ```jsx
            // 생성자 함수
            function Circle(radius) {
              // 이 함수가 new 연산자와 함께 호출되지 않았다면 new.target은 undefined다.
              if (!new.target) {
                // new 연산자와 함께 생성자 함수를 재귀 호출하여 생성된 인스턴스를 반환한다.
                return new Circle(radius);
              }
            
              this.radius = radius;
              this.getDiameter = function () {
                return 2 * this.radius;
              };
            }
            
            // new 연산자 없이 생성자 함수를 호출하여도 new.target을 통해 생성자 함수로서 호출된다.
            const circle = Circle(5);
            console.log(circle.getDiameter());  // 10
            ```
            
            - new.target은 ES6에서 도입된 최신 문법으로, new.target을 사용할 수 없는 상황이라면 **스코프 세이프 생성자 패턴**을 사용할 수 있다.
        
    - 대부분의 빌트인 생성자 함수(Object, String, Number, Boolean, Function, Array, Date, RegExp, Promise 등)는 new 연산자와 함께 호출되었는지를 확인한 후 적절한 값을 반환한다.
        - 예를 들어, Object와 Function 생성자 함수는 new 연산자 없이 호출해도 new 연산자와 함께 호출했을 때와 동일하게 동작한다.
            
            ```jsx
            let obj = new Object();
            console.log(obj); // {}
            
            obj = Object();
            console.log(obj); // {}
            
            let f = new Function('x', 'return x ** x');
            console.log(f); // ƒ anonymous(x) { return x ** x }
            
            f = Function('x', 'return x ** x');
            console.log(f); // ƒ anonymous(x) { return x ** x }
            ```
            
        - 하지만 String, Number, Boolean 생성자 함수는 new 연산자와 함께 호출했을 때의 String, Number, Boolean 객체를 생성하여 반환하지만 new 연산자 없이 호출하면 문자열, 숫자, 불리언 값을 반환한다. 
        ( 이를 통해 데이터 타입을 변환하기도 한다. )
            
            ```jsx
            const str = String(123);
            console.log(str, typeof str); // 123 string
            
            const num = Number('123');
            console.log(num, typeof num); // 123 number
            
            const bool = Boolean('true');
            console.log(bool, typeof bool); // true boolean
            ```