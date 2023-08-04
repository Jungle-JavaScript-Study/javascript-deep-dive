### CH. 25 클래스

- 클래스와 생성자 함수
    - 생성자 함수와 클래스는 프로토타입 기반의 객체지향을 구현했다는 점에서 매우 유사하다.
    하지만, 클래스는 생성자 함수 기반의 객체 생성 방식보다 견고하고 명료하다.
    (특히 클래스의 extends 와 super 키워드는 상속 관계 구현을 더욱 간결하고 명료하게 한다. )
    - 클래스와 생성자 함수의 차이점
        1. 클래스를 new 연산자 없이 호출하면 에러가 발생한다. 
        생성자 함수는 new 연산자 없이 호출하면 일반 함수로서 호출된다.
        2. 클래스는 상속을 지원하는 extends와 super 키워드를 제공한다.
        생성자 함수는 extends와 super 키워드를 지원하지 않는다.
        3. 클래스는 호이스팅이 발생하지 않는 것처럼 동작한다.
        함수 선언문으로 정의된 생성자 함수는 함수 호이스팅이, 
        함수 표현식으로 정의한 생성자 함수는 변수 호이스팅이 발생한다.
        4. 클래스 내의 모든 코드에는 암묵적으로 strict mode 가 지정되어 실행되며 strict mode 를 해제할 수 없다.
        생성자함수는 암묵적으로 strict mode 가 지정되지 않는다.
        5. 클래스의 constructor. 프로토타입 메서드, 정적 메서드는 모두 프로퍼티 어트리뷰트 [[ Enumerable ]]의 값이 false 다. ( 열거 되지 않는다. )
- 클래스 정의
    - **클래스는 함수다.**
        
        ```jsx
        // 익명 클래스 표현식
        const Person = class {};
        
        // 기명 클래스 표현식
        const Person = class MyClass {};
        ```
        
    - 클래스 몸체에는 0개 이상의 메서드만 정의할 수 있다.
    (constructor(생성자), 프로토타입 메서드, 정적 메서드)
        
        ```jsx
        // 클래스 선언문
        class Person {
          // 생성자
          constructor(name) {
            // 인스턴스 생성 및 초기화
            this.name = name; // name 프로퍼티는 public하다.
          }
        
          // 프로토타입 메서드
          sayHi() {
            console.log(`Hi! My name is ${this.name}`);
          }
        
          // 정적 메서드
          static sayHello() {
            console.log('Hello!');
          }
        }
        
        // 인스턴스 생성
        const me = new Person('Lee');
        
        // 인스턴스의 프로퍼티 참조
        console.log(me.name); // Lee
        // 프로토타입 메서드 호출
        me.sayHi(); // Hi! My name is Lee
        // 정적 메서드 호출
        Person.sayHello(); // Hello!
        ```
        
    
- 클래스 호이스팅
    - 클래스는 함수로 평가된다.
    - 단, 클래스는 let, const 키워드로 선언한 변수처럼 호이스팅된다.
    (클래스 선언문 이전에 일시적 사각지대(Temporal Dead Zone, TDZ)에 빠지기 때문에 호이스팅이 발생하지 않는 것처럼 동작한다.)
- 인스턴스 생성
    - 클래스는 생성자 함수이며, new 연산자와 함께 호출되어 인스턴스를 생성한다.
    (클래스는 인스턴스를 생성하는 것이 유일한 존재 이유이므로 **반드시 new 연산자와 함께 호출**해야 한다.)
        
        ```jsx
        class Person {}
        
        // 인스턴스 생성
        const me = new Person();
        console.log(me); // Person {}
        ```
        
