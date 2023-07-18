### CH. 21 빌트인 객체

- 자바스크립트의 객체는 다음과 같이 크게 3개의 객체로 분류할 수 있다.
    - 표준 빌트인 객체
        - 표준 빌트인 객체는 ECMAScript 사양에 정의된 객체를 말하며, 애플리케이션 전역의 공통 기능을 제공한다. 
        → 자바스크립트 실행 환경(브라우저 또는 Node.js 환경)과 관계없이 언제나 사용할 수 있다.
        - 표준 빌트인 객체는 전역 객체의 프로퍼티로서 제공된다.
        별도의 선언 없이 전역 변수처럼 언제나 참조할 수 있다.
    - 호스트 객체
        - 브라우저 환경에서는 클라이언트 사이드 Web API 를 호스트 객체로 제공,
        Node.js 환경에서는 Node.js 고유의 API를 호스트 객체로 제공.
    - 사용자 정의 객체
        - 사용자가 직접 정의한 객체
- 표준 빌트인 객체
    - Math, Reflect, JSON 을 제외한 표준 빌트인 객체는 모두 인스턴스를 생성할 수 있는 생성자 함수 객체이다. 
    **생성자 함수 객체인 표준 빌트인 객체**는 **프로토타입 메서드와 정적 메서드를 제공**하고 **생성자 함수 객체가 아닌 표준 빌트인 객체**는 **정적 메서드만 제공**한다.
        
        ```jsx
        // String 생성자 함수에 의한 String 객체 생성
        const strObj = new String('Lee'); // String {"Lee"}
        console.log(typeof strObj);       // object
        
        // Number 생성자 함수에 의한 Number 객체 생성
        const numObj = new Number(123); // Number {123}
        console.log(typeof numObj);     // object
        
        // Boolean 생성자 함수에 의한 Boolean 객체 생성
        const boolObj= new Boolean(true); // Boolean {true}
        console.log(typeof boolObj);      // object
        
        // Function 생성자 함수에 의한 Function 객체(함수) 생성
        const func = new Function('x', 'return x * x'); // ƒ anonymous(x )
        console.log(typeof func);                       // function
        
        // Array 생성자 함수에 의한 Array 객체(배열) 생성
        const arr = new Array(1, 2, 3); // (3) [1, 2, 3]
        console.log(typeof arr);        // object
        
        // RegExp 생성자 함수에 의한 RegExp 객체(정규 표현식) 생성
        const regExp = new RegExp(/ab+c/i); // /ab+c/i
        console.log(typeof regExp);         // object
        
        // Date 생성자 함수에 의한 Date 객체 생성
        const date = new Date();  // Fri May 08 2020 10:43:25 GMT+0900 (대한민국 표준시)
        console.log(typeof date); // object
        ```
        
        - 표준 빌트인 객체의 prototype 프로퍼티에 바인딩된 객체(ex> String.prototype)는 다양한 기능의 빌트인 프로토타입 메서드를 제공한다.
        표준 빌트인 객체는 인스턴스 없이도 호출 가능한 빌트인 정적 메서드를 제공한다.
