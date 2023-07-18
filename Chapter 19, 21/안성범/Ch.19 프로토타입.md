### CH. 19 프로토타입

- 자바스크립트는 명령형(imperative), 함수형(functional), 프로토타입 기반(prototype-based) 객체지향 프로그래밍(OOP; Object Ori-ented Programming)을 지원하는 멀티 패러다임 프로그래밍 언어이다.
→ 자바스크립트는 객체 기반의 프로그래밍 언어이며 ****************************************************************************************************************************************자바스크립트를 이루고 있는 거의 “모든 것”이 객체****************************************************************************************************************************************이다.
- 객체지향 프로그래밍
    - 객체지향 프로그래밍은 실세계의 실체(사물이나 개념)를 인식하는 철학적 사고를 프로그래밍에 접목하려는 시도에서 시작한다.
    실체는 특징이나 성질을 나타내는 ******************************************************************속성(attribute/property)******************************************************************을 가지고 있고, 이를 통해 실체를 인식하거나 구별할 수 있다.
    → 다양한 속성 중에서 프로그램에 필요한 속성만 간추려 내어 표현하는 것을 ****************************추상화(abstraction)****************************이라 한다.
    - 프로그래머(subject, 주체)는 속성으로 표현된 객체(object)를 다른 객체와 구별하여 인식할 수 있다.
    → ********************************************************************************************************************************************************************************속성을 통해 여러 개의 값을 하나의 단위로 구성한 복합적인 자료구조********************************************************************************************************************************************************************************를 객체라 한다.
    - 객체는 **************************************************************************************************************상태 데이터와 동작을 하나의 논리적인 단위로 묶은 복합적인 자료구조**************************************************************************************************************
    객체의 상태 데이터(property, 프로퍼티) , 동작(method, 메서드)
- 상속과 프로토타입
    - 상속(inheritance)은 객체지향 프로그래밍의 핵심 개념으로, 어떤 객체의 프로퍼티 또는 메서드를 다른 객체가 상속받아 그대로 사용할 수 있는 것을 말한다.
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/26263853-95f4-4633-ad06-e9c442d1d206/Untitled.png)
        
    - 동일한 생성자 함수에 의해 생성된 모든 인스턴스가 동일한 메서드를 중복 소유하는 것은 메모리를 불필요하게 낭비한다. ( 인스턴스를 생성할 때마다 메서드를 생성하므로 퍼포먼스에도 악영향을 준다. )
    → 상속을 통해 불필요한 중복 제거 가능
    ****************************************************************************************************자바스크립트는 프로토타입(prototype)을 기반으로 상속을 구현한다.****************************************************************************************************
        
        ```jsx
        // 생성자 함수
        function Circle(radius) {
          this.radius = radius;
        }
        
        // Circle 생성자 함수가 생성한 모든 인스턴스가 getArea 메서드를
        // 공유해서 사용할 수 있도록 프로토타입에 추가한다.
        // 프로토타입은 Circle 생성자 함수의 prototype 프로퍼티에 바인딩되어 있다.
        Circle.prototype.getArea = function () {
          return Math.PI * this.radius ** 2;
        };
        
        // 인스턴스 생성
        const circle1 = new Circle(1);
        const circle2 = new Circle(2);
        
        // Circle 생성자 함수가 생성한 모든 인스턴스는 부모 객체의 역할을 하는
        // 프로토타입 Circle.prototype으로부터 getArea 메서드를 상속받는다.
        // 즉, Circle 생성자 함수가 생성하는 모든 인스턴스는 하나의 getArea 메서드를 공유한다.
        console.log(circle1.getArea === circle2.getArea); // true
        
        console.log(circle1.getArea()); // 3.141592653589793
        console.log(circle2.getArea()); // 12.566370614359172
        ```
        
        ![상속에 의한 메서드 공유](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c3bb3436-a0ea-425b-a445-1314f90c06a2/Untitled.png)
        
        상속에 의한 메서드 공유
        
    - Circle 생성자 함수가 생성한 모든 인스턴스는 자신의 프로토타입, 즉 상위(부모) 객체 역할을 하는 Circle.prototype의 모든 프로퍼티와 메서드를 상속받는다.
    → 상속은 ********************************코드의 재사용********************************이란 관점에서 매우 유용하다.
