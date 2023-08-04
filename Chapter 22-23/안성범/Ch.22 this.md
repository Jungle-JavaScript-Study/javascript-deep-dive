### CH. 22 this

- this 키워드
    - this는 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 **자기 참조 변수**(self-referencing variable)다. 
    **this를 통해 자신이 속한 객체 또는 자신이 생성할 인스턴스의 프로퍼티나 메서드를 참조할 수 있다.**
    - **this 가 가리키는 값(즉, this 바운딩)은 함수 호출 방식에 의해 동적으로 결정된다.**
    - ex>
        
        ```jsx
        // 객체 리터럴
        const circle = {
          radius: 5,
          getDiameter() {
            // this는 메서드를 호출한 객체를 가리킨다.
            return 2 * this.radius;
          }
        };
        
        console.log(circle.getDiameter()); // 10
        
        // 생성자 함수
        function Circle(radius) {
          // this는 생성자 함수가 생성할 인스턴스를 가리킨다.
          this.radius = radius;
        }
        
        Circle.prototype.getDiameter = function () {
          // this는 생성자 함수가 생성할 인스턴스를 가리킨다.
          return 2 * this.radius;
        };
        
        // 인스턴스 생성
        const circle = new Circle(5);
        console.log(circle.getDiameter()); // 10
        
        // this는 어디서든지 참조 가능하다.
        // 전역에서 this는 전역 객체 window를 가리킨다.
        console.log(this); // window
        
        function square(number) {
          // 일반 함수 내부에서 this는 전역 객체 window를 가리킨다.
          console.log(this); // window
          return number * number;
        }
        square(2);
        
        const person = {
          name: 'Lee',
          getName() {
            // 메서드 내부에서 this는 메서드를 호출한 객체를 가리킨다.
            console.log(this); // {name: "Lee", getName: ƒ}
            return this.name;
          }
        };
        console.log(person.getName()); // Lee
        
        function Person(name) {
          this.name = name;
          // 생성자 함수 내부에서 this는 생성자 함수가 생성할 인스턴스를 가리킨다.
          console.log(this); // Person {name: "Lee"}
        }
        
        const me = new Person('Lee');
        ```
        
    - 하지만 this는 객체의 프로퍼티나 메서드를 참조하기 위한 자기 참조 변수이므로 일반적으로 객체의 메서드 내부 또는 생성자 함수 내부에서만 의미가 있다.
    따라서 strict mode가 적용된 일반 함수 내부의 this 에는 undefined가 바인딩된다.
    (일반 함수 내부에서 this 를 사용할 필요가 없기 때문이다.)
