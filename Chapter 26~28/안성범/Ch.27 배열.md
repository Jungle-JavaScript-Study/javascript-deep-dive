### CH. 27 배열

- 배열
    - 배열은 여러 개의 값을 순차적으로 나열한 자료구조이다.
    - 배열이 가지고 있는 값을 **요소(element)**라고 부른다.
    - 자바스크립트의 모든 값은 배열의 요소가 될 수 있다.
    - 배열의 요소는 배열에서 자신의 위치를 나타내는 0 이상의 정수인 **인덱스(index)**를 갖는다.
    - 요소에 접근할 때에는 대괄호 표기법을 사용한다
        
        ```jsx
        arr[0] // -> 'apple'
        arr[1] // -> 'banana'
        arr[2] // -> 'orange'
        ```
        
    - 배열은 요소의 개수, 즉 배열의 길이를 나타내는 **length 프로퍼티**를 갖는다.
    - 자바스크립트에 배열이라는 타입은 존재하지 않는다. 배열은 객체 타입이다.
    - 배열은 객체지만 일반 객체와는 구별되는 독특한 특징이 있다.
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2a8603d8-99b2-4711-baff-3f739c27ab5c/Untitled.png)
        
    - 배열의 장점은 처음부터 순차적으로 요소에 접근할 수도 있고, 마지막부터 역순으로 요소에 접근할 수도 있으며, 특정 위치부터 순차적으로 요소에 접근할 수도 있다는 것이다.
    ( 이는 배열이 인덱스, 즉 값의 순서와 length 프로퍼티를 갖기 때문에 가능한 것이다. )
- 자바스크립트 배열은 배열이 아니다
    - **자료구조**에서 말하는 배열은 동일한 크기의 메모리 공간이 빈틈없이 연속적으로 나열된 자료구조를 말한다.
    ( 즉, 배열의 요소는 하나의 데이터 타입으로 통일되어 있으며 서로 연속적으로 인접해 있다. 이러한 배열을 **밀집 배열(dense array)**이라고 한다. )
    - 자바스크립트에서의 배열은 일반적인 의미의 배열과 다르다. 
    즉, 배열의 요소를 위한 각각의 메모리 공간은 동일한 크기를 갖지 않아도 되며, 연속적으로 이어져 있지 않을 수도 있다.
    ( 배열의 요소가 연속적으로 이어져 있지 않은 배열을 **희소 배열(sparse array)**이라고 한다. )
    - 일반적인 배열과 자바스크립트 배열의 장단점
        - 일반적인 배열은 인덱스로 요소에 빠르게 접근할 수 있다. 
        하지만, 요소를 삽입 또는 삭제하는 경우에는 효율적이지 않다.
        - 자바스크립트 배열은 해시 테이블로 구현된 객체이므로 인덱스로 요소에 접근하는 경우 일반적인 배열보다 성능적인 면에서 느릴수밖에 없는 구조적인 단점이 있다.
        하지만, 요소를 삽입 또는 삭제하는 경우에는 일반적인 배열보다 빠른 성능을 기대할 수 있다.
- length 프로퍼티와 희소 배열
    - length 프로퍼티는 요소의 개수, 즉 배열의 길이를 나타내는 0 이상의 정수를 값으로 갖는다.
    - length 프로퍼티의 값은 빈 배열일 경우 0이며, 빈 배열이 아닐 경우 가장 큰 인덱스에 1을 더한 것과 같다.
    - length 프로퍼티의 값은 0과 2^32-1(4,294,967,296 -1) 미만의 양의 정수다.
    따라서 배열에서 사용할 수 있는 가장 작은 인덱스는 0이며, 가장 큰 인덱스는 2^32 -2(4,294,967,294)다.
    - length 프로퍼티의 값은 배열에 요소를 추가하거나 삭제하면 자동 갱신된다.
    - length 프로퍼티의 값은 배열의 길이를 바탕으로 결정되지만 임의의 숫자 값을 명시적으로 할당할 수도 있다.
        
        ```jsx
        const arr = [1, 2, 3, 4, 5];
        
        // 현재 length 프로퍼티 값인 5보다 작은 숫자 값 3을 length 프로퍼티에 할당
        arr.length = 3;
        
        // 배열의 길이가 5에서 3으로 줄어든다.
        console.log(arr); // [1, 2, 3]
        
        const arr2 = [1];
        
        // 현재 length 프로퍼티 값인 1보다 큰 숫자 값 3을 length 프로퍼티에 할당
        arr2.length = 3;
        
        // length 프로퍼티 값은 변경되지만 실제로 배열의 길이가 늘어나지는 않는다.
        // 값 없이 비어 있는 요소를 위해 메모리 공간을 확보하지 않으며 빈 요소를 생성하지도 않는다.
        console.log(arr2.length); // 3
        console.log(arr2); // [1, empty × 2]
        ```
        
    - 배열의 요소가 연속적으로 위치하지 않고 일부가 비어 있는 배열을 희소 배열이라고 한다. 
    자바스크립트는 희소 배열을 문법적으로 허용한다.
    희소 배열의 length는 희소 배열의 실제 요소 개수보다 언제나 크다.
    하지만, 배열을 생성할 경우에 희소 배열을 생성하지 않도록 주의해야 한다.
    **( 배열에는 같은 타입의 요소를 연속적으로 위치시키는 것이 최선이다. )**
        
        ```jsx
        // 희소 배열
        const sparse = [, 2, , 4];
        
        // 희소 배열의 length 프로퍼티 값은 요소의 개수와 일치하지 않는다.
        console.log(sparse.length); // 4
        console.log(sparse); // [empty, 2, empty, 4]
        
        // 배열 sparse에는 인덱스가 0, 2인 요소가 존재하지 않는다.
        console.log(Object.getOwnPropertyDescriptors(sparse));
        /*
        {
          '1': { value: 2, writable: true, enumerable: true, configurable: true },
          '3': { value: 4, writable: true, enumerable: true, configurable: true },
          length: { value: 4, writable: true, enumerable: false, configurable: false }
        }
        */
        ```
        