- 프로토타입 객체
    - 프로토타입 객체(줄여서 프로토타입)란 객체지향 프로그래밍의 근간을 이루는 객체 간 상속을 구현하기 위해 사용된다.
    - 모든 객체는 [[Prototype]]이라는 내부 슬롯을 가지며, 이 내부 슬롯의 값은 프로토타입의 참조(null인 경우도 있다.) 
    [[Prototype]]에 저장되는 프로토타입은 객체 생성 방식에 의해 결정된다.
    ex> 객체 리터럴에 의해 생성된 객체의 프로토타입은 Object.prototype이고 생성자 함수에 의해 생성된 객체의 프로토타입은 생성자 함수의 prototype 프로퍼티에 바인딩되어 있는 객체이다.
    - 모든 객체는 하나의 프로토타입을 갖는다. 
    모든 프로토타입은 생성자 함수와 연결되어 있다.
        
        ![객체와 프로토타입과 생성자 함수는 서로 연결되어 있다.](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0f846ede-afde-431d-9b0c-75cc1c136734/Untitled.png)
        
        객체와 프로토타입과 생성자 함수는 서로 연결되어 있다.
        
    - __ proto __ 접근자 프로퍼티
        - **모든 객체는 __ proto __ 접근자 프로퍼티를 통해 자신의 프로토타입, 즉 [[Prototype]] 내부 슬롯에 간접적으로 접근할 수 있다.**
        - __ proto __ 는 접근자 프로퍼티다.
            - __ proto __ 접근자 프로퍼티를 통해 간접적으로 [[Prototype]] 내부 슬롯의 값, 즉 프로토타입에 접근할 수 있다.
            - 접근자 프로퍼티는 **자체적으로 값을 갖지 않고 다른 데이터 프로퍼티의 값을 읽거나 저장할 때 사용하는 접근자 함수**([[Get]], [[Set]]) **프로퍼티 어트리뷰트로 구성된 프로퍼티**이다.
                
                ```jsx
                const obj = {};
                const parent = { x: 1 };
                
                // getter 함수인 get __proto__가 호출되어 obj 객체의 프로토타입을 취득
                obj.__proto__;
                // setter함수인 set __proto__가 호출되어 obj 객체의 프로토타입을 교체
                obj.__proto__ = parent;
                
                console.log(obj.x); // 1
                ```
                
        - __ proto __ 접근자 프로퍼티는 상속을 통해 사용된다.
            - __ proto __ 접근자 프로퍼티는 객체가 직접 소유하는 프로퍼티가 아니라 Object.prototype의 프로퍼티이다.
            모든 객체는 상속을 통해 Object.prototype.__proto__ 접근자 프로퍼티를 사용할 수 있다.
                
                ```jsx
                const person = { name: 'Lee' };
                
                // person 객체는 __proto__ 프로퍼티를 소유하지 않는다.
                console.log(person.hasOwnProperty('__proto__')); // false
                
                // __proto__ 프로퍼티는 모든 객체의 프로토타입 객체인 Object.prototype의 접근자 프로퍼티다.
                console.log(Object.getOwnPropertyDescriptor(Object.prototype, '__proto__'));
                // {get: ƒ, set: ƒ, enumerable: false, configurable: true}
                
                // 모든 객체는 Object.prototype의 접근자 프로퍼티 __proto__를 상속받아 사용할 수 있다.
                console.log({}.__proto__ === Object.prototype); // true
                ```
                
        - __ proto __ 접근자 프로퍼티를 통해 프로토타입에 접근하는 이유
            - **[[Prototype]] 내부 슬롯의 값, 즉 프로토타입에 접근하기 위해 접근자 프로퍼티를 사용하는 이유는 상호 참조에 의해 프로토타입 체인이 생성되는 것을 방지**하기 위해서다.
                
                ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a2a29bee-c44b-4eaa-a3fe-8c32c42aa93c/Untitled.png)
                
            - 프로토타입 체인은 단방향 링크드 리스트로 구현되어야 한다.
            → 아무런 체크 없이 무조건적으로 프로토타입을 교체할 수 없도록 
            __ proto __ 접근자 프로퍼티를 통해 프로토타입에 접근하고 교체하도록 구현되어 있다.
        - __ proto __ 접근자 프로퍼티를 코드 내에서 직접 사용하는 것은 권장하지 않는다.
            - 코드 내에서 __ proto __ 접근자 프로퍼티를 직접 사용하는 것은 권장하지 않는다.
            → __ proto __ 접근자 프로퍼티 대신 프로토타입의 참조를 취득하고 싶은 경우에는 Object.getPrototypeOf 메서드를 사용하고, 프로토타입을 교체하고 싶은 경우에는 Object.setPrototypeOf 메서드를 사용할 것을 권장한다.
    - 함수 객체의 prototype 프로퍼티
        - **************************************************************함수 객체만이 소유하는 prototype 프로퍼티는 생성자 함수가 생성할 인스턴스의 프로토타입을 가리킨다.
        →************************************************************** prototype 프로퍼티는 생성자 함수가 생성할 객체(인스턴스)의 프로토타입을 가리킨다.
        - 따라서 생성자 함수로서 생성할 수 없는 함수(non-constructor)는 prototype 프로퍼티를 소유하지 않으며 프로토타입도 생성하지 않는다.
            
            ```jsx
            // 화살표 함수는 non-constructor다.
            const Person = name => {
              this.name = name;
            };
            
            // non-constructor는 prototype 프로퍼티를 소유하지 않는다.
            console.log(Person.hasOwnProperty('prototype')); // false
            
            // non-constructor는 프로토타입을 생성하지 않는다.
            console.log(Person.prototype); // undefined
            
            // ES6의 메서드 축약 표현으로 정의한 메서드는 non-constructor다.
            const obj = {
              foo() {}
            };
            
            // non-constructor는 prototype 프로퍼티를 소유하지 않는다.
            console.log(obj.foo.hasOwnProperty('prototype')); // false
            
            // non-constructor는 프로토타입을 생성하지 않는다.
            console.log(obj.foo.prototype); // undefined
            ```
            
        - ******************************************************************************************************************모든 객체가 가지고 있는(엄밀히 말하면 Object.prototype으로부터 상속받은) __proto__ 접근자 프로퍼티와 함수 객체만이 가지고 있는 prototype 프로퍼티는 결국 동일한 프로토타입을 가리킨다.****************************************************************************************************************** 
        ( 하지만 이들 프로퍼티를 사용하는 주체가 다르다. )
            
            ```jsx
            // 생성자 함수
            function Person(name) {
              this.name = name;
            }
            
            const me = new Person('Lee');
            
            // 결국 Person.prototype과 me.__proto__는 결국 동일한 프로토타입을 가리킨다.
            console.log(Person.prototype === me.__proto__);  // true
            ```
            
            ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c36ea0d8-d894-430c-9083-df863c458666/Untitled.png)
            
            ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fcfacd0f-c848-4e96-9448-d846f4883b41/Untitled.png)
            
    - 프로토타입의 constructor 프로퍼티와 생성자 함수
        - 모든 프로토타입은 constructor 프로퍼티를 갖는다.
        이 constructor 프로퍼티는 prototype 프로퍼티로 자신을 참조하고 있는 생성자 함수를 가리킨다.
        ( 이 연결은 함수 객체가 생성될 때 이뤄진다. )
            
            ```jsx
            // 생성자 함수
            function Person(name) {
              this.name = name;
            }
            
            const me = new Person('Lee');
            
            // me 객체의 생성자 함수는 Person이다.
            console.log(me.constructor === Person);  // true
            ```
            
            ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9788978f-0ec8-48bd-8236-a515df9ca20a/Untitled.png)
            