- 함수 호출 방식과 this 바인딩
    - **this 바인딩(this에 바인딩될 값)은 함수 호출 방식에 따라 동적으로 결정된다.**
    - 일반 함수 호출
        - **일반 함수로 호출된 모든 함수(중첩 함수, 콜백 함수 포함) 내부의 this 에는 전역 객체가 바인딩된다.**
        
        ```jsx
        function foo() {
          console.log("foo's this: ", this);  // window
          function bar() {
            console.log("bar's this: ", this); // window
          }
          bar();
        }
        foo();
        ```
        
    - 메서드 호출
        - 메서드 내부의 this에는 메서드를 호출한 객체(메서드를 호출할 때 메서드 이름 앞의 마침표 연산자 앞에 기술한 객체)가 바인딩된다. 
        주의할 것은 메서드 내부의 this 는 메서드를 소유한 객체가 아닌 메서드를 호출한 객체에 바인딩된다는 것이다.
            
            ```jsx
            const person = {
              name: 'Lee',
              getName() {
                // 메서드 내부의 this는 메서드를 호출한 객체에 바인딩된다.
                return this.name;
              }
            };
            
            // 메서드 getName을 호출한 객체는 person이다.
            console.log(person.getName()); // Lee
            ```
            
    - 생성자 함수 호출
        - 생성자 함수 내부의 this 에는 생성자 함수가 (미래에) 생성할 인스턴스가 바인딩된다.
            
            ```jsx
            // 생성자 함수
            function Circle(radius) {
              // 생성자 함수 내부의 this는 생성자 함수가 생성할 인스턴스를 가리킨다.
              this.radius = radius;
              this.getDiameter = function () {
                return 2 * this.radius;
              };
            }
            
            // 반지름이 5인 Circle 객체를 생성
            const circle1 = new Circle(5);
            // 반지름이 10인 Circle 객체를 생성
            const circle2 = new Circle(10);
            
            console.log(circle1.getDiameter()); // 10
            console.log(circle2.getDiameter()); // 20
            ```
            
            ```jsx
            // new 연산자와 함께 호출하지 않으면 생성자 함수로 동작하지 않는다. 즉, 일반적인 함수의 호출이다.
            const circle3 = Circle(15);
            
            // 일반 함수로 호출된 Circle에는 반환문이 없으므로 암묵적으로 undefined를 반환한다.
            console.log(circle3); // undefined
            
            // 일반 함수로 호출된 Circle 내부의 this는 전역 객체를 가리킨다.
            console.log(radius); // 15
            ```
            
    - Function.prototype.apply/call/bind 메서드에 의한 간접 호출
        - **Function.prototype.apply/call/bind 메서드에 첫 번째 인수로 전달한 객체에 this가 바인딩된다.**
        - apply, call, bind 메서드는 Function.prototype의 메서드다.
        즉, 이들 메서드는 모든 함수가 상속받아 사용할 수 있다.
            
            ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/83bd561b-3957-44d5-aa3b-570eb3aec616/Untitled.png)
            
        - **apply 와 call 메서드의 본질적인 기능은 함수를 호출하는 것이다.**
            
            ```jsx
            function getThisBinding() {
              console.log(arguments);
              return this;
            }
            
            // this로 사용할 객체
            const thisArg = { a: 1 };
            
            // getThisBinding 함수를 호출하면서 인수로 전달한 객체를 getThisBinding 함수의 this에 바인딩한다.
            // apply 메서드는 호출할 함수의 인수를 배열로 묶어 전달한다.
            console.log(getThisBinding.apply(thisArg, [1, 2, 3]));
            // Arguments(3) [1, 2, 3, callee: ƒ, Symbol(Symbol.iterator): ƒ]
            // {a: 1}
            
            // call 메서드는 호출할 함수의 인수를 쉼표로 구분한 리스트 형식으로 전달한다.
            console.log(getThisBinding.call(thisArg, 1, 2, 3));
            // Arguments(3) [1, 2, 3, callee: ƒ, Symbol(Symbol.iterator): ƒ]
            // {a: 1}
            ```
            
        - Function.prototype.bind 메서드는 apply 와 call 메서드와 달리 함수를 호출하지 않는다. 다만, 첫 번째 인수로 전달한 값으로 this 바인딩이 교체된 함수를 새롭게 생성해 반환한다.
            
            ```jsx
            function getThisBinding() {
              return this;
            }
            
            // this로 사용할 객체
            const thisArg = { a: 1 };
            
            // bind 메서드는 첫 번째 인수로 전달한 thisArg로 this 바인딩이 교체된
            // getThisBinding 함수를 새롭게 생성해 반환한다.
            console.log(getThisBinding.bind(thisArg)); // getThisBinding
            // bind 메서드는 함수를 호출하지는 않으므로 명시적으로 호출해야 한다.
            console.log(getThisBinding.bind(thisArg)()); // {a: 1}
            ```
            
        - bind 메서드는 메서드의 this 와 메서드 내부의 중첩 함수 또는 콜백 함수의 this 가 불일치하는 문제를 해결하기 위해 유용하게 사용된다.
        
        ```jsx
        const person = {
          name: 'Lee',
          foo(callback) {
            // ①
            setTimeout(callback, 100);
          }
        };
        
        person.foo(function () {
          console.log(`Hi! my name is ${this.name}.`); // ② Hi! my name is .
          // 일반 함수로 호출된 콜백 함수 내부의 this.name은 브라우저 환경에서 window.name과 같다.
          // 브라우저 환경에서 window.name은 브라우저 창의 이름을 나타내는 빌트인 프로퍼티이며 기본값은 ''이다.
          // Node.js 환경에서 this.name은 undefined다.
        });
        ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
        // 콜백 함수 내부의 this를 외부 함수 내부의 this와 일치시켜야 한다.
        const person = {
          name: 'Lee',
          foo(callback) {
            // bind 메서드로 callback 함수 내부의 this 바인딩을 전달
            setTimeout(callback.bind(this), 100);
          }
        };
        
        person.foo(function () {
          console.log(`Hi! my name is ${this.name}.`); // Hi! my name is Lee.
        });
        ```