- 배열 생성
    - 배열 리터럴
        - 배열 리터럴은 0개 이상의 요소를 쉼표로 구분하여 대괄호([])로 묶는다.
        배열 리터럴은 객체 리터럴과 달리 프로퍼티 키가 없고 값만 존재한다.
        
        ```jsx
        const arr = [1, 2, 3];
        console.log(arr.length); // 3
        
        // 배열 리터럴에 요소를 하나도 추가하지 않으면 length 프로퍼티 값이 0인 빈 배열이 된다.
        const arr = [];
        console.log(arr.length); // 0
        
        ㅂ// 배열 리터럴에 요소를 생략하면 희소 배열이 생성된다.
        const arr = [1, , 3]; // 희소 배열
        
        // 희소 배열의 length는 배열의 실제 요소 개수보다 언제나 크다.
        console.log(arr.length); // 3
        console.log(arr);        // [1, empty, 3]
        console.log(arr[1]);     // undefined
        ```
        
    - Array 생성자 함수
        - Object 생성자 함수를 통해 객체를 생성할 수 있듯이 Array 생성자 함수를 통해 배열을 생성할 수도 있다.
        - 전달된 인수가 1개이고 숫자인 경우 length 프로퍼티 값이 인수인 희소 배열을 생성한다.
        length 프로퍼티 값이 0은 아니지만, 실제로 배열의 요소는 존재하지 않는다.
            
            ```jsx
            const arr = new Array(10);
            
            console.log(arr); // [empty × 10]
            console.log(arr.length); // 10
            ```
            
        - 전달된 인수가 없는 경우 빈 배열을 생성한다. ( 배열 리터럴 [ ]과 같다. )
            
            ```jsx
            new Array(); // -> []
            ```
            
        - 전달된 인수가 2개 이상이거나 숫자가 아닌 경우 인수를 요소로 갖는 배열을 생성한다.
            
            ```jsx
            // 전달된 인수가 2개 이상이면 인수를 요소로 갖는 배열을 생성한다.
            new Array(1, 2, 3); // -> [1, 2, 3]
            
            // 전달된 인수가 1개지만 숫자가 아니면 인수를 요소로 갖는 배열을 생성한다.
            new Array({}); // -> [{}]
            ```
            
        - Array 생성자 함수는 new 연산자와 함께 호출하지 않더라도(일반 함수로서 호출해도) 배열을 생성하는 생성자 함수로 동작한다.
        ( Array 생성자 함수 내부에서 new.target 을 확인하기 때문이다. )
            
            ```jsx
            Array(1, 2, 3); // -> [1, 2, 3]
            ```
            
    - Array.of
        - ES6에서 도입된 Array.of 메서드는 전달된 인수를 요소로 갖는 배열을 생성한다.
        ( Array.of는 Array 생성자 함수와 다르게 전달된 인수가 1개이고 숫자이더라도 인수를 요소로 갖는 배열을 생성한다. )
            
            ```jsx
            // 전달된 인수가 1개이고 숫자이더라도 인수를 요소로 갖는 배열을 생성한다.
            Array.of(1); // -> [1]
            
            Array.of(1, 2, 3); // -> [1, 2, 3]
            
            Array.of('string'); // -> ['string']
            ```
            
    - Array.from
        - ES6에서 도입된 Array.from 메서드는 유사 배열 객체 또는 이터러블 객체를 인수로 전달받아 배열로 변환하여 반환한다.
            
            ```jsx
            // 유사 배열 객체를 변환하여 배열을 생성한다.
            Array.from({ length: 2, 0: 'a', 1: 'b' }); // -> ['a', 'b']
            
            // 이터러블을 변환하여 배열을 생성한다. 문자열은 이터러블이다.
            Array.from('Hello'); // -> ['H', 'e', 'l', 'l', 'o']
            
            // Array.from에 length만 존재하는 유사 배열 객체를 전달하면 undefined를 요소로 채운다.
            Array.from({ length: 3 }); // -> [undefined, undefined, undefined]
            
            // Array.from은 두 번째 인수로 전달한 콜백 함수의 반환값으로 구성된 배열을 반환한다.
            Array.from({ length: 3 }, (_, i) => i); // -> [0, 1, 2]
            ```
            
            Array.from을 사용하면 두 번째 인수로 전달한 콜백 함수를 통해 값을 만들면서 요소를 채울 수 있다.
            Array.from 메서드는 두 번째 인수로 전달한 콜백 함수에 첫 번째 인수에 의해 생성된 배열의 요소값과 인덱스를 순차적으로 전달하면서 호출하고, 콜백 함수의 반환값으로 구성된 배열을 반환한다.
            
- 배열 요소의 참조
    - 배열의 요소를 참조할 때에는 대괄호 ([ ]) 표기법을 사용한다.
    대괄호 안에는 인덱스가 와야 한다.
    정수로 평가되는 표현식이라면 인덱스 대신 사용할 수 있다.
    ( 인덱스는 값을 참조할 수 있다는 의미에서 객체의 프로퍼티 키와 같은 역할을 한다.)
        
        ```jsx
        const arr = [1, 2];
        
        // 인덱스가 0인 요소를 참조
        console.log(arr[0]); // 1
        // 인덱스가 1인 요소를 참조
        console.log(arr[1]); // 2
        
        const arr = [1, 2];
        
        // 인덱스가 2인 요소를 참조. 배열 arr에는 인덱스가 2인 요소가 존재하지 않는다.
        console.log(arr[2]); // undefined
        ```
        