- 리터럴 표기법에 의해 생성된 객체의 생성자 함수와 프로토타입
    - 생성자 함수에 의해 생성된 인스턴스도 있지만, 
    **리터럴 표기법에 의한 객체 생성 방식**과 같이 명시적으로 new 연산자와 함께 생성자 함수를 호출하여 인스턴스를 생성하지 않는 **객체 생성 방식**도 있다.
        
        ```jsx
        // 객체 리터럴
        const obj = {};
        
        // 함수 리터럴
        const add = function (a, b) { return a + b; };
        
        // 배열 리터럴
        const arr = [1, 2, 3];
        
        // 정규표현식 리터럴
        const regexp = /is/ig;
        ```
        
        - 리터럴 표기법에 의해 생성된 객체도 물론 프로토타입이 존재한다.
        하지만 **리터럴 표기법에 의해 생성된 객체의 경우** **프로토타입의 constructor 프로퍼티가 가리키는 생성자 함수가 반드시 객체를 생성한 생성자 함수라고 단정할 수는 없다.**
        
        ```jsx
        // obj 객체는 Object 생성자 함수로 생성한 객체가 아니라 객체 리터럴로 생성했다.
        const obj = {};
        
        // 하지만 obj 객체의 생성자 함수는 Object 생성자 함수다.
        console.log(obj.constructor === Object); // true
        
        // foo 함수는 Function 생성자 함수로 생성한 함수 객체가 아니라 함수 선언문으로 생성했다.
        function foo() {}
        
        // 하지만 constructor 프로퍼티를 통해 확인해보면 함수 foo의 생성자 함수는 Function 생성자 함수다.
        console.log(foo.constructor === Function); // true
        ```
        
        - 리터럴 표기법에 의해 생성된 객체도 상속을 위해 프로토타입이 필요하다.
        → 리터럴 표기법에 의해 생성된 객체도 가상적인 생성자 함수를 갖는다.
        프로토타입은 생성자 함수와 더불어 생성되며 prototype, constructor 프로퍼티에 의해 연결되어 있기 때문이다.
        ****************************************************************************************************************************************************************************************************************************( 프로토타입과 생성자 함수는 단독으로 존재할 수 없고 언제나 쌍(pair)으로 존재한다. )****************************************************************************************************************************************************************************************************************************
        - 리터럴 표기법(객체 리터럴, 함수 리터럴, 배열 리터럴, 정규 표현식 리터럴 등)에 의해 생성된 객체는 생성자 함수에 의해 생성된 객체는 아니다.
        ( 하지만 결국 객체로서 동일한 특성을 갖는다. )
        → 프로토타입의 constructor 프로퍼티를 통해 연결되어 있는 생성자 함수를 리터럴 표기법으로 생성한 객체를 생성한 생성자 함수로 생각해도 크게 무리는 없다.
            
            ![리터럴 표기법에 의해 생성된 객체의 생성자 함수와 프로토타입](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/01b72716-0fbf-463d-bd9e-8e6b1a42e875/Untitled.png)
            
            리터럴 표기법에 의해 생성된 객체의 생성자 함수와 프로토타입
            