- 메서드
    - constructor
        - constructor 는 인스턴스를 생성하고 초기화하기 위한 특수한 메서드이다.
        - constructor 내부의 this 는 생성자 함수와 마찬가지로 클래스가 생성한 인스턴스를 가리킨다.
        - constructor 는 클래스 내의 최대 한 개만 존재할 수 있다.
        ( 만약 2개 이상의 constructor를 포함하면 문법에러 가 발생한다.)
        - constructor 는 생략할 수 있다. 생략하면, 클래스에 다음과 같이 빈 constructor가 암묵적으로 정의된다. ( 빈 constructor 에 의해 빈 객체를 생성한다. )
        
        ```jsx
        class Person {
          constructor(name, address) {
            // 인수로 인스턴스 초기화
            this.name = name;
            this.address = address;
          }
        }
        
        // 인수로 초기값을 전달한다. 초기값은 constructor에 전달된다.
        const me = new Person('Lee', 'Seoul');
        console.log(me); // Person {name: "Lee", address: "Seoul"}
        ```
        
        - 프로퍼티가 추가되어 초기화된 인스턴스를 생성하려면 constructor 내부에서 this에 인스턴스 프로퍼티를 추가한다.
        - **constructor 내부에서 return 문을 반드시 생략해야 한다.**
        ( constructor 내부에서 명시적으로 this 가 아닌 다른 값을 반환하는 것은 클래스의 기본 동작을 훼손하기 때문 )
    - 프로토타입 메서드
        - 클래스 몸체에서 정의한 메서드는 생성자 함수에 의한 객체 생성 방식과는 다르게 클래스의 prototype 프로퍼티에 메서드를 추가하지 않아도 기본적으로 프로토타입 메서드가 된다.
            
            ```jsx
            class Person {
              // 생성자
              constructor(name) {
                // 인스턴스 생성 및 초기화
                this.name = name;
              }
            
              // 프로토타입 메서드
              sayHi() {
                console.log(`Hi! My name is ${this.name}`);
              }
            }
            
            const me = new Person('Lee');
            me.sayHi(); // Hi! My name is Lee
            ```
            
            생성자 함수와 마찬가지로 클래스가 생성한 인스턴스는 프로토타입 체인의 일원이 된다.
            
    - 정적(static) 메서드
        - 정적 메서드는 인스턴스를 생성하지 않아도 호출할 수 있는 메서드를 말한다.
        - 클래스에서는 메서드에 static 키워드를 붙이면 정적 메서드(클래스 메서드)가 된다.
        
        ```jsx
        // 생성자 함수
        function Person(name) {
          this.name = name;
        }
        
        // 정적 메서드
        Person.sayHi = function () {
          console.log('Hi!');
        };
        
        // 정적 메서드 호출
        Person.sayHi(); // Hi!
        
        class Person {
          // 생성자
          constructor(name) {
            // 인스턴스 생성 및 초기화
            this.name = name;
          }
        
          // 정적 메서드
          static sayHi() {
            console.log('Hi!');
          }
        }
        ```
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8ce7ae8d-4dd0-4e54-9b38-c6a9a1e615b5/Untitled.png)
        
        - 정적 메서드는 인스턴스로 호출할 수 없다. 인스턴스의 프로토타입 체인 상에는 클래스가 존재하지 않기 때문에 인스턴스로 클래스의 메서드를 상속받을 수 없다.
        
        ```jsx
        // 정적 메서드는 클래스로 호출한다.
        // 정적 메서드는 인스턴스 없이도 호출할 수 있다.
        Person.sayHi(); // Hi!
        
        // 인스턴스 생성
        // 인스턴스로는 호출 할 수 없다.
        const me = new Person('Lee');
        me.sayHi(); // TypeError: me.sayHi is not a function
        ```
        
    - 정적 메서드와 프로토타입 메서드의 차이
        1. 정적 메서드와 프로토타입 메서드는 자신이 속해 있는 프로토타입 체인이 다르다.
        2. 정적 메서드는 클래스로 호출하고 프로토타입 메서드는 인스턴스로 호출한다.
        3. 정적 메서드는 인스턴스 프로퍼티를 참조할 수 없지만, 프로토타입 메서드는 인스턴스 프로퍼티를 참조할 수 있다.
        - this 를 사용하지 않는 메서드는 정적 메서드로 정의하는 것이 좋다.
        - 클래스 또는 생성자 함수를 하나의 네임스페이스로 사용하여 정적 메서드를 모아 놓으면 이름 충돌 가능성을 줄여 주고 관련 함수들을 구조화할 수 있는 효과가 있다.
        → 정적 메서드는 애플리케이션 전역에서 사용할 유틸리티 함수를 전역 함수로 정의하지 않고 메서드로 구조화 할 때 유용하다.
    - 클래스에서 정의한 메서드의 특징
        1. function 키워드를 생략한 메서드 축약 표현을 사용한다.
        2. 객체 리터럴과는 다르게 클래스에 메서드를 정의할 때는 콤마가 필요 없다.
        3. 암묵적으로 strict mode로 실행된다.
        4. for … in 문이나 Object.keys 메서드 등으로 열거할 수 없다.
        ([[ Enumerable ]] 의 값이 false 이다.)
        5. 내부 메서드 [[Construct]]를 갖지 않는 non-constructor다. 
        따라서 new 연산자와 함께 호출할 수 없다.