- 배열 요소의 추가와 갱신
    - 배열에 요소를 동적으로 추가할 수 있다.
    존재하지 않는 인덱스를 사용해 값을 할당하면 새로운 요소가 추가된다.
    ( 이때 length 프로퍼티 값은 자동 갱신된다. )
    - 이미 요소가 존재하는 요소에 값을 재할당하면 요소값이 갱신된다.
    - 인덱스는 요소의 위치를 나타내므로 반드시 0 이상의 정수(또는 정수 형태의 문자열)를 사용해야 한다.
    만약, 정수 이외의 값을 인덱스처럼 사용하면 요소가 생성되는 것이 아니라 프로퍼티가 생성된다.
    ( 이때 생성된 프로퍼티는 length 프로퍼티 값에 영향을 주지 않는다. )
        
        ```jsx
        const arr = [];
        
        // 배열 요소의 추가
        arr[0] = 1;
        arr['1'] = 2;
        
        // 프로퍼티 추가
        arr['foo'] = 3;
        arr.bar = 4;
        arr[1.1] = 5;
        arr[-1] = 6;
        
        console.log(arr); // [1, 2, foo: 3, bar: 4, '1.1': 5, '-1': 6]
        
        // 프로퍼티는 length에 영향을 주지 않는다.
        console.log(arr.length); // 2
        ```
        
- 배열 요소의 삭제
    - 배열은 사실 객체이기 때문에 배열의 특정 요소를 삭제하기 위해 delete 연산자를 사용할 수 있다.
    하지만, delete 연산자를 사용하면 배열은 희소 배열이 되며 length 프로퍼티 값은 변하지 않는다.
    → 희소 배열을 만드는 delete 연산자는 사용하지 않는 것이 좋다.
    - 희소 배열을 만들지 않으면서 배열의 특정 요소를 완전히 삭제하려면 Array.prototype.splice 메서드를 사용한다.
        
        ```jsx
        const arr = [1, 2, 3];
        
        // 배열 요소의 삭제
        delete arr[1];
        console.log(arr); // [1, empty, 3]
        
        // length 프로퍼티에 영향을 주지 않는다. 즉, 희소 배열이 된다.
        console.log(arr.length); // 3
        
        const arr = [1, 2, 3];
        
        // Array.prototype.splice(삭제를 시작할 인덱스, 삭제할 요소 수)
        // arr[1]부터 1개의 요소를 제거
        arr.splice(1, 1);
        console.log(arr); // [1, 3]
        
        // length 프로퍼티가 자동 갱신된다.
        console.log(arr.length); // 2
        ```
        