- 프로토타입의 생성 시점
    - 객체는 리터럴 표기법 또는 생성자 함수에 의해 생성되므로 결국 모든 객체는 생성자 함수와 연결되어 있다.
    - ****************************************************************************************************************************************************************프로토타입은 생성자 함수가 생성되는 시점에 더불어 생성된다.****************************************************************************************************************************************************************
        - 사용자 정의 생성자 함수와 프로토타입 생성 시점
            - 생성자 함수로서 호출할 수 있는 함수(constructor)는 함수 정의가 평가되어 함수 객체를 생성하는 시점에 프로토타입도 더불어 생성된다.
            (non-constructor 는 프로토타입이 생성되지 않는다.)
            - 빌트인 생성자 함수가 아닌 사용자 정의 생성자 함수는 자신이 평가되어 함수 객체로 생성되는 시점에 프로토타입도 더불어 생성된다.
            (생성된 프로토타입의 프로토타입은 언제나 Object.prototype 이다.)
                
                ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1cc6131b-99f3-4242-949b-de06a07570bb/Untitled.png)
                
        - 빌트인 생성자 함수와 프로토타입 생성 시점
            - 빌트인 생성자 함수도 일반 함수와 마찬가지로 빌트인 생성자 함수가 생성되는 시점에 프로토타입이 생성된다.
            모든 빌트인 생성자 함수는 전역 객체가 생성되는 시점에 생성된다.
            ( 생성된 프로토타입은 빌트인 생성자 함수의 prototype 프로퍼티에 바인딩된다. )
            - 객체가 생성되기 이전에 생성자 함수와 프로토타입은 이미 객체화되어 존재한다.
            ( ****************************************************************************************************************************************************************************************************************************************************************************************************************************이후 생성자 함수 또는 리터럴 표기법으로 객체를 생성하면 프로토타입은 생성된 객체의 [[Prototype]] 내부 슬롯에 할당된다.**************************************************************************************************************************************************************************************************************************************************************************************************************************** )
            생성된 객체는 프로토타입을 상속받는다.
                
                ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ade56af6-9b4c-49ad-82af-49521dd5d1ed/Untitled.png)
                
        - 객체 생성 방식과 프로토타입의 결정
            - 다양한 방식으로 생성된 모든 객체는 각 방식마다 세부적인 객체 생성 방식의 차이는 있으나 추상 연산 OrdinaryObjectCreate에 의해 생성된다는 공통점이 있다.
            프로토타입은 추상 연산 OrdinaryObjectCreate에 전달되는 인수에 의해 결정된다.
            ( 이 인수는 객체가 생성되는 시점에 객체 생성 방식에 의해 결정된다. )
            - 객체 리터럴에 의해 생성된 객체의 프로토타입
                - 자바스크립트 엔진은 객체 리터럴을 평가하여 객체를 생성할 때 추상 연산 OrdinaryObjectCreate를 호출한다.
                ( 이 때 추상 연산 OrdinaryObjectCreate에 전달되는 프로토타입은 Object.prototype 이다. )
                    
                    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/764089b3-5424-4f60-ae8c-88af5a8b5b9c/Untitled.png)
                    
            - Object 생성자 함수에 의해 생성된 객체의 프로토타입
                - Object 생성자 함수를 인수 없이 호출하면 빈 객체가 생성된다.
                Object 생성자 함수를 호출하면 객체 리터럴과 마찬가지로 추상 연산 OrdinaryObjectCreate가 호출된다.
                ( 이때 추상 연산 OrdinaryObjectCreate에 전달되는 프로토타입은 Object.prototype 이다. )
                - **객체 리터럴과 Object 생성자 함수에 의한 객체 생성 방식의 차이는 프로퍼티를 추가하는 방식에 있다.
                (** 객체 리터럴 방식은 객체 리터럴 내부에 프로퍼티를 추가하지만 Object 생성자 함수 방식은 일단 빈 객체를 생성한 이후 프로퍼티를 추가해야 한다. )
                    
                    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1d28e96b-4d6d-4c3c-9a68-d41d59b643f5/Untitled.png)
                    
            - 생성자 함수에 의해 생성된 객체의 프로토타입
                - new 연산자와 함께 생성자 함수를 호출하여 인스턴스를 생성하면 다른 객체 생성 방식과 마찬가지로 추상 연산 OrdinaryObjectCreate가 호출된다.
                (이 때 추상 연산 OrdinaryObjectCreate에 전달되는 프로토타입은 생성자 함수의 prototype 프로퍼티에 바인딩되어 있는 객체이다. )
                - 사용자 정의 생성자 함수 Person.prototype 의 프로퍼티는 constructor 뿐이다.
                    
                    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/adc93707-f7be-4374-94a2-ac7000531603/Untitled.png)
                    
                - 일반 객체와 같이 프로토타입에도 프로퍼티를 추가/삭제 할 수 있다 
                ( 이렇게 추가/삭제된 프로퍼티는 프로토타입 체인에 즉각 반영된다. )
                    
                    ```jsx
                    function Person(name) {
                      this.name = name;
                    }
                    
                    // 프로토타입 메서드
                    Person.prototype.sayHello = function () {
                      console.log(`Hi! My name is ${this.name}`);
                    };
                    
                    const me = new Person('Lee');
                    const you = new Person('Kim');
                    
                    me.sayHello();  // Hi! My name is Lee
                    you.sayHello(); // Hi! My name is Kim
                    ```
                    
                    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d14ed3fe-bdc0-4180-ae18-d1fa3fc2b406/Untitled.png)
                    
    