- 원시값과 래퍼 객체
    
    ```jsx
    const str = 'hello';
    
    // 원시 타입인 문자열이 프로퍼티와 메서드를 갖고 있는 객체처럼 동작한다.
    console.log(str.length); // 5
    console.log(str.toUpperCase()); // HELLO
    ```
    
    - 원시값인 문자열, 숫자, 불리언 값의 경우 이들 원시값에 대해 마치 객체처럼 마침표 표기법(또는 대괄호 표기법)으로 접근하면 자바스크립트 엔진이 일시적으로 원시값을 연관된 객체로 변환해 주기 때문이다.
    - 원시값을 객체처럼 사용하면 자바스크립트 엔진은 암묵적으로 연관된 객체를 생성하여 생성된 객체로 프로퍼티에 접근하거나 메서드를 호출하고 다시 원시값으로 되돌린다.
    - 이처럼 ****************************************************************************************************************************************************************************************************************************************************문자열, 숫자, 불리언 값에 대해 객체처럼 접근하면 생성되는 임시 객체를 래퍼 객체(wrapper object)****************************************************************************************************************************************************************************************************************************************************라 한다.
        
        ```jsx
        const str = 'hi';
        
        // 원시 타입인 문자열이 래퍼 객체인 String 인스턴스로 변환된다.
        console.log(str.length); // 2
        console.log(str.toUpperCase()); // HI
        
        // 래퍼 객체로 프로퍼티에 접근하거나 메서드를 호출한 후, 다시 원시값으로 되돌린다.
        console.log(typeof str); // string
        ```
        
        ![식별자가 원시값을 갖도록 되돌리고 래퍼 객체는 가비지 컬렉션의 대상이 된다.](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ba260da6-e96a-46f2-83ff-c4e6e78e455e/Untitled.png)
        
        식별자가 원시값을 갖도록 되돌리고 래퍼 객체는 가비지 컬렉션의 대상이 된다.
        