- 클래스의 인스턴스 생성 과정
    - new 연산자와 함께 클래스를 호출하면 생성자 함수와 마찬가지로 클래스의 내부 메서드 [[Constructor]]가 호출된다. **********************************************************************************************************클래스는 new 연산자 없이 호출할 수 없다.**********************************************************************************************************
    1. 인스턴스 생성과 this 바인딩
        - constructor 내부의 this 는 클래스가 생성한 인스턴스를 가리킨다.
    2. 인스턴스 초기화
        - constructor의 내부 코드가 실행되어 this에 바인딩되어 있는 인스턴스를 초기화한다.
    3. 인스턴스 반환
        - 클래스의 모든 처리가 끝나면 완성된 인스턴스가 바인딩된 this가 암묵적으로 반환된다.
        
        ```jsx
        class Person {
          // 생성자
          constructor(name) {
            // 1. 암묵적으로 인스턴스가 생성되고 this에 바인딩된다.
            console.log(this); // Person {}
            console.log(Object.getPrototypeOf(this) === Person.prototype); // true
        
            // 2. this에 바인딩되어 있는 인스턴스를 초기화한다.
            this.name = name;
        
            // 3. 완성된 인스턴스가 바인딩된 this가 암묵적으로 반환된다.
          }
        }
        ```
        