- **프로토타입 체인**
    - **자바스크립트는 객체의 프로퍼티(메서드 포함)에 접근하려고 할 때 해당 객체에 접근하려는 프로퍼티가 없다면 [[Prototype]] 내부 슬롯의 참조를 따라 자신의 부모 역할을 하는 프로토타입의 프로퍼티를 순차적으로 검색한다.
    ( 이를 프로토타입 체인 이라 한다. )
    프로토타입 체인은 자바스크립트가 객체지향 프로그래밍의 상속을 구현하는 메커니즘이다.**
    
    ```jsx
    function Person(name) {
      this.name = name;
    }
    
    // 프로토타입 메서드
    Person.prototype.sayHello = function () {
      console.log(`Hi! My name is ${this.name}`);
    };
    
    const me = new Person('Lee');
    
    // hasOwnProperty는 Object.prototype의 메서드다.
    console.log(me.hasOwnProperty('name')); // true
    ```
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9f5254d7-b6be-4cd5-a8c0-636c1b59fb56/Untitled.png)
    
    ```jsx
    // hasOwnProperty는 Object.prototype의 메서드다.
    // me 객체는 프로토타입 체인을 따라 hasOwnProperty 메서드를 검색하여 사용한다.
    me.hasOwnProperty('name'); // -> true
    ```
    
    - me.hasOwnProperty(’name’)과 같이 메서드를 호출하면 자바스크립트 엔진은 다음과 같은 과정을 거쳐 메서드를 검색한다.
    ( 프로퍼티를 참조하는 경우도 마찬가지다.)
    1. hasOwnProperty 메서드를 호출한 me 객체에서 hasOwnProperty 메서드를 검색한다. 
    → me 객체에는 hasOwnProperty 메서드가 없으므로 프로토타입 체인을 따라([[Prototype]] 내부 슬롯에 바인딩되어 있는 프로토타입(Person.prototype)으로 이동하여 hasOwnProperty 메서드를 검색한다.
    2. Person.prototype에도 hasOwnProperty 메서드가 없으므로 프로토타입 체인을 따라, [[Prototype]] 내부 슬롯에 바인딩되어 있는 프로토타입(Object.prototype)으로 이동하여 hasOwnProperty 메서드를 검색한다.
    3. Object.prototype에는 hasOwnProperty 메서드가 존재한다. 자바스크립트 엔진은 Object.prototype.hasOwnProperty 메서드를 호출한다.
    이 때, Object.prototype.hasOwnProperty 메서드의 this에는 me 객체가 바인딩된다.
    - 프로토타입 체인의 최상위에 위치하는 객체는 언제나 Object.prototype이다. 
    따라서 모든 객체는 Object.prototype을 상속받는다.
    ( **********************************************************************************************************************************Object.prototype 을 프로토타입 체인의 종점(end of prototype chain)**********************************************************************************************************************************이라 한다. )
    → Object.prototype의 프로토타입, 즉 [[Prototype]] 내부 슬롯의 값은 null이다.
     ( 프로토타입 체인의 종점인 Object.prototype에서도 프로퍼티를 검색할 수 없는 경우 undefined 를 반환한다. **********************************************************************************이 때 에러가 발생하지 않는다.********************************************************************************** )
    - **프로토타입 체인은 상속과 프로퍼티 검색을 위한 메커니즘**이라 할 수 있다.
    반대로, 프로퍼티가 아닌 식별자는 스코프 체인에서 검색한다.
    → ********************************************************************************************************************스코프 체인은 식별자 검색을 위한 메커니즘********************************************************************************************************************이라 할 수 있다.
    - 아래 예제의 경우, 
    스코프체인에서 me 식별자 검색
    (me 식별자는 전역에서 선언되었으므로 전역 스코프에서 검색)
    → me 객체의 프로토타입 체인에서 hasOwnProperty 메서드 검색
    ( 이처럼 ********************************************************************************************************************************************************************************************************************************************************************************************************************************************************************스코프 체인과 프로토타입 체인은 서로 연관없이 별도로 동작하는 것이 아니라 서로 협력하여 식별자와 프로퍼티를 검색하는 데 사용된다.******************************************************************************************************************************************************************************************************************************************************************************************************************************************************************** )
        
        ```jsx
        me.hasOwnProperty('name');
        ```
        
- 오버라이딩과 프로퍼티 섀도잉
    
    ```jsx
    const Person = (function () {
      // 생성자 함수
      function Person(name) {
        this.name = name;
      }
    
      // 프로토타입 메서드
      Person.prototype.sayHello = function () {
        console.log(`Hi! My name is ${this.name}`);
      };
    
      // 생성자 함수를 반환
      return Person;
    }());
    
    const me = new Person('Lee');
    
    // 인스턴스 메서드
    me.sayHello = function () {
      console.log(`Hey! My name is ${this.name}`);
    };
    
    // 인스턴스 메서드가 호출된다. 프로토타입 메서드는 인스턴스 메서드에 의해 가려진다.
    me.sayHello(); // Hey! My name is Lee
    ```
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6da1c7b6-5cd3-48a2-9c15-ee2308e1f52c/Untitled.png)
    
    - 프로토타입의 프로퍼티와 같은 이름의 프로퍼티를 인스턴스에 추가하면 프로토타입 체인을 따라 프로토타입 프로퍼티를 검색하여 프로토타입 프로퍼티를 덮어쓰는 것이 아니라 인스턴스 프로퍼티로 추가한다.
    ( 이 때 인스턴스 메서드 sayHello는 프로토타입 메서드 sayHello를 오버라이딩했고 프로토타입 메서드 sayHello 는 가려진다. )
    - 하위 객체를 통해 프로토타입의 프로퍼티를 변경 또는 삭제하는 것은 불가능하다.
    ( 하위 객체를 통해 프로토타입에 get 액세스는 허용되나 set 액세스는 허용되지 않는다. )
    → 프로토타입 프로퍼티를 변경 또는 삭제하려면 하위 객체를 통해 프로토타입 체인으로 접근하는 것이 아니라 프로토타입에 직접 접근해야한다.