- 배열 메서드
    - 배열 메서드는 결과물을 반환하는 패턴이 두 가지이다.
        1. **원본 배열(배열 메서드를 호출한 배열. 즉, 배열 메서드의 구현체 내부에서 this가 가리키는 객체)를 직접 변경하는 메서드(mutator method)**
        2. **원본 배열을 직접 변경하지 않고 새로운 배열을 생성하며 반환하는 메서드(accessor method)**
        - 원본 배열을 직접 변경하는 메서드는 외부 상태를 직접 변경하는 부수 효과가 있으므로 사용할 때 주의해야 한다. 
        → 가급적 원본 배열을 직접 변경하지 않는 메서드를 사용하는 편이 좋다.
    - Array.isArray
        - 전달된 인수가 배열이면 true, 배열이 아니면 false를 반환한다.
            
            ```jsx
            // true
            Array.isArray([]);
            Array.isArray([1, 2]);
            Array.isArray(new Array());
            
            // false
            Array.isArray();
            Array.isArray({});
            Array.isArray(null);
            Array.isArray(undefined);
            Array.isArray(1);
            Array.isArray('Array');
            Array.isArray(true);
            Array.isArray(false);
            Array.isArray({ 0: 1, length: 1 })
            ```
            
    - Array.prototype.indexOf
        - indexOf 메서드는 원본 배열에서 인수로 전달된 요소를 검색하여 인덱스를 반환한다.
            - 원본 배열에 인수로 전달한 요소와 중복되는 요소가 여러 개 있다면 첫 번째로 검색된 요소의 인덱스를 반환한다.
            - **원본 배열에 인수로 전달된 요소가 존재하지 않으면 -1 을 반환한다.**
        - indexOf 메서드 대신 ES7에서 도입된 Array.prototype.includes 메서드를 사용하면 가독성이 더 좋다.
            
            ```jsx
            const foods = ['apple', 'banana', 'orange'];
            
            // foods 배열에 'orange' 요소가 존재하는지 확인한다.
            if (foods.indexOf('orange') === -1) {
              // foods 배열에 'orange' 요소가 존재하지 않으면 'orange' 요소를 추가한다.
              foods.push('orange');
            }
            
            console.log(foods); // ["apple", "banana", "orange"]
            
            const foods = ['apple', 'banana'];
            
            // foods 배열에 'orange' 요소가 존재하는지 확인한다.
            if (!foods.includes('orange')) {
              // foods 배열에 'orange' 요소가 존재하지 않으면 'orange' 요소를 추가한다.
              foods.push('orange');
            }
            
            console.log(foods); // ["apple", "banana", "orange"]
            ```
            
    - Array.prototype.push ( mutator method )
        - 인수로 전달받은 모든 값을 원본 배열의 마지막 요소로 추가하고 변경된 length 프로퍼티 값을 반환한다.
        ( push 메서드는 원본 배열을 직접 변경한다. )
        - 마지막 요소로 추가할 요소가 하나뿐이라면 push 메서드를 사용하지 않고 length 프로퍼티를 사용하여 배열의 마지막에 요소를 직접 추가할 수도 있다.
        ( 이 방법이 push 메서드보다 빠르다. )
        - push 메서드는 원본 배열을 직접 변경하는 부수 효과가 있어서, push 메서드보다는 ES6의 스프레드 문법을 사용하는 편이 좋다.
        ( 스프레드 문법을 사용하면 함수 호출 없이 표현식으로 마지막에 요소를 추가할 수 있으며 부수 효과도 없다. )
        
        ```jsx
        const arr = [1, 2];
        
        // 인수로 전달받은 모든 값을 원본 배열 arr의 마지막 요소로 추가하고 변경된 length 값을 반환한다.
        let result = arr.push(3, 4);
        console.log(result); // 4
        
        // push 메서드는 원본 배열을 직접 변경한다.
        console.log(arr); // [1, 2, 3, 4]
        
        const arr = [1, 2];
        
        // arr.push(3)과 동일한 처리를 한다. 이 방법이 push 메서드보다 빠르다.
        arr[arr.length] = 3;
        console.log(arr); // [1, 2, 3]
        
        const arr = [1, 2];
        
        // ES6 스프레드 문법
        const newArr = [...arr, 3];
        console.log(newArr); // [1, 2, 3]
        ```
        
    - Array.prototype.pop ( mutator method )
        - 원본 배열에서 마지막 요소를 제거하고 제거한 요소를 반환한다.
        - 원본 배열이 빈 배열이면 undefined를 반환한다.
        pop 메서드는 원본 배열을 직접 변경한다.
        - Array.prototype.push 와 pop 을 이용한 스택 구현
            - 생성자 함수로 구현
                
                ```jsx
                const Stack = (function () {
                  function Stack(array = []) {
                    if (!Array.isArray(array)) {
                      // "47. 에러 처리" 참고
                      throw new TypeError(`${array} is not an array.`);
                    }
                    this.array = array;
                  }
                
                  Stack.prototype = {
                    // "19.10.1. 생성자 함수에 의한 프로토타입의 교체" 참고
                    constructor: Stack,
                    // 스택의 가장 마지막에 데이터를 밀어 넣는다.
                    push(value) {
                      return this.array.push(value);
                    },
                    // 스택의 가장 마지막 데이터, 즉 가장 나중에 밀어 넣은 최신 데이터를 꺼낸다.
                    pop() {
                      return this.array.pop();
                    },
                    // 스택의 복사본 배열을 반환한다.
                    entries() {
                      return [...this.array];
                    }
                  };
                
                  return Stack;
                }());
                
                const stack = new Stack([1, 2]);
                console.log(stack.entries()); // [1, 2]
                
                stack.push(3);
                console.log(stack.entries()); // [1, 2, 3]
                
                stack.pop();
                console.log(stack.entries()); // [1, 2]
                ```
                
            - 클래스로 구현
                
                ```jsx
                class Stack {
                  #array; // private class member
                
                  constructor(array = []) {
                    if (!Array.isArray(array)) {
                      throw new TypeError(`${array} is not an array.`);
                    }
                    this.#array = array;
                  }
                
                  // 스택의 가장 마지막에 데이터를 밀어 넣는다.
                  push(value) {
                    return this.#array.push(value);
                  }
                
                  // 스택의 가장 마지막 데이터, 즉 가장 나중에 밀어 넣은 최신 데이터를 꺼낸다.
                  pop() {
                    return this.#array.pop();
                  }
                
                  // 스택의 복사본 배열을 반환한다.
                  entries() {
                    return [...this.#array];
                  }
                }
                
                const stack = new Stack([1, 2]);
                console.log(stack.entries()); // [1, 2]
                
                stack.push(3);
                console.log(stack.entries()); // [1, 2, 3]
                
                stack.pop();
                console.log(stack.entries()); // [1, 2]
                ```
                
    - Array.prototype.unshift ( mutator method )
        - 인수로 전달받은 모든 값을 원본 배열의 선두에 요소로 추가하고 변경된 length 프로퍼티 값을 반환한다.
        unshift 메서드는 원본 배열을 직접 변경한다.
        - unshift 메서드는 원본 배열을 직접 변경하는 부수 효과가 있어, ES6의 스프레드 문법을 사용하는 편이 좋다.
            
            ```jsx
            const arr = [1, 2];
            
            // 인수로 전달받은 모든 값을 원본 배열의 선두에 요소로 추가하고 변경된 length 값을 반환한다.
            let result = arr.unshift(3, 4);
            console.log(result); // 4
            
            // unshift 메서드는 원본 배열을 직접 변경한다.
            console.log(arr); // [3, 4, 1, 2]
            
            const arr = [1, 2];
            
            // ES6 스프레드 문법
            const newArr = [3, ...arr];
            console.log(newArr); // [3, 1, 2]
            ```
            
    - Array.prototype.shift ( mutator method )
        - 원본 배열에서 첫 번째 요소를 제거하고 제거한 요소를 반환한다.
        원본 배열이 빈 배열이면 undefined를 반환한다.
        shift 메서드는 원본 배열을 직접 변경한다.
            
            ```jsx
            const arr = [1, 2];
            
            // 원본 배열에서 첫 번째 요소를 제거하고 제거한 요소를 반환한다.
            let result = arr.shift();
            console.log(result); // 1
            
            // shift 메서드는 원본 배열을 직접 변경한다.
            console.log(arr); // [2]
            ```
            
        - Array.prototype.shift 와 push 메서드를 이용한 큐 구현
            - 생성자 함수로 구현
                
                ```jsx
                const Queue = (function () {
                  function Queue(array = []) {
                    if (!Array.isArray(array)) {
                      // "47. 에러 처리" 참고
                      throw new TypeError(`${array} is not an array.`);
                    }
                    this.array = array;
                  }
                
                  Queue.prototype = {
                    // "19.10.1. 생성자 함수에 의한 프로토타입의 교체" 참고
                    constructor: Queue,
                    // 큐의 가장 마지막에 데이터를 밀어 넣는다.
                    enqueue(value) {
                      return this.array.push(value);
                    },
                    // 큐의 가장 처음 데이터, 즉 가장 먼저 밀어 넣은 데이터를 꺼낸다.
                    dequeue() {
                      return this.array.shift();
                    },
                    // 큐의 복사본 배열을 반환한다.
                    entries() {
                      return [...this.array];
                    }
                  };
                
                  return Queue;
                }());
                
                const queue = new Queue([1, 2]);
                console.log(queue.entries()); // [1, 2]
                
                queue.enqueue(3);
                console.log(queue.entries()); // [1, 2, 3]
                
                queue.dequeue();
                console.log(queue.entries()); // [2, 3]
                ```
                
            - 클래스로 구현
                
                ```jsx
                class Queue {
                  #array; // private class member
                
                  constructor(array = []) {
                    if (!Array.isArray(array)) {
                      throw new TypeError(`${array} is not an array.`);
                    }
                    this.#array = array;
                  }
                
                  // 큐의 가장 마지막에 데이터를 밀어 넣는다.
                  enqueue(value) {
                    return this.#array.push(value);
                  }
                
                  // 큐의 가장 처음 데이터, 즉 가장 먼저 밀어 넣은 데이터를 꺼낸다.
                  dequeue() {
                    return this.#array.shift();
                  }
                
                  // 큐의 복사본 배열을 반환한다.
                  entries() {
                    return [...this.#array];
                  }
                }
                
                const queue = new Queue([1, 2]);
                console.log(queue.entries()); // [1, 2]
                
                queue.enqueue(3);
                console.log(queue.entries()); // [1, 2, 3]
                
                queue.dequeue();
                console.log(queue.entries()); // [2, 3]
                ```
                
    - Array.prototype.concat ( accessor method )
        - 인수로 전달된 값들(배열 또는 원시값)을 원본 배열의 마지막 요소로 추가한 새로운 배열을 반환한다.
        - 인수로 전달한 값이 배열인 경우 배열을 해체하여 새로운 배열의 요소로 추가한다.
        원본 배열은 변경되지 않는다.
        - push 와 unshift 메서드는 concat 메서드로 대체할 수 있다.
        ( concat 메서드를 사용할 경우 반환값을 반드시 변수에 할당받아야 한다. )
        - concat 메서드는 ES6의 스프레드 문법으로 대체할 수 있다.
        → push / unshift 메서드와 concat 메서드를 사용하는 대신 ES6 의 스프레드 문법을 일관성 있게 사용하는 것을 권장한다.
            
            ```jsx
            const arr1 = [1, 2];
            const arr2 = [3, 4];
            
            // 배열 arr2를 원본 배열 arr1의 마지막 요소로 추가한 새로운 배열을 반환한다.
            // 인수로 전달한 값이 배열인 경우 배열을 해체하여 새로운 배열의 요소로 추가한다.
            let result = arr1.concat(arr2);
            console.log(result); // [1, 2, 3, 4]
            
            // 숫자를 원본 배열 arr1의 마지막 요소로 추가한 새로운 배열을 반환한다.
            result = arr1.concat(3);
            console.log(result); // [1, 2, 3]
            
            // 배열 arr2와 숫자를 원본 배열 arr1의 마지막 요소로 추가한 새로운 배열을 반환한다.
            result = arr1.concat(arr2, 5);
            console.log(result); // [1, 2, 3, 4, 5]
            
            // 원본 배열은 변경되지 않는다.
            console.log(arr1); // [1, 2]
            
            let result = [1, 2].concat([3, 4]);
            console.log(result); // [1, 2, 3, 4]
            
            // concat 메서드는 ES6의 스프레드 문법으로 대체할 수 있다.
            result = [...[1, 2], ...[3, 4]];
            console.log(result); // [1, 2, 3, 4]
            ```
            
    - Array.prototype.splice ( mutator method )
        - 원본 배열의 중간에 요소를 추가하거나 중간에 있는 요소를 제거하는 경우 splice 메서드를 사용한다.
        - splice 메서드는 3개의 매개변수가 있으며 원본 배열을 직접 변경한다.
            - start : 원본 배열의 요소를 제거하기 시작할 인덱스 
            ( -1 이면 마지막 요소, -n 이면 마지막에서 n 번째 요소를 가리킨다. )
            - deleteCount : start 부터 제거할 요소의 개수 
            ( 0 이면 아무런 요소도 제거되지 않는다. )
            - items : 제거한 위치에 삽입할 요소들의 목록
            ( 생략할 경우 원본 배열에서 요소들을 제거하기만 한다. )
            
            ```jsx
            const arr = [1, 2, 3, 4];
            
            // 원본 배열의 인덱스 1부터 2개의 요소를 제거하고 그 자리에 새로운 요소 20, 30을 삽입한다.
            const result = arr.splice(1, 2, 20, 30);
            
            // 제거한 요소가 배열로 반환된다.
            console.log(result); // [2, 3]
            // splice 메서드는 원본 배열을 직접 변경한다.
            console.log(arr); // [1, 20, 30, 4]
            ```
            
    - Array.prototype.slice ( accessor method )
        - 인수로 전달된 범위의 요소들을 복사하여 배열로 반환한다.
        원본 배열은 변경되지 않는다.
        - slice 메서드는 두 개의 매개변수를 갖는다.
            - start : 복사를 시작할 인덱스
            - end : 복사를 종료할 인덱스 
            ( 이 인덱스에 해당하는 요소는 복사되지 않는다. 
            생략하면 기본값은 length 프로퍼티 값이다. )
            
            ```jsx
            const arr = [1, 2, 3, 4];
            
            // 원본 배열의 인덱스 1부터 2개의 요소를 제거한다.
            const result = arr.splice(1, 2);
            
            // 원본 배열이 변경된다.
            console.log(arr); // [1, 4]
            // 제거한 요소가 배열로 반환된다.
            console.log(result); // [2, 3]
            
            const arr2 = [1, 2, 3];
            
            // 인수를 모두 생략하면 원본 배열의 복사본을 생성하여 반환한다.
            const copy = arr2.slice();
            console.log(copy); // [1, 2, 3]
            console.log(copy === arr2); // false
            
            // 이때 생성된 복사본은 얕은 복사(shallow copy)를 통해 생성된다.
            const todos = [
              { id: 1, content: 'HTML', completed: false },
              { id: 2, content: 'CSS', completed: true },
              { id: 3, content: 'Javascript', completed: false }
            ];
            
            // 얕은 복사(shallow copy)
            const _todos = todos.slice();
            // const _todos = [...todos];
            
            // _todos와 todos는 참조값이 다른 별개의 객체다.
            console.log(_todos === todos); // false
            
            // 배열 요소의 참조값이 같다. 즉, 얕은 복사되었다.
            console.log(_todos[0] === todos[0]); // true
            ```
            
    - Array.prototype.join
        - 원본 배열의 모든 요소를 문자열로 변환한 후, 인수로 전달받은 문자열, 즉 구분자(separator)로 연결한 문자열을 반환한다.
        ( 구분자는 생략 가능하며 기본 구분자는 콤마(” , “)다.
            
            ```jsx
            const arr = [1, 2, 3, 4];
            
            // 기본 구분자는 ','이다.
            // 원본 배열 arr의 모든 요소를 문자열로 변환한 후, 기본 구분자 ','로 연결한 문자열을 반환한다.
            arr.join(); // -> '1,2,3,4';
            
            // 원본 배열 arr의 모든 요소를 문자열로 변환한 후, 빈문자열로 연결한 문자열을 반환한다.
            arr.join(''); // -> '1234'
            
            // 원본 배열 arr의 모든 요소를 문자열로 변환한 후, 구분자 ':'로 연결한 문자열을 반환한다.ㄴ
            arr.join(':'); // -> '1:2:3:4'
            ```
            
    - Array.prototype.reverse ( mutator method )
        - 원본 배열의 순서를 반대로 뒤집는다.
        원본 배열이 변경된다.
        ( 반환 값은 변경된 배열이다. )
            
            ```jsx
            const arr = [1, 2, 3];
            const result = arr.reverse();
            
            // reverse 메서드는 원본 배열을 직접 변경한다.
            console.log(arr); // [3, 2, 1]
            // 반환값은 변경된 배열이다.
            console.log(result); // [3, 2, 1]
            ```
            
    - Array.prototype.fill ( mutator method )
        - ES6 에서 도입된 fill 메서드는 인수로 전달받은 값을 배열의 처음부터 끝까지 요소로 채운다.
        원본 배열이 변경된다.
        
        ```jsx
        const arr = [1, 2, 3];
        
        // 인수로 전달 받은 값 0을 배열의 처음부터 끝까지 요소로 채운다.
        arr.fill(0);
        
        // fill 메서드는 원본 배열을 직접 변경한다.
        console.log(arr); // [0, 0, 0]
        
        // 두번째 인수로 요소 채우기를 시작할 인덱스를 전달할 수 있다.
        const arr2 = [1, 2, 3];
        
        // 인수로 전달받은 값 0을 배열의 인덱스 1부터 끝까지 요소로 채운다.
        arr2.fill(0, 1);
        
        // fill 메서드는 원본 배열을 직접 변경한다.
        console.log(arr2); // [1, 0, 0]
        
        // 세번째 인수로 요소 채우기를 멈출 인덱스를 전달할 수 있다.
        const arr3 = [1, 2, 3, 4, 5];
        
        // 인수로 전달받은 값 0을 배열의 인덱스 1부터 3 이전(인덱스 3 미포함)까지 요소로 채운다.
        arr3.fill(0, 1, 3);
        
        // fill 메서드는 원본 배열을 직접 변경한다.
        console.log(arr3); // [1, 0, 0, 4, 5]
        ```
        
    - Array.prototype.includes
        - ES 7에서 도입된 includes 메서드는 배열 내에 특정 요소가 포함되어 있는지 확인하여 true 또는 false를 반환한다.
        첫 번째 인수로 검색할 대상을 지정한다.
        두 번째 인수로 검색을 시작할 인덱스를 전달할 수 있다.
        ( 생략할 경우 기본값 0이 설정된다. 두 번째 인수에 음수를 전달하면 length 프로퍼티 값과 음수 인덱스를 합산하여(length + index) 검색 시작 인덱스를 설정한다. )
            
            ```jsx
            const arr = [1, 2, 3];
            
            // 배열에 요소 2가 포함되어 있는지 확인한다.
            arr.includes(2); // -> true
            
            // 배열에 요소 100이 포함되어 있는지 확인한다.
            arr.includes(100); // -> false
            
            const arr2 = [1, 2, 3];
            
            // 배열에 요소 1이 포함되어 있는지 인덱스 1부터 확인한다.
            arr2.includes(1, 1); // -> false
            
            // 배열에 요소 3이 포함되어 있는지 인덱스 2(arr.length - 1)부터 확인한다.
            arr2.includes(3, -1); // -> true
            ```
            
    - Array.prototype.flat
        - ES10(ECMAScript 2019)에서 도입된 flat 메서드는 인수로 전달한 깊이만큼 재귀적으로 배열을 평탄화한다.
            
            ```jsx
            [1, [2, 3, 4, 5]].flat(); // -> [1, 2, 3, 4, 5]
            
            // 중첩 배열을 평탄화할 깊이를 인수로 전달할 수 있다.
            // 중첩 배열을 평탄화하기 위한 깊이 값의 기본값은 1이다.
            [1, [2, [3, [4]]]].flat();  // -> [1, 2, [3, [4]]]
            [1, [2, [3, [4]]]].flat(1); // -> [1, 2, [3, [4]]]
            
            // 중첩 배열을 평탄화하기 위한 깊이 값을 2로 지정하여 2단계 깊이까지 평탄화한다.
            [1, [2, [3, [4]]]].flat(2); // -> [1, 2, 3, [4]]
            // 2번 평탄화한 것과 동일하다.
            [1, [2, [3, [4]]]].flat().flat(); // -> [1, 2, 3, [4]]
            
            // 중첩 배열을 평탄화하기 위한 깊이 값을 Infinity로 지정하여 중첩 배열 모두를 평탄화한다.
            [1, [2, [3, [4]]]].flat(Infinity); // -> [1, 2, 3, 4]
            ```
            
- 배열 고차 함수
    - 고차 함수는 함수를 인수로 전달받거나 함수를 반환하는 함수
    - Array.prototype.sort ( mutator method )
        - 배열의 요소를 정렬한다. 
        원본 배열을 직접 변경하여 정렬된 배열을 반환한다.
        ( 기본적으로 오름차순으로 요소를 정렬한다. )
            
            ```jsx
            const fruits = ['Banana', 'Orange', 'Apple'];
            
            // 오름차순(ascending) 정렬
            fruits.sort();
            
            // sort 메서드는 원본 배열을 직접 변경한다.
            console.log(fruits); // ['Apple', 'Banana', 'Orange']
            
            // 내림차순(descending) 정렬
            fruits.reverse();
            
            // reverse 메서드도 원본 배열을 직접 변경한다.
            console.log(fruits); // ['Orange', 'Banana', 'Apple']
            ```
            
        - sort 메서드의 기본 정렬 순서는 유니코드 코드 포인트의 순서를 따른다. 
        배열의 요소가 숫자 타입이라 할지라도 배열의 요소를 일시적으로 문자열로 변환한 후 유니코드 코드 포인트의 순서를 기준으로 정렬한다.
        → 숫자 요소를 정렬할 때는 sort 메서드에 **정렬 순서를 정의하는 비교 함수를 인수로 전달**해야 한다.
            
            ```jsx
            const points = [40, 100, 1, 5, 2, 25, 10];
            
            // 숫자 배열의 오름차순 정렬. 비교 함수의 반환값이 0보다 작으면 a를 우선하여 정렬한다.
            points.sort((a, b) => a - b);
            console.log(points); // [1, 2, 5, 10, 25, 40, 100]
            
            // 숫자 배열에서 최소/최대값 취득
            console.log(points[0], points[points.length]); // 1
            
            // 숫자 배열의 내림차순 정렬. 비교 함수의 반환값이 0보다 크면 b를 우선하여 정렬한다.
            points.sort((a, b) => b - a);
            console.log(points); // [100, 40, 25, 10, 5, 2, 1]
            
            // 숫자 배열에서 최대값 취득
            console.log(points[0]); // 100
            ```
            
    - Array.prototype.forEach
        - for 문은 반복을 위한 변수를 선언해야 하며, 조건식과 증감식으로 이루어져 있어서 함수형 프로그래밍이 추구하는 바와 맞지 않는다.
        → forEach 메서드는 for문을 대체할 수 있는 고차 함수이다.
        - forEach 메서드는 자신의 내부에서 반복문을 실행한다.
        ( 자신을 호출한 배열을 순회하면서 수행해야 할 처리를 콜백 함수로 전달받아 반복 호출한다. )
        - forEach 메서드는 for문과는 달리 break, continue 문을 사용할 수 없다.
        ( 배열의 모든 요소를 빠짐없이 모두 순회하며 중간에 순회를 중단할 수 없다. )
        
        ```jsx
        const numbers = [1, 2, 3];
        let pows = [];
        
        // for 문으로 배열 순회
        for (let i = 0; i < numbers.length; i++) {
          pows.push(numbers[i] ** 2);
        }
        console.log(pows); // [1, 4, 9]
        
        // for 문으로 구현된 위 예제를 forEach로 구현하면 다음과 같다.
        const numbers = [1, 2, 3];
        let pows = [];
        
        // forEach 메서드는 numbers 배열의 모든 요소를 순회하면서 콜백 함수를 반복 호출한다.
        numbers.forEach(item => pows.push(item ** 2));
        console.log(pows); // [1, 4, 9]
        
        // forEach 메서드는 콜백 함수를 호출하면서 3개(요소값, 인덱스, this)의 인수를 전달한다.
        [1, 2, 3].forEach((item, index, arr) => {
          console.log(`요소값: ${item}, 인덱스: ${index}, this: ${JSON.stringify(arr)}`);
        });
        /*
        요소값: 1, 인덱스: 0, this: [1,2,3]
        요소값: 2, 인덱스: 1, this: [1,2,3]
        요소값: 3, 인덱스: 2, this: [1,2,3]
        */
        ```
        
    - Array.prototype.map ( accessor method )
        - 자신을 호출한 배열의 모든 요소를 순회하면서 인수로 전달받은 콜백 함수를 반복 호출한다.
        - **콜백 함수의 반환값들로 구성된 새로운 배열을 반환한다.**
        원본 배열은 변경되지 않는다.
        - forEach 메서드와 map 메서드의 공통점과 차이점
            - 공통점
                - 자신을 호출한 배열의 모든 요소를 순회하면서 인수로 전달받은 콜백함수를 반복 호출한다
            - 차이점
                - forEach 메서드는 언제나 undefined를 반환,
                map 메서드는 콜백 함수의 반환값들로 구성된 새로운 배열을 반환
        - map 메서드가 생성하여 반환하는 새로운 배열의 length프로퍼티 값은 map 메서드를 호출한 배열의 length 프로퍼티 값과 반드시 일치한다.
        ( 즉, map 메서드를 호출한 배열과 map 메서드가 생성하여 반환한 배열은 1:1 매핑한다. )
            
            ```jsx
            // map 메서드는 콜백 함수를 호출하면서 3개(요소값, 인덱스, this)의 인수를 전달한다.
            [1, 2, 3].map((item, index, arr) => {
              console.log(`요소값: ${item}, 인덱스: ${index}, this: ${JSON.stringify(arr)}`);
              return item;
            });
            /*
            요소값: 1, 인덱스: 0, this: [1,2,3]
            요소값: 2, 인덱스: 1, this: [1,2,3]
            요소값: 3, 인덱스: 2, this: [1,2,3]
            */
            ```
            
    - Array.prototype.filter ( accessor method )
        - 자신을 호출한 배열의 모든 요소를 순회하면서 인수로 전달받은 콜백 함수를 반복 호출한다.
        **콜백 함수의 반환값이 true인 요소로만 구성된 새로운 배열을 반환한다.**
        원본 배열은 변경되지 않는다.
        - filter 메서드는 자신을 호출한 배열에서 필터링 조건을 만족하는 특정 요소만 추출하여 새로운 배열을 만들고 싶을 때 사용한다.
            
            ```jsx
            // filter 메서드는 콜백 함수를 호출하면서 3개(요소값, 인덱스, this)의 인수를 전달한다.
            [1, 2, 3].filter((item, index, arr) => {
              console.log(`요소값: ${item}, 인덱스: ${index}, this: ${JSON.stringify(arr)}`);
              return item % 2;
            });
            /*
            요소값: 1, 인덱스: 0, this: [1,2,3]
            요소값: 2, 인덱스: 1, this: [1,2,3]
            요소값: 3, 인덱스: 2, this: [1,2,3]
            */
            ```
            
    - Array.prototype.reduce ( accessor method )
        - 자신을 호출한 배열의 모든 요소를 순회하며 인수로 전달받은 콜백 함수를 반복 호출한다.
        콟개 함수의 반환값을 다음 순회 시에 콜백 함수의 첫 번째 인수로 전달하면서 콜백 함수를 호출하여 **하나의 결과값을 만들어 반환한다.**
        원본 배열은 변경되지 않는다.
        - reduce 메서드는 4개의 인수, 초기값 또는 콜백 함수 이전의 반환값, reduce 메서드를 호출한 배열의 요소값과 인덱스, reduce 메서드를 호출한 배열 자체(this)가 전달된다.
        - reduce 메서드를 호출할 때는 초기값을 생략하지 말고 언제나 전달하는 것이 안전하다.
            
            ```jsx
            // [1, 2, 3, 4]의 모든 요소의 누적을 구한다.
            const sum = [1, 2, 3, 4].reduce((accumulator, currentValue, index, array) => accumulator + currentValue, 0);
            
            console.log(sum); // 10
            ```
            
    - Array.prototype.some
        - 자신을 호출한 배열의 요소를 순회하면서 인수로 전달된 콜백 함수를 호출한다.
        some 메서드는 콜백 함수의 반환값이 단 한 번이라도 참이면 true, 모두 거짓이면 false를 반환한다.
            
            ```jsx
            // 배열의 요소 중에 10보다 큰 요소가 1개 이상 존재하는지 확인
            [5, 10, 15].some(item => item > 10); // -> true
            
            // 배열의 요소 중에 0보다 작은 요소가 1개 이상 존재하는지 확인
            [5, 10, 15].some(item => item < 0); // -> false
            
            // 배열의 요소 중에 'banana'가 1개 이상 존재하는지 확인
            ['apple', 'banana', 'mango'].some(item => item === 'banana'); // -> true
            
            // some 메서드를 호출한 배열이 빈 배열인 경우 언제나 false를 반환한다.
            [].some(item => item > 3); // -> false
            ```
            
    - Array.prototype.every
        - 자신을 호출한 배열의 요소를 순회하면서 인수로 전달된 콜백 함수를 호출한다.
        every 메서드는 콜백 함수의 반환값이 모두 참이면 true, 단 한 번이라도 거짓이면 false를 반환한다.
            
            ```jsx
            // 배열의 모든 요소가 3보다 큰지 확인
            [5, 10, 15].every(item => item > 3); // -> true
            
            // 배열의 모든 요소가 10보다 큰지 확인
            [5, 10, 15].every(item => item > 10); // -> false
            
            // every 메서드를 호출한 배열이 빈 배열인 경우 언제나 true를 반환한다.
            [].every(item => item > 3); // -> true
            ```
            
    - Array.prototype.find
        - 자신을 호출한 배열의 요소를 순회하면서 인수로 전달된 콜백 함수를 호출하여 반환값이 true 인 첫 번째 요소를 반환한다.
        ( 반환값이 true인 요소가 존재하지 않는다면 undefined를 반환한다. )
            
            ```jsx
            const users = [
              { id: 1, name: 'Lee' },
              { id: 2, name: 'Kim' },
              { id: 2, name: 'Choi' },
              { id: 3, name: 'Park' }
            ];
            
            // id가 2인 첫 번째 요소를 반환한다. find 메서드는 배열이 아니라 요소를 반환한다.
            users.find(user => user.id === 2); // -> {id: 2, name: 'Kim'}
            ```
            
    - Array.prototype.findIndex
        - ES6에서 도입된 findIndex 메서드는 자신을 호출한 배열의 요소를 순회하면서 인수로 전달된 콜백 함수를 호출하여 반환값이 true인 첫 번째 인덱스를 반환한다.
        ( 콜백 함수의 반환값이 true 인 요소가 존재하지 않는다면 -1 을 반환한다. )
            
            ```jsx
            const users = [
              { id: 1, name: 'Lee' },
              { id: 2, name: 'Kim' },
              { id: 2, name: 'Choi' },
              { id: 3, name: 'Park' }
            ];
            
            // id가 2인 요소의 인덱스를 구한다.
            users.findIndex(user => user.id === 2); // -> 1
            
            // name이 'Park'인 요소의 인덱스를 구한다.
            users.findIndex(user => user.name === 'Park'); // -> 3
            
            // 위와 같이 프로퍼티 키와 프로퍼티 값으로 요소의 인덱스를 구하는 경우
            // 다음과 같이 콜백 함수를 추상화할 수 있다.
            function predicate(key, value) {
              // key와 value를 기억하는 클로저를 반환
              return item => item[key] === value;
            }
            
            // id가 2인 요소의 인덱스를 구한다.
            users.findIndex(predicate('id', 2)); // -> 1
            
            // name이 'Park'인 요소의 인덱스를 구한다.
            users.findIndex(predicate('name', 'Park')); // -> 3
            ```
            
    - Array.prototype.flatMap
        - ES10에서 도입된 faltMap 메서드는 map 메서드를 통해 생성된 새로운 배열을 평탄화한다.
        ( 즉, map 메서드와 flat 메서드를 순차적으로 실행하는 효과가 있다. )
        ( 단, flatMap 메서드는 flat 메서드처럼 인수를 전달하여 평탄화 깊이를 지정할 수는 없고 1단계만 평탄화한다. )
            
            ```jsx
            const arr = ['hello', 'world'];
            
            // flatMap은 1단계만 평탄화한다.
            arr.flatMap((str, index) => [index, [str, str.length]]);
            // -> [[0, ['hello', 5]], [1, ['world', 5]]] => [0, ['hello', 5], 1, ['world', 5]]
            
            // 평탄화 깊이를 지정해야 하면 flatMap 메서드를 사용하지 말고 map 메서드와 flat 메서드를 각각 호출한다.
            arr.map((str, index) => [index, [str, str.length]]).flat(2);
            // -> [[0, ['hello', 5]], [1, ['world', 5]]] => [0, 'hello', 5, 1, 'world', 5]
            ```