- 프로퍼티
    - 인스턴스 프로퍼티
        - 인스턴스 프로퍼티는 constructor 내부에서 정의해야 한다.
    - 접근자 프로퍼티
        - 접근자 프로퍼티는 자체적으로는 값[[Value]]을 갖지 않고 다른 데이터 프로퍼티의 값을 읽거나 저장할 때 사용하는 접근자 함수로 구성된 프로퍼티이다.
            
            ```jsx
            const person = {
              // 데이터 프로퍼티
              firstName: 'Ungmo',
              lastName: 'Lee',
            
              // fullName은 접근자 함수로 구성된 접근자 프로퍼티다.
              // getter 함수
              get fullName() {
                return `${this.firstName} ${this.lastName}`;
              },
              // setter 함수
              set fullName(name) {
                // 배열 디스트럭처링 할당: "36.1. 배열 디스트럭처링 할당" 참고
                [this.firstName, this.lastName] = name.split(' ');
              }
            };
            
            // 데이터 프로퍼티를 통한 프로퍼티 값의 참조.
            console.log(`${person.firstName} ${person.lastName}`); // Ungmo Lee
            
            // 접근자 프로퍼티를 통한 프로퍼티 값의 저장
            // 접근자 프로퍼티 fullName에 값을 저장하면 setter 함수가 호출된다.
            person.fullName = 'Heegun Lee';
            console.log(person); // {firstName: "Heegun", lastName: "Lee"}
            
            // 접근자 프로퍼티를 통한 프로퍼티 값의 참조
            // 접근자 프로퍼티 fullName에 접근하면 getter 함수가 호출된다.
            console.log(person.fullName); // Heegun Lee
            
            // fullName은 접근자 프로퍼티다.
            // 접근자 프로퍼티는 get, set, enumerable, configurable 프로퍼티 어트리뷰트를 갖는다.
            console.log(Object.getOwnPropertyDescriptor(person, 'fullName'));
            // {get: ƒ, set: ƒ, enumerable: true, configurable: true}
            ```
            
            - 클래스의 메서드는 기본적으로 프로토타입 메서드가 된다. 
            따라서 클래스의 접근자 프로퍼티 또한 인스턴스 프로퍼티가 아닌 프로토타입의 프로퍼티가 된다.
            
            ```jsx
            // Object.getOwnPropertyNames는 비열거형(non-enumerable)을 포함한 모든 프로퍼티의 이름을 반환한다.(상속 제외)
            Object.getOwnPropertyNames(me); // -> ["firstName", "lastName"]
            Object.getOwnPropertyNames(Object.getPrototypeOf(me)); // -> ["constructor", "fullName"]
            ```
            
            ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a2ed2677-de4d-4515-902d-e3767f78bff6/Untitled.png)
            
        
    - 클래스 필드 정의 제안
        - **클래스필드(필드 또는 멤버)는 클래스 기반 객체지향 언어에서 클래스가 생성할 인스턴스의 프로퍼티를 가리키는 용어**이다.
        - 자바스크립트의 클래스 몸체에는 메서드만 선언할 수 있다.
        따라서 클래스 몸체에 자바와 유사하게 클래스 필드를 선언하면 문법 에러가 발생한다.
        → 하지만, 최신 브라우저 또는 최신 Node.js(ver12이상)에서 실행하면 문법 에러가 발생하지 않고 정상 작동한다.
        
        ```jsx
        class Person {
          // 클래스 필드 정의
          name = 'Lee';
        }
        
        const me = new Person();
        console.log(me); // Person {name: "Lee"}
        ```
        
        - 클래스 몸체에서 클래스 필드를 정의하는 경우 this 에 클래스 필드를 바인딩해서는 안된다.
        **this 는 클래스의 constructor와 메서드 내에서만 유효하다.**
        - 클래스 필드 정의 제안으로 인해 인스턴스 프로퍼티를 정의하는 방식은 두 가지가 되었다.
            1. 인스턴스를 생성할 때 외부 초기값으로 클래스 필드를 초기화할 필요가 있다면 constructor에서 인스턴스 프로퍼티를 정의하는 기존 방식을 사용하고
            2. 인스턴스를 생성할 때 외부 초기값으로 클래스 필드를 초기화할 필요가 없다면 기존의 constructor에서 인스턴스 프로퍼티를 정의하는 방식과 클래스 필드 정의 제안 모두 사용할 수 있다.
        - 
    - private 필드 정의 제안
        - private 필드의 선두에는 #을 붙여준다.
        private 필드를 참조할 때도 #을 붙여주어야 한다.
            
            ```jsx
            class Person {
              // private 필드 정의
              #name = '';
            
              constructor(name) {
                // private 필드 참조
                this.#name = name;
              }
            }
            
            const me = new Person('Lee');
            
            // private 필드 #name은 클래스 외부에서 참조할 수 없다.
            console.log(me.#name);
            // SyntaxError: Private field '#name' must be declared in an enclosing class
            ```
            
            - public 필드는 어디서든 참조할 수 있지만 private 필드는 클래스 내부에서만 참조할 수 있다.
            - 클래스 외부에서 private 필드에 직접 접근할 수 있는 방법은 없다.
            다만, 접근자 프로퍼티를 통해 간접적으로 접근하는 방법은 유효하다.
                
                ```jsx
                class Person {
                  // private 필드 정의
                  #name = '';
                
                  constructor(name) {
                    this.#name = name;
                  }
                
                  // name은 접근자 프로퍼티다.
                  get name() {
                    // private 필드를 참조하여 trim한 다음 반환한다.
                    return this.#name.trim();
                  }
                }
                
                const me = new Person(' Lee ');
                console.log(me.name); // Lee
                ```
                
            - private 필드는 반드시 클래스 몸체에 정의해야 한다. 
            private 필드를 직접 constructor에 정의하면 에러가 발생한다.
    - static 필드 정의 제안
        - 최신 브라우저와 최신 Node.js(ver12이상)에 static public 필드, static private 필드, static private 메서드를 정의할 수 있는 “Static class features”가 구현되어 있다.
        
        ```jsx
        class MyMath {
          // static public 필드 정의
          static PI = 22 / 7;
        
          // static private 필드 정의
          static #num = 10;
        
          // static 메서드
          static increment() {
            return ++MyMath.#num;
          }
        }
        
        console.log(MyMath.PI); // 3.142857142857143
        console.log(MyMath.increment()); // 11
        ```
        