- 프로토타입의 교체
    - 프로토타입은 임의의 다른 객체로 변경할 수 있다.
    → 부모 객체인 프로토타입을 동적으로 변경할 수 있다.
    ( 이러한 특징을 활용하여 객체 간의 상속 관계를 동적으로 변경할 수 있다. )
    - 프로토타입은 생성자 함수 또는 인스턴스에 의해 교체할 수 있다.
    - 생성자 함수에 의한 프로토타입의 교체
        
        ```jsx
        const Person = (function () {
          function Person(name) {
            this.name = name;
          }
        
          // ① 생성자 함수의 prototype 프로퍼티를 통해 프로토타입을 교체
          Person.prototype = {
            sayHello() {
              console.log(`Hi! My name is ${this.name}`);
            }
          };
        
          return Person;
        }());
        
        const me = new Person('Lee');
        ```
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c3638e6f-a7a4-4711-99c0-54d1550fb9f1/Untitled.png)
        
        - 프로토타입으로 교체한 객체 리터럴에는 constructor 프로퍼티가 없다.
        ( constructor 프로퍼티는 자바스크립트 엔진이 프로토타입을 생성할 때 암묵적으로 추가한 프로퍼티다. )
        → 따라서 me 객체의 생성자 함수를 검색하면 Person이 아닌 Object가 나온다.
            
            ```jsx
            // 프로토타입을 교체하면 constructor 프로퍼티와 생성자 함수 간의 연결이 파괴된다.
            console.log(me.constructor === Person); // false
            // 프로토타입 체인을 따라 Object.prototype의 constructor 프로퍼티가 검색된다.
            console.log(me.constructor === Object); // true
            ```
            
            ```jsx
            const Person = (function () {
              function Person(name) {
                this.name = name;
              }
            
              // 생성자 함수의 prototype 프로퍼티를 통해 프로토타입을 교체
              Person.prototype = {
                // constructor 프로퍼티와 생성자 함수 간의 연결을 설정
                constructor: Person,
                sayHello() {
                  console.log(`Hi! My name is ${this.name}`);
                }
              };
            
              return Person;
            }());
            
            const me = new Person('Lee');
            
            // constructor 프로퍼티가 생성자 함수를 가리킨다.
            console.log(me.constructor === Person); // true
            console.log(me.constructor === Object); // false
            ```
            
    - 인스턴스에 의한 프로토타입의 교체
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9b1af065-ec64-454c-84a2-b0d6a85d97ec/Untitled.png)
        
        - 
    - 프로토타입 교체를 통해 객체 간의 상속 관계를 동적으로 변경하는 것은 꽤나 번거롭다.
    → **프로토타입은 직접 교체하지 않는 것이 좋다.
    (** 상속 관계를 인위적으로 설정하려면 ‘직접 상속’이 더 편리하고 안전,
    클래스를 사용하면 간편하고 직관적으로 상속 관계를 구현할 수 있다. )
