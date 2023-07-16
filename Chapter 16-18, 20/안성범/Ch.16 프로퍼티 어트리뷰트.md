### CH. 16 프로퍼티 어트리뷰트

- 내부 슬롯과 내부 메서드
    - 프로퍼티 어트리뷰트를 이해하기 위해 내부 슬롯(internal slot)과 내부 메서드(internal method)개념을 알아야한다.
        - 내부 슬롯과 내부 메서드는 자바스크립트 엔진의 구현 알고리즘을 설명하기 위해 ECMAScript 사양에서 사용하는 의사 프로퍼티(pseudo property)와 의사 메서드(pseudo method)이다.
        ECMAScript 사양에 등장하는 이중 대괄호([[ … ]])로 감싼 이름들이다.
    - 내부 슬롯과 내부 메서드는 자바스크립트 엔진의 내부 로직이므로 원칙적으로 자바스크립트는 내부 슬롯과 내부 메서드에 직접적으로 접근하거나 호출할 수 있는 방법을 제공하지 않는다. - 단, 일부 내부 슬롯과 내부 메서드에 한하여 간접적으로 접근할 수 있는 수단을 제공하기는 한다.
        - ex> 모든 객체는 [[Prototype]] 이라는 내부 슬롯을 갖는다.
        [[Prototype]] 내부 슬롯의 경우, _ _proto_ _를 통해 간접적으로 접근할 수 있다.
- 프로퍼티 어트리뷰트와 프로퍼티 디스크립터 객체
    - **자바스크립트 엔진은 프로퍼티를 생성할 때 프로퍼티의 상태를 나타내는 프로퍼티 어트리뷰트를 기본값으로 자동 정의한다.**
    - Object.getOwnPropertyDescriptor 메서드를 호출할 때 첫 번째 매개변수에는 객체의 참조를 전달하고, 두 번째 매개변수에는 프로퍼티 키를 문자열로 전달한다.
    이때 Object.getOwnPropertyDescriptor 메서드는 ******************************************************************************************************프로퍼티 디스크립터(PropertyDescriptor)객체******************************************************************************************************를 반환한다.
    ( 만약 존재하지 않는 프로퍼티나 상속받은 프로퍼티에 대한 프로퍼티 디스크립터를 요구하면 undefined가 반환된다. )
    - Object.getOwnPropertyDescriptors 메서드는 모든 프로퍼티의 프로퍼티 어트리뷰트 정보를 제공하는 프로퍼티 디스크립터 객체들을 반환한다.
        
        ```jsx
        const person = {
          name: 'Lee',
        };
        
        console.log(Object.getOwnPropertyDescriptor(person, 'name'));
        // {value: "Lee", writable: true, enumerable: true, configurable: true}
        
        person.age = 20;
        
        console.log(Object.getOwnPropertyDescriptors(person));
        
        /*
        {
          name : {value: "Lee", writable: true, enumerable: true, configurable; true},
        age : {value: 20, writable: true, enumerable: true, configurable; true},
        }
        */
        ```
        