- 상속에 의한 클래스 확장
    - 클래스 상속과 생성자 함수 상속
        - 프로토타입 기반 상속은 프로토타입 체인을 통해 다른 객체의 자산을 상속받는 개념이지만 **상속에 의한 클래스 확장은 기존 클래스를 상속받아 새로운 클래스를 확장(extends)하여 정의**하는 것이다.
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/dc657b14-7fba-40b4-9a69-7e547d37cb4a/Untitled.png)
        
        - 예제
            
            ```jsx
            class Animal {
              constructor(age, weight) {
                this.age = age;
                this.weight = weight;
              }
            
              eat() { return 'eat'; }
            
              move() { return 'move'; }
            }
            
            // 상속을 통해 Animal 클래스를 확장한 Bird 클래스
            class Bird extends Animal {
              fly() { return 'fly'; }
            }
            
            const bird = new Bird(1, 5);
            
            console.log(bird); // Bird {age: 1, weight: 5}
            console.log(bird instanceof Bird); // true
            console.log(bird instanceof Animal); // true
            
            console.log(bird.eat());  // eat
            console.log(bird.move()); // move
            console.log(bird.fly());  // fly
            ```
            
            ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/56766e0f-5f7f-4eeb-92d5-2d984b799542/Untitled.png)
            
    - extends 키워드
        - 상속을 통해 클래스를 확장하려면 extends 키워드를 사용하여 상속받을 클래스를 정의한다.
            
            ```jsx
            // 수퍼(베이스/부모)클래스
            class Base {}
            
            // 서브(파생/자식)클래스
            class Derived extends Base {}
            ```
            
        - 상속을 통해 확장된 클래스를 서브클래스(subclass) 
        (파생 클래스(derived class) 자식 클래스(child class))
        서브클래스에게 상속된 클래스를 수퍼클래스(super-class)
        (베이스 클래스(base class) 부모 클래스(parent class))
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b73462de-4acd-4295-ba16-17a72d1b65b6/Untitled.png)
        
    - 동적 상속
        - extends 키워드는 클래스뿐만 아니라 생성자 함수를 상속받아 클래스를 확장할 수도 있다.
        단, extends 키워드 앞에는 반드시 클래스가 와야 한다.
        - extends 키워드 다음에는 클래스뿐만 아니라 [[Constructor]] 내부 메서드를 갖는 함수 객체로 평가될 수 있는 모든 표현식을 사용할 수 있다.
        → 이를 통해 동적으로 상속받을 대상을 결정할 수 있다.
        
        ```jsx
        // 생성자 함수
        function Base(a) {
          this.a = a;
        }
        
        // 생성자 함수를 상속받는 서브클래스
        class Derived extends Base {}
        
        const derived = new Derived(1);
        console.log(derived); // Derived {a: 1}
        
        function Base1() {}
        
        class Base2 {}
        
        let condition = true;
        
        // 조건에 따라 동적으로 상속 대상을 결정하는 서브클래스
        class Derived extends (condition ? Base1 : Base2) {}
        
        const derived = new Derived();
        console.log(derived); // Derived {}
        
        console.log(derived instanceof Base1); // true
        console.log(derived instanceof Base2); // false
        ```
        
    - 서브클래스의 constructor
        - 수퍼클래스와 서브클래스 모두 constructor를 생략하면, constructor 가 암묵적으로 정의된다.
        
        ```jsx
        // 수퍼클래스
        class Base {
          constructor() {}
        }
        
        // 서브클래스
        class Derived extends Base {
          constructor() { super(); }
        }
        
        const derived = new Derived();
        console.log(derived); // Derived {}
        ```
        