- instanceof 연산자
    
    ```jsx
    객체 instanceof 생성자 함수
    ```
    
    - **우변의 생성자 함수의 prototype에 바인딩된 객체가 좌변의 객체의 프로토타입 체인 상에 존재하면 true로 평가, 그렇지 않으면 false로 평가.**
    
    ```jsx
    // 생성자 함수
    function Person(name) {
      this.name = name;
    }
    
    const me = new Person('Lee');
    
    // 프로토타입으로 교체할 객체
    const parent = {};
    
    // 프로토타입의 교체
    Object.setPrototypeOf(me, parent);
    
    // Person 생성자 함수와 parent 객체는 연결되어 있지 않다.
    console.log(Person.prototype === parent); // false
    console.log(parent.constructor === Person); // false
    
    // parent 객체를 Person 생성자 함수의 prototype 프로퍼티에 바인딩한다.
    Person.prototype = parent;
    
    // Person.prototype이 me 객체의 프로토타입 체인 상에 존재하므로 true로 평가된다.
    console.log(me instanceof Person); // true
    
    // Object.prototype이 me 객체의 프로토타입 체인 상에 존재하므로 true로 평가된다.
    console.log(me instanceof Object); // true
    ```
    
    - instanceof 연산자는 **생성자 함수의 prototype에 바인딩된 객체가 프로토타입 체인 상에 존재하는지 확인한다.**
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fe11d14b-c812-41a9-8a68-1057d6ab931f/Untitled.png)
        