- 데이터 프로퍼티와 접근자 프로퍼티
    - 데이터 프로퍼티 (data property)
        - 키와 값으로 구성된 일반적인 프로퍼티
            
            ![이 프로퍼티 어트리뷰트는 자바스크립트 엔진이 프로퍼티를 생성할 때 기본값으로 자동 정의된다.](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f069a68d-efea-421a-acee-d3c21f0b9aa1/Untitled.png)
            
            이 프로퍼티 어트리뷰트는 자바스크립트 엔진이 프로퍼티를 생성할 때 기본값으로 자동 정의된다.
            
        - 프로퍼티가 생성될 때 [[Value]] 의 값은 프로퍼티 값으로 초기화되며 [[Writable]], [[Enumerable]], [[Configurable]] 의 값은 true 로 초기화된다.
    - 접근자 프로퍼티 (accessor property)
        - 자체적으로는 값을 갖지 않고 다른 데이터 프로퍼티의 값을 읽거나 저장할 때 호출되는 접근자 함수(accessor function)로 구성된 프로퍼티
            
            ![접근자 프로퍼티가 갖는 프로퍼티 어트리뷰트](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/56bf1819-fb55-4e46-92bc-aed3a69e2077/Untitled.png)
            
            접근자 프로퍼티가 갖는 프로퍼티 어트리뷰트
            
        - 접근자 함수는 getter/setter 함수라고도 부른다.
            
            ```jsx
            const person={
            // 데이터 프로퍼티
            	firstName: "Ungmo",
            	lastName: "Lee",
            
            	// fullName은 접근자 함수로 구성된 접근자 프로퍼티다 .
            	// getter함수
            	get fullName(){
            		return `${this.firstName} ${this.lastName}`;
            	},
            	//setter 함수
            	set fullName(name){
            	//배열 디스트럭처링 할당
            	[this.firstName, this.lastName] = name.split(' ')
            	}
            };
            
            //데이터 프로퍼티를 통한 프로퍼티 값의 참조
            console.log(person.firstName + ' ' + person.lastName); // Ungmo Lee
            
            //접근자 프로퍼티를 통한 프로퍼티 값의 저장
            //접근자 프로퍼티 fullName에 값을 저장하면 setter함수가 호출된다
            person.fullName = 'Heegun Lee';
            console.log(person) //{firstName: 'Heegun', lastName: 'Lee'}
            
            //접근자 프로퍼티를 통한 프로퍼티 값의 참조
            //접근자 프로퍼티 fullName에 접근하면 getter함수가 호출된다
            console.log(person.fullName); // Heegun Lee
            
            //firstName은 데이터 프로퍼티다
            //데이터 프로퍼티는 [[Value]], [[Writable]], [[Enumerable]],[[Configurable]] 프로퍼티 어트리뷰트를 갖는다
            let descriptor = Object.getOwnPropertyDescriptor(person, 'firstName');
            console.log(descriptor);
            // {value: "Heegun", writable: true, enumerable: true, configurable: true}
            
            //fullName 은 접근자 프로퍼티다.
            // 접근자 프로퍼티는 [[Get]], [[Set]], [[Enumerable]], [[Configurable]] 프로퍼티 어트리뷰트를 갖는다.
            descriptor = Object.getOwnPropertyDescriptors(person, 'fullName');
            console.log(descriptor);
            // {get: f, set: f, enumerable: true, configurable: true}
            ```
            
        - 프로토타입은 어떤 객체의 상위(부모) 객체의 역할을 하는 객체이다.
        프로토타입은 하위(자식) 객체에서 자신의 프로퍼티와 메서드를 상속한다.