- super 키워드
    - super 키워드는 함수처럼 호출할 수도 있고 this와 같이 식별자처럼 참조할 수 있는 특수한 키워드다.
        - super를 호출하면 수퍼클래스의 constructor(super-constructor)를 호출한다.
        - super를 참조하면 수퍼클래스의 메서드를 호출할 수 있다.
    - super 호출
        - super를 호출하면 수퍼클래스의 constructor(super-constructor)를 호출한다.
            
            ```jsx
            // 수퍼클래스
            class Base {
              constructor(a, b) { // ④
                this.a = a;
                this.b = b;
              }
            }
            
            // 서브클래스
            class Derived extends Base {
              constructor(a, b, c) { // ②
                super(a, b); // ③
                this.c = c;
              }
            }
            
            const derived = new Derived(1, 2, 3); // ①
            console.log(derived); // Derived {a: 1, b: 2, c: 3}
            ```
            
        - super를 호출할 때 주의사항
            1. 서브클래스에서 constructor를 생략하지 않는 경우 서브클래스의 constructor에서는 반드시 super를 호출해야 한다.
                
                ```jsx
                class Base {}
                
                class Derived extends Base {
                  constructor() {
                    // ReferenceError: Must call super constructor in derived class before accessing 'this' or returning from derived constructor
                    console.log('constructor call');
                  }
                }
                
                const derived = new Derived();
                ```
                
            2. 서브클래스의 constructor에서 super를 호출하기 전에는 this 를 참조할 수 없다.
                
                ```jsx
                class Base {}
                
                class Derived extends Base {
                  constructor() {
                    // ReferenceError: Must call super constructor in derived class before accessing 'this' or returning from derived constructor
                    this.a = 1;
                    super();
                  }
                }
                
                const derived = new Derived(1);
                ```
                
            3. super는 반드시 서브클래스의 constructor에서만 호출한다.
            서브클래스가 아닌 클래스의 constructor나 함수에서 super를 호출하면 에러가 발생한다.
                
                ```jsx
                class Base {
                  constructor() {
                    super(); // SyntaxError: 'super' keyword unexpected here
                  }
                }
                
                function Foo() {
                  super(); // SyntaxError: 'super' keyword unexpected here
                }
                ```
                
        
    - super 참조
        - **메서드 내에서 super를 참조하면 수퍼클래스의 메서드를 호출할 수 있다.**
        1.  서브클래스의 프로토타입 메서드 내에서 super.sayHi는 수퍼클래스의 프로토타입 메서드 sayHi를 가리킨다.
            
            ```jsx
            // 수퍼클래스
            class Base {
              constructor(name) {
                this.name = name;
              }
            
              sayHi() {
                return `Hi! ${this.name}`;
              }
            }
            
            // 서브클래스
            class Derived extends Base {
              sayHi() {
                // super.sayHi는 수퍼클래스의 프로토타입 메서드를 가리킨다.
                return `${super.sayHi()}. how are you doing?`;
              }
            }
            
            const derived = new Derived('Lee');
            console.log(derived.sayHi()); // Hi! Lee. how are you doing?
            ```
            
            - super 참조를 의사 코드로 표현하면 다음과 같다.
                
                ```jsx
                /*
                [[HomeObject]]는 메서드 자신을 바인딩하고 있는 객체를 가리킨다.
                [[HomeObject]]를 통해 메서드 자신을 바인딩하고 있는 객체의 프로토타입을 찾을 수 있다.
                예를 들어, Derived 클래스의 sayHi 메서드는 Derived.prototype에 바인딩되어 있다.
                따라서 Derived 클래스의 sayHi 메서드의 [[HomeObject]]는 Derived.prototype이고
                이를 통해 Derived 클래스의 sayHi 메서드 내부의 super 참조가 Base.prototype으로 결정된다.
                따라서 super.sayHi는 Base.prototype.sayHi를 가리키게 된다.
                */
                super = Object.getPrototypeOf([[HomeObject]])
                ```
                
                - **주의할 것은 ES6의 메서드 축약 표현으로 정의된 함수만이 [[HomeObject]]를 갖는다는 것이다.**
        2. 서브클래스의 정적 메서드 내에서 super.sayHi는 수퍼클래스의 정적 메서드 sayHi를 가리킨다.
            
            ```jsx
            // 수퍼클래스
            class Base {
              static sayHi() {
                return 'Hi!';
              }
            }
            
            // 서브클래스
            class Derived extends Base {
              static sayHi() {
                // super.sayHi는 수퍼클래스의 정적 메서드를 가리킨다.
                return `${super.sayHi()} how are you doing?`;
              }
            }
            
            console.log(Derived.sayHi()); // Hi! how are you doing?
            ```
            