- 직접 상속
    - Object.create 에 의한 직접 상속
        - Object.create 메서드는 명시적으로 프로토타입을 지정하여 새로운 객체를 생성한다.
        ( Object.create 메서드도 다른 객체 생성 방식과 마찬가지로 추상 연산 OrdinaryObjectCreate 를 호출한다. )
        - Object.create 메서드의 
        첫 번째 매개변수에는 생성할 객체의 프로토타입으로 지정할 객체를 전달한다.
        두번째 매개변수에는 생성할 객체의 프로퍼티 키와 프로퍼티 디스크립터 객체로 이뤄진 객체를 전달한다. 
        ( 두 번째 형식은 Object.defineProperties 메서드의 두 번째 인수와 동일. 옵션이므로 생략 가능 )
            
            ```jsx
            // 프로토타입이 null인 객체를 생성한다. 생성된 객체는 프로토타입 체인의 종점에 위치한다.
            // obj → null
            let obj = Object.create(null);
            console.log(Object.getPrototypeOf(obj) === null); // true
            // Object.prototype을 상속받지 못한다.
            console.log(obj.toString()); // TypeError: obj.toString is not a function
            
            // obj → Object.prototype → null
            // obj = {};와 동일하다.
            obj = Object.create(Object.prototype);
            console.log(Object.getPrototypeOf(obj) === Object.prototype); // true
            
            // obj → Object.prototype → null
            // obj = { x: 1 };와 동일하다.
            obj = Object.create(Object.prototype, {
              x: { value: 1, writable: true, enumerable: true, configurable: true }
            });
            // 위 코드는 다음과 동일하다.
            // obj = Object.create(Object.prototype);
            // obj.x = 1;
            console.log(obj.x); // 1
            console.log(Object.getPrototypeOf(obj) === Object.prototype); // true
            
            const myProto = { x: 10 };
            // 임의의 객체를 직접 상속받는다.
            // obj → myProto → Object.prototype → null
            obj = Object.create(myProto);
            console.log(obj.x); // 10
            console.log(Object.getPrototypeOf(obj) === myProto); // true
            
            // 생성자 함수
            function Person(name) {
              this.name = name;
            }
            
            // obj → Person.prototype → Object.prototype → null
            // obj = new Person('Lee')와 동일하다.
            obj = Object.create(Person.prototype);
            obj.name = 'Lee';
            console.log(obj.name); // Lee
            console.log(Object.getPrototypeOf(obj) === Person.prototype); // true
            ```
            
            - Object.create 메서드는 첫 번째 매개변수에 전달한 객체의 프로토타입 체인에 속하는 객체를 생성한다.
            ( 즉, **객체를 생성하면서 직접적으로 상속을 구현하는 것이다.** )
            이 메서드의 장점은, 
            1. new 연산자가 없이도 객체를 생성할 수 있다.
            2. 프로토타입을 지정하면서 객체를 생성할 수 있다.
            3. 객체 리터럴에 의해 생성된 객체도 상속받을 수 있다.
    - 객체 리터럴 내부에서 __ proto __ 에 의한 직접 상속
        - ES6 에서는 객체 리터럴 내부에서 __ proto __ 접근자 프로퍼티를 사용하여 직접 상속을 구현할 수 있다.
            
            ```jsx
            const myProto = { x: 10 };
            
            // 객체 리터럴에 의해 객체를 생성하면서 프로토타입을 지정하여 직접 상속받을 수 있다.
            const obj = {
              y: 20,
              // 객체를 직접 상속받는다.
              // obj → myProto → Object.prototype → null
              __proto__: myProto
            };
            /* 위 코드는 아래와 동일하다.
            const obj = Object.create(myProto, {
              y: { value: 20, writable: true, enumerable: true, configurable: true }
            });
            */
            
            console.log(obj.x, obj.y); // 10 20
            console.log(Object.getPrototypeOf(obj) === myProto); // true
            ```
            
        
- 정적 프로퍼티 / 메서드
    - 정적 프로퍼티 / 메서드 는 생성자 함수로 인스턴스를 생성하지 않아도 참조 / 호출할 수 있는 프로퍼티 / 메서드 를 말한다.
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a019a1dc-f93b-4d2d-8018-238a83881ae8/Untitled.png)
        
    - 생성자 함수가 생성한 인스턴스는 자신의 프로토타입 체인에 속한 객체의 프로퍼티 / 메서드 에 접근할 수 있다.
    → 하지만 정적 프로퍼티 / 메서드는 인스턴스의 프로토타입 체인에 속한 객체의 프로퍼티 / 메서드 가 아니므로 인스턴스로 접근할 수 없다.
    
    ```jsx
    function Foo() {}
    
    // 프로토타입 메서드
    // this를 참조하지 않는 프로토타입 메소드는 정적 메서드로 변경해도 동일한 효과를 얻을 수 있다.
    Foo.prototype.x = function () {
      console.log('x');
    };
    
    const foo = new Foo();
    // 프로토타입 메서드를 호출하려면 인스턴스를 생성해야 한다.
    foo.x(); // x
    
    // 정적 메서드
    Foo.x = function () {
      console.log('x');
    };
    
    // 정적 메서드는 인스턴스를 생성하지 않아도 호출할 수 있다.
    Foo.x(); // x
    ```
    
    - 만약 인스턴스 / 프로토타입 메서드 내에서 this 를 사용하지 않는다면 그 메서드는 정적 메서드로 변경할 수 있다. 
    메서드 내에서 인스턴스를 참조할 필요가 없다면 정적 메서드로 변경하여도 동작한다.
    프로토타입 메서드를 호출하려면 인스턴스를 생성해야 하지만 정적 메서드는 인스턴스를 생성하지 않아도 호출할 수 있다.
- 프로퍼티 존재 확인
- 프로퍼티 열거