- 프로퍼티 정의
    - 프로퍼티 정의란 **새로운 프로퍼티를 추가하면서 프로퍼티 어트리뷰트를 명시적으로 정의**하거나, **기존 프로퍼티의 프로퍼티 어트리뷰트를 재정의**하는 것을 말한다.
    → 이를 통해 객체의 프로퍼티가 어떻게 동작해야 하는지를 명확히 정의할 수 있다.
        
        ```jsx
        const person = {};
        
        // 데이터 프로퍼티 정의
        Object.defineProperty(person, 'firstName', {
          value: 'Ungmo',
          writable: true,
          enumerable: true,
          configurable: true
        });
        
        Object.defineProperty(person, 'lastName', {
          value: 'Lee'
        });
        
        let descriptor = Object.getOwnPropertyDescriptor(person, 'firstName');
        console.log('firstName', descriptor);
        // firstName {value: "Ungmo", writable: true, enumerable: true, configurable: true}
        
        // 디스크립터 객체의 프로퍼티를 누락시키면 undefined, false가 기본값이다.
        descriptor = Object.getOwnPropertyDescriptor(person, 'lastName');
        console.log('lastName', descriptor);
        // lastName {value: "Lee", writable: false, enumerable: false, configurable: false}
        
        // [[Enumerable]]의 값이 false인 경우
        // 해당 프로퍼티는 for...in 문이나 Object.keys 등으로 열거할 수 없다.
        // lastName 프로퍼티는 [[Enumerable]]의 값이 false이므로 열거되지 않는다.
        console.log(Object.keys(person)); // ["firstName"]
        
        // [[Writable]]의 값이 false인 경우 해당 프로퍼티의 [[Value]]의 값을 변경할 수 없다.
        // lastName 프로퍼티는 [[Writable]]의 값이 false이므로 값을 변경할 수 없다.
        // 이때 값을 변경하면 에러는 발생하지 않고 무시된다.
        person.lastName = 'Kim';
        
        // [[Configurable]]의 값이 false인 경우 해당 프로퍼티를 삭제할 수 없다.
        // lastName 프로퍼티는 [[Configurable]]의 값이 false이므로 삭제할 수 없다.
        // 이때 프로퍼티를 삭제하면 에러는 발생하지 않고 무시된다.
        delete person.lastName;
        
        // [[Configurable]]의 값이 false인 경우 해당 프로퍼티를 재정의할 수 없다.
        // Object.defineProperty(person, 'lastName', { enumerable: true });
        // Uncaught TypeError: Cannot redefine property: lastName
        
        descriptor = Object.getOwnPropertyDescriptor(person, 'lastName');
        console.log('lastName', descriptor);
        // lastName {value: "Lee", writable: false, enumerable: false, configurable: false}
        
        // 접근자 프로퍼티 정의
        Object.defineProperty(person, 'fullName', {
          // getter 함수
          get() {
            return `${this.firstName} ${this.lastName}`;
          },
          // setter 함수
          set(name) {
            [this.firstName, this.lastName] = name.split(' ');
          },
          enumerable: true,
          configurable: true
        });
        
        descriptor = Object.getOwnPropertyDescriptor(person, 'fullName');
        console.log('fullName', descriptor);
        // fullName {get: ƒ, set: ƒ, enumerable: true, configurable: true}
        
        person.fullName = 'Heegun Lee';
        console.log(person); // {firstName: "Heegun", lastName: "Lee"}
        ```
        
        ![Object.defineProperty 메서드로 프로퍼티를 정의할 때, 생략된 어트리뷰트의 기본값](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bdbdf951-65de-4e7b-a1a4-40a1a97d7208/Untitled.png)
        
        Object.defineProperty 메서드로 프로퍼티를 정의할 때, 생략된 어트리뷰트의 기본값
        
        - Object.defineProperty 메서드는 한번에 하나의 프로퍼티만 정의할 수 있다.
        Object.defineProperties 메서드를 사용하면 여러 개의 프로퍼티를 한 번에 정의할 수 있다.