- 상속 클래스의 인스턴스 생성 과정
    - 예제
        
        ```jsx
        // 수퍼클래스
        class Rectangle {
          constructor(width, height) {
            this.width = width;
            this.height = height;
          }
        
          getArea() {
            return this.width * this.height;
          }
        
          toString() {
            return `width = ${this.width}, height = ${this.height}`;
          }
        }
        
        // 서브클래스
        class ColorRectangle extends Rectangle {
          constructor(width, height, color) {
            super(width, height);
            this.color = color;
          }
        
          // 메서드 오버라이딩
          toString() {
            return super.toString() + `, color = ${this.color}`;
          }
        }
        
        const colorRectangle = new ColorRectangle(2, 4, 'red');
        console.log(colorRectangle); // ColorRectangle {width: 2, height: 4, color: "red"}
        
        // 상속을 통해 getArea 메서드를 호출
        console.log(colorRectangle.getArea()); // 8
        // 오버라이딩된 toString 메서드를 호출
        console.log(colorRectangle.toString()); // width = 2, height = 4, color = red
        ```
        
        ![CorolRectangle 클래스에 의해 생성된 인스턴스의 프로토타입 체인](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2c28f924-4e0d-4ee3-b4d3-e0330949ef84/Untitled.png)
        
        CorolRectangle 클래스에 의해 생성된 인스턴스의 프로토타입 체인
        
    1. 서브클래스의 super 호출
        - 자바스크립트 엔진은 클래스를 평가할 때 수퍼클래스와 서브클래스를 구분하기 위해 “base” 또는 “derived”를 값으로 갖는 내부 슬롯 [[ConstructorKind]]를 갖는다.
        - **************************************************************서브클래스는 자신이 직접 인스턴스를 생성하지 않고 수퍼클래스에게 인스턴스 생성을 위임한다.
        → 서브클래스의 constructor 에서 반드시 super를 호출해야 하는 이유**************************************************************
        - 서브클래스 constructor 내부에 super 호출이 없으면 에러가 발생한다.
        ( 실제로 인스턴스를 생성하는 주체는 수퍼클래스이므로 수퍼클래스의 constructor를 호출하는 super가 호출되지 않으면 인스턴스를 생성할 수 없기 때문이다. )
    2. 수퍼클래스의 인스턴스 생성과 this 바인딩
        
        ```jsx
        // 수퍼클래스
        class Rectangle {
          constructor(width, height) {
            // 암묵적으로 빈 객체, 즉 인스턴스가 생성되고 this에 바인딩된다.
            console.log(this); // ColorRectangle {}
            // new 연산자와 함께 호출된 함수, 즉 new.target은 ColorRectangle이다.
            console.log(new.target); // ColorRectangle
        
            // 생성된 인스턴스의 프로토타입으로 ColorRectangle.prototype이 설정된다.
            console.log(Object.getPrototypeOf(this) === ColorRectangle.prototype); // true
            console.log(this instanceof ColorRectangle); // true
            console.log(this instanceof Rectangle); // true
        ...
        ```
        
        - 인스턴스는 수퍼클래스가 생성한 것이다. 하지만 new 연산자와 함께 호출된 서브클래스라는 것이 중요하다.
        **인스턴스는 new.target 이 가리키는 서브클래스가 생성한 것으로 처리된다.**
        - 즉, 생성된 인스턴스의 프로토타입은 new.target, 즉, 서브클래스의 prototype 프로퍼티가 가리키는 객체(ColorRectangle.prototype)이다.
    3. 수퍼클래스의 인스턴스 초기화
        - 수퍼클래스의 constructor가 실행되어 this 에 바인딩되어 있는 인스턴스를 초기화한다.
    4. 서브클래스 constructor 로의 복귀와 this 바인딩
        - super의 호출이 종료되고 제어 흐름이 서브클래스 constructor로 돌아온다.
        **이때 super가 반환한 인스턴스가 this에 바인딩된다.
        서브클래스는 별도의 인스턴스를 생성하지 않고 super가 반환한 인스턴스를 this에 바인딩하여 그대로 사용한다.
        → super가 호출되지 않으면 인스턴스가 생성되지 않으며, this 바인딩도 할 수 없다.
        → 서브클래스의 constructor에서 super를 호출하기 전에는 this를 참조할 수 없는 이유가 바로 이 때문이다.**
    5. 서브클래스의 인스턴스 초기화
        - super 호출 이후, 서브클래스의 constructor에 기술되어 있는 인스턴스 초기화가 실행된다.
    6. 인스턴스 반환
        - 클래스의 모든 처리가 끝나면 완성된 인스턴스가 바인딩된 this가 암묵적으로 반환된다.
            
            ```jsx
            // 서브클래스
            class ColorRectangle extends Rectangle {
              constructor(width, height, color) {
                super(width, height);
            
                // super가 반환한 인스턴스가 this에 바인딩된다.
                console.log(this); // ColorRectangle {width: 2, height: 4}
            
                // 인스턴스 초기화
                this.color = color;
            
                // 완성된 인스턴스가 바인딩된 this가 암묵적으로 반환된다.
                console.log(this); // ColorRectangle {width: 2, height: 4, color: "red"}
              }
            ...
            ```
            
- 표준 빌트인 생성자 함수 확장
    - extends 키워드 다음에는 클래스뿐만이 아니라 [[Construct]] 내부 메서드를 갖는 함수 객체로 평가될 수 있는 모든 표현식을 사용할 수 있다.
    → String, Number, Array 같은 표준 빌트인 객체도 [[Construct]] 내부 메서드를 갖는 생성자 함수이므로 extends 키워드를 사용하여 확장할 수 있다.