- **String, Number, Boolean 생성자 함수를 new 연산자와 함께 호출하여 문자열, 숫자, 불리언 인스턴스를 생성할 필요가 없으며 권장하지도 않는다.**
- 문자열, 숫자, 불리언, 심벌 이외의 원시값, 즉 null과 undefined는 래퍼 객체를 생성하지 않는다.
→ 따라서 null과 undefined 값을 객체처럼 사용하면 에러가 발생한다.
- 전역 객체
    - 전역 객체(global object)는 코드가 실행되기 이전 단계에 자바스크립트 엔진에 의해 어떤 객체보다도 먼저 생성되는 특수한 객체, 어떤 객체에도 속하지 않은 최상위 객체이다.
    ( 브라우저 환경에서는 window(또는 self, this, frames)가 전역 객체, 
     Node.js 환경에서는 global이 전역 객체를 가리킨다. )
    - 전역 객체 자신은 어떤 객체의 프로퍼티도 아니며 객체의 계층적 구조상 표준 빌트인 객체와 호스트 객체를 프로퍼티로 소유한다는 것을 말한다.
    - 전역 객체의 특징
        - 전역 객체는 개발자가 의도적으로 생성할 수 없다.
        - 전역 객체의 프로퍼티를 참조할 때 window(또는 global)를 생략할 수 있다.
            
            ```jsx
            // 문자열 'F'를 16진수로 해석하여 10진수로 변환하여 반환한다.
            window.parseInt('F', 16); // -> 15
            // window.parseInt는 parseInt로 호출할 수 있다.
            parseInt('F', 16); // -> 15
            
            window.parseInt === parseInt; // -> true
            ```
            
        - 전역 객체는 Object, String, Number, Boolean, Function, Array, RegExp, Date, Math, Promise 같은 모든 표준 빌트인 객체를 프로퍼티로 가지고 있다.
        - 자바스크립트 실행 환경에서는 호스트객체를 제공한다.
        - var 키워드로 선언한 전역 변수와 선언하지 않은 변수에 값을 할당한 암묵적 전역, 그리고 전역 함수는 전역 객체의 프로퍼티가 된다.
            
            ```jsx
            // var 키워드로 선언한 전역 변수
            var foo = 1;
            console.log(window.foo); // 1
            
            // 선언하지 않은 변수에 값을 암묵적 전역. bar는 전역 변수가 아니라 전역 객체의 프로퍼티다.
            bar = 2; // window.bar = 2
            console.log(window.bar); // 2
            
            // 전역 함수
            function baz() { return 3; }
            console.log(window.baz()); // 3
            ```
            
        - let 이나 const 키워드로 선언한 전역 변수는 전역 객체의 프로퍼티가 아니다.
        let 이나 const 키워드로 선언한 전역 변수는 보이지 않는 개념적인 블록(전역 렉시컬 환경의 선언적 환경 레코드) 내에 존재하게 된다.
        (즉, window.foo 와 같이 접근할 수 없다.)
        - 브라우저 환경의 모든 자바스크립트 코드는 하나의 전역 객체 window를 공유한다.
        여러 개의 script 태그를 통해 자바스크립트 코드를 분리해도 하나의 전역 객체window를 공유하는 것은 변함이 없다.
        이는 분리되어 있는 자바스크립트 코드가 하나의 전역을 공유한다는 의미이다.
    - 빌트인 전역 프로퍼티
        - 빌트인 전역 프로퍼티는 전역 객체의 프로퍼티를 의미한다.
            - Infinity
                
                ```jsx
                // 전역 프로퍼티는 window를 생략하고 참조할 수 있다.
                console.log(window.Infinity === Infinity); // true
                
                // 양의 무한대
                console.log(3/0);  // Infinity
                // 음의 무한대
                console.log(-3/0); // -Infinity
                // Infinity는 숫자값이다.
                console.log(typeof Infinity); // number
                ```
                
            - NaN
                
                ```jsx
                console.log(window.NaN); // NaN
                
                console.log(Number('xyz')); // NaN
                console.log(1 * 'string');  // NaN
                console.log(typeof NaN);    // number
                ```
                
            - undefined
                
                ```jsx
                console.log(window.undefined); // undefined
                
                var foo;
                console.log(foo); // undefined
                console.log(typeof undefined); // undefined
                ```
                
    - 빌트인 전역 함수
        - 빌트인 전역 함수는 전역에서 호출할 수 있는 빌트인 함수로서 전역 객체의 메서드이다.
            - eval - **eval 함수의 사용은 금지해야한다.**
                - eval 함수는 자바스크립트 코드를 나타내는 문자열을 인수로 받는다.
                - 전달받은 문자열 코드가 표현식이라면 eval 함수는 문자열 코드를 런타임에 평가하여 값을 생성하고, 전달받은 인수가 표현식이 아닌 문이라면 eval 함수는 문자열 코드를 런타임에 실행한다.
                (문자열 코드가 여러 개의 문으로 이루어져 있다면 모든 문을 실행한다.)
                - **eval 함수는 기존의 스코프를 런타임에 동적으로 수정한다.**
                - 단, strict mode에서 eval 함수는 기존의 스코프를 수정하지 않고 eval 함수 자신의 자체적인 스코프를 생성한다.
                - 인수로 전달받은 문자열 코드가 let, const 키워드를 사용한 변수 선언문이라면 암묵적으로 strict mode 가 적용된다.
            - isFinite
                - 전달받은 인수가 정상적인 유한수인지 검사하여 유한수이면 true,
                무한수이면 false 를 반환한다.
                - isFinite(null)은 true를 반환한다. 
                → null을 숫자로 변환하여 검사를 수행했기 때문이다.
                (null을 숫자 타입으로 변환하면 0이 된다.)
            - isNaN
                - 전달받은 인수가 NaN인지 검사하여 그 결과를 불리언 타입으로 반환한다.
                ( 전달받은 인수의 타입이 숫자가 아니면 숫자로 타입을 변환후 검사를 수행한다. )
            - parseFloat
                - 전달받은 문자열 인수를 부동 소수점 숫자, 즉 실수로 해석(parsing)하여 반환한다.
                    
                    ```jsx
                    // 문자열을 실수로 해석하여 반환한다.
                    parseFloat('3.14');  // -> 3.14
                    parseFloat('10.00'); // -> 10
                    
                    // 공백으로 구분된 문자열은 첫 번째 문자열만 변환한다.
                    parseFloat('34 45 66'); // -> 34
                    parseFloat('40 years'); // -> 40
                    
                    // 첫 번째 문자열을 숫자로 변환할 수 없다면 NaN을 반환한다.
                    parseFloat('He was 40'); // -> NaN
                    
                    // 앞뒤 공백은 무시된다.
                    parseFloat(' 60 '); // -> 60
                    ```
                    
            - parseInt
                - 전달받은 문자열 인수를 정수로 해석하여 반환한다.
                - 두 번째 인수로 진법을 나타내는 기수(2~36)를 전달할 수 있다.
                    
                    ```jsx
                    const x = 15;
                    
                    // 10진수 15를 2진수로 변환하여 그 결과를 문자열로 반환한다.
                    x.toString(2); // -> '1111'
                    // 문자열 '1111'을 2진수로 해석하고 그 결과를 10진수 정수로 반환한다
                    parseInt(x.toString(2), 2); // -> 15
                    
                    // 10진수 15를 8진수로 변환하여 그 결과를 문자열로 반환한다.
                    x.toString(8); // -> '17'
                    // 문자열 '17'을 8진수로 해석하고 그 결과를 10진수 정수로 반환한다
                    parseInt(x.toString(8), 8); // -> 15
                    
                    // 10진수 15를 16진수로 변환하여 그 결과를 문자열로 반환한다.
                    x.toString(16); // -> 'f'
                    // 문자열 'f'를 16진수로 해석하고 그 결과를 10진수 정수로 반환한다
                    parseInt(x.toString(8), 8); // -> 15
                    
                    // 숫자값을 문자열로 변환한다.
                    x.toString(); // -> '15'
                    // 문자열 '15'를 10진수로 해석하고 그 결과를 10진수 정수로 반환한다
                    parseInt(x.toString()); // -> 15
                    ```
                    
                - 첫 번째 인수로 전달된 문자열이 “0x” 또는 “0X”로 시작하는 16진수 리터럴이라면 16진수로 해석하여 10진수 정수로 반환한다.
                ( 하지만 2진수 리터럴과 8진수 리터럴은 제대로 해석하지 못한다. )
                → 문자열을 8진수로 해석하려면 지수를 반드시 지정해야 한다.
                - 주의
                    - 첫 번째 인수로 전달한 문자열의 첫 번째 문자가 해당 지수의 숫자로 변환될 수 없다면 NaN을 반환한다.
                        
                        ```jsx
                        // 'A'는 10진수로 해석할 수 없다.
                        parseInt('A0'); // -> NaN
                        // '2'는 2진수로 해석할 수 없다.
                        parseInt('20', 2); // -> NaN
                        ```
                        
                    - 첫 번째 인수로 전달한 문자열의 두 번째 문자부터 해당 진수를 나타내는 숫자가 아닌 문자(예를 들어 2진수의 경우 2)와 마주치면 이 문자와 계속되는 문자들은 전부 무시되며 해석된 정수값만 반환한다.
                        
                        ```jsx
                        // 10진수로 해석할 수 없는 'A' 이후의 문자는 모두 무시된다.
                        parseInt('1A0'); // -> 1
                        // 2진수로 해석할 수 없는 '2' 이후의 문자는 모두 무시된다.
                        parseInt('102', 2); // -> 2
                        // 8진수로 해석할 수 없는 '8' 이후의 문자는 모두 무시된다.
                        parseInt('58', 8); // -> 5
                        // 16진수로 해석할 수 없는 'G' 이후의 문자는 모두 무시된다.
                        parseInt('FG', 16); // -> 15
                        ```
                        
                    - 첫번째 인수로 전달한 문자열에 공백이 있다면 첫 번째 문자열만 해석하여 반환하며 앞뒤 공백은 무시된다.
                    ( 만일 첫 번째 문자열을 숫자로 해석할 수 없는 경우 NaN을 반환한다. )
                        
                        ```jsx
                        // 공백으로 구분된 문자열은 첫 번째 문자열만 변환한다.
                        parseInt('34 45 66'); // -> 34
                        parseInt('40 years'); // -> 40
                        // 첫 번째 문자열을 숫자로 변환할 수 없다면 NaN을 반환한다.
                        parseInt('He was 40'); // -> NaN
                        // 앞뒤 공백은 무시된다.
                        parseInt(' 60 '); // -> 60
                        ```
                        
            - encodeURI / decodeURI
                - encodeURI 함수는 완전한 URI를 문자열로 전달받아 이스케이프 처리를 위해 인코딩한다.
                - 인코딩이란 URI의 문자들을 이스케이프 처리하는 것을 의미한다.
                
                ```jsx
                const uri = 'http://example.com?name=이웅모&job=programmer&teacher';
                
                // encodeURI 함수는 완전한 URI를 전달받아 이스케이프 처리를 위해 인코딩한다.
                const enc = encodeURI(uri);
                console.log(enc);
                // http://example.com?name=%EC%9D%B4%EC%9B%85%EB%AA%A8&job=programmer&teacher
                
                // decodeURI 함수는 인코딩된 완전한 URI를 전달받아 이스케이프 처리 이전으로 디코딩한다.
                const dec = decodeURI(enc);
                console.log(dec);
                // http://example.com?name=이웅모&job=programmer&teacher
                ```
                
            - encodeURIComponent / decodeURIComponent
                - encodeURIComponent 함수는 URI 구성 요소(component)를 인수로 전달받아 인코딩한다.
                - encodeURIComponent 함수는 인수로 전달된 문자열을 URI의 구성요소인 쿼리 스트링의 일부로 간주한다.
                → 쿼리 스트링 구분자로 사용되는 = , ? , & 까지 인코딩한다.
                (반면에 encodeURI 함수는 매개변수로 전달된 문자열을 완전한 URI 전체라고 간주한다. 
                → 쿼리 스트링 구분자로 사용되는 = , ? , & 은 인코딩하지 않는다.)
                
                ```jsx
                // URI의 쿼리 스트링
                const uriComp = 'name=이웅모&job=programmer&teacher';
                
                // encodeURIComponent 함수는 인수로 전달받은 문자열을 URI의 구성요소인 쿼리 스트링의 일부로 간주한다.
                // 따라서 쿼리 스트링 구분자로 사용되는 =, ?, &까지 인코딩한다.
                let enc = encodeURIComponent(uriComp);
                console.log(enc);
                // name%3D%EC%9D%B4%EC%9B%85%EB%AA%A8%26job%3Dprogrammer%26teacher
                
                let dec = decodeURIComponent(enc);
                console.log(dec);
                // 이웅모&job=programmer&teacher
                
                // encodeURI 함수는 인수로 전달받은 문자열을 완전한 URI로 간주한다.
                // 따라서 쿼리 스트링 구분자로 사용되는 =, ?, &를 인코딩하지 않는다.
                enc = encodeURI(uriComp);
                console.log(enc);
                // name=%EC%9D%B4%EC%9B%85%EB%AA%A8&job=programmer&teacher
                
                dec = decodeURI(enc);
                console.log(dec);
                // name=이웅모&job=programmer&teacher
                ```
                
    - 암묵적 전역
        - 자바스크립트 엔진은 y = 20을 window.y = 20 으로 해석하여 전역 객체에 프로퍼티를 동적 생성한다.
        → y는 전역 객체의 프로퍼티가 되어 마치 전역 변수 처럼 동작한다.
        (이러한 현상을 ******************************암묵적 전역******************************이라고 한다.)
        - 또한, 변수가 아니라 단지 프로퍼티인 y는 delete 연산자로 삭제할 수 있다.
        전역 변수는 프로퍼티이지만 delete 연산자로 삭제할 수 없다.
            
            ```jsx
            var x = 10; // 전역 변수
            
            function foo () {
              // 선언하지 않은 식별자에 값을 할당
              y = 20; // window.y = 20;
              console.log(x + y);
            }
            
            foo(); // 30
            
            console.log(window.x); // 10
            console.log(window.y); // 20
            
            delete x; // 전역 변수는 삭제되지 않는다.
            delete y; // 프로퍼티는 삭제된다.
            
            console.log(window.x); // 10
            console.log(window.y); // undefined
            ```