- 객체 변경 방지
    - 객체는 변경 가능한 값이므로 재할당 없이 직접 변경할 수 있다. 
    자바스크립트는 객체의 변경을 방지하는 다양한 메서드를 제공한다.
    객체 변경 방지 메서드들은 객체의 변경을 금지하는 강도가 다르다.
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/44327594-d1fe-4848-a5a7-41693a1d2506/Untitled.png)
        
    - 객체 확장 금지
        - Object.preventExtensions 메서드는 객체의 확장을 금지한다.
        ****************************************************************************************************************************확장이 금지된 객체는 프로퍼티 추가가 금지된다.****************************************************************************************************************************
            
            ```jsx
            const person = { name: 'Lee' };
            
            // person 객체는 확장이 금지된 객체가 아니다.
            console.log(Object.isExtensible(person)); // true
            
            // person 객체의 확장을 금지하여 프로퍼티 추가를 금지한다.
            Object.preventExtensions(person);
            
            // person 객체는 확장이 금지된 객체다.
            console.log(Object.isExtensible(person)); // false
            
            // 프로퍼티 추가가 금지된다.
            person.age = 20; // 무시. strict mode에서는 에러
            console.log(person); // {name: "Lee"}
            
            // 프로퍼티 추가는 금지되지만 삭제는 가능하다.
            delete person.name;
            console.log(person); // {}
            
            // 프로퍼티 정의에 의한 프로퍼티 추가도 금지된다.
            Object.defineProperty(person, 'age', { value: 20 });
            // TypeError: Cannot define property age, object is not extensible
            ```
            
    - 객체 밀봉
        - Object.seal 메서드는 객체를 밀봉한다
        ******************************************************************************************************밀봉된 객체는 읽기와 쓰기만 가능하다.******************************************************************************************************
            
            ```jsx
            const person = { name: 'Lee' };
            
            // person 객체는 밀봉(seal)된 객체가 아니다.
            console.log(Object.isSealed(person)); // false
            
            // person 객체를 밀봉(seal)하여 프로퍼티 추가, 삭제, 재정의를 금지한다.
            Object.seal(person);
            
            // person 객체는 밀봉(seal)된 객체다.
            console.log(Object.isSealed(person)); // true
            
            // 밀봉(seal)된 객체는 configurable이 false다.
            console.log(Object.getOwnPropertyDescriptors(person));
            /*
            {
              name: {value: "Lee", writable: true, enumerable: true, configurable: false},
            }
            */
            
            // 프로퍼티 추가가 금지된다.
            person.age = 20; // 무시. strict mode에서는 에러
            console.log(person); // {name: "Lee"}
            
            // 프로퍼티 삭제가 금지된다.
            delete person.name; // 무시. strict mode에서는 에러
            console.log(person); // {name: "Lee"}
            
            // 프로퍼티 값 갱신은 가능하다.
            person.name = 'Kim';
            console.log(person); // {name: "Kim"}
            
            // 프로퍼티 어트리뷰트 재정의가 금지된다.
            Object.defineProperty(person, 'name', { configurable: true });
            // TypeError: Cannot redefine property: name
            ```
            
    - 객체 동결
        - Object.freeze 메서드는 객체를 동결한다.
        ******************************************************************************************동결된 객체는 읽기만 가능하다.******************************************************************************************
            
            ```jsx
            const person = { name: 'Lee' };
            
            // person 객체는 동결(freeze)된 객체가 아니다.
            console.log(Object.isFrozen(person)); // false
            
            // person 객체를 동결(freeze)하여 프로퍼티 추가, 삭제, 재정의, 쓰기를 금지한다.
            Object.freeze(person);
            
            // person 객체는 동결(freeze)된 객체다.
            console.log(Object.isFrozen(person)); // true
            
            // 동결(freeze)된 객체는 writable과 configurable이 false다.
            console.log(Object.getOwnPropertyDescriptors(person));
            /*
            {
              name: {value: "Lee", writable: false, enumerable: true, configurable: false},
            }
            */
            
            // 프로퍼티 추가가 금지된다.
            person.age = 20; // 무시. strict mode에서는 에러
            console.log(person); // {name: "Lee"}
            
            // 프로퍼티 삭제가 금지된다.
            delete person.name; // 무시. strict mode에서는 에러
            console.log(person); // {name: "Lee"}
            
            // 프로퍼티 값 갱신이 금지된다.
            person.name = 'Kim'; // 무시. strict mode에서는 에러
            console.log(person); // {name: "Lee"}
            
            // 프로퍼티 어트리뷰트 재정의가 금지된다.
            Object.defineProperty(person, 'name', { configurable: true });
            // TypeError: Cannot redefine property: name
            ```
            
    - 불변 객체
        - 변경 방지 메서드들은 얕은 변경 방지(shallow only)로 직속 프로퍼티만 변경이 방지되고 중첩 객체까지는 영향을 주지 못한다.
        따라서, Object.freeze 메서드로 객체를 동결하여도 중첩 객체까지 동결할 수 없다.
        - 객체의 중첩 객체까지 변경이 불가능한 읽기 전용의 불변 객체를 구현하려면 객체를 값으로 갖는 모든 프로퍼티에 대해 재귀적으로 Object.freeze 메서드를 호출해야 한다.
            
            ```jsx
            function deepFreeze(target) {
              // 객체가 아니거나 동결된 객체는 무시하고 객체이고 동결되지 않은 객체만 동결한다.
              if (target && typeof target === 'object' && !Object.isFrozen(target)) {
                Object.freeze(target);
                /*
                  모든 프로퍼티를 순회하며 재귀적으로 동결한다.
                  Object.keys 메서드는 객체 자신의 열거 가능한 프로퍼티 키를 배열로 반환한다.
                  ("19.15.2. Object.keys/values/entries 메서드" 참고)
                  forEach 메서드는 배열을 순회하며 배열의 각 요소에 대하여 콜백 함수를 실행한다.
                  ("27.9.2. Array.prototype.forEach" 참고)
                */
                Object.keys(target).forEach(key => deepFreeze(target[key]));
              }
              return target;
            }
            
            const person = {
              name: 'Lee',
              address: { city: 'Seoul' }
            };
            
            // 깊은 객체 동결
            deepFreeze(person);
            
            console.log(Object.isFrozen(person)); // true
            // 중첩 객체까지 동결한다.
            console.log(Object.isFrozen(person.address)); // true
            
            person.address.city = 'Busan';
            console.log(person); // {name: "Lee", address: {city: "Seoul"}}
            ```