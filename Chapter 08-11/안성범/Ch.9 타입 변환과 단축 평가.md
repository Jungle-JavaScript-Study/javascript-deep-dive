### CH. 9 타입 변환과 단축 평가

- 타입 변환
    - 개발자가 의도적으로 값의 타입을 변환하는 것을 **********************************************명시적 타입 변환(explicit coercion)********************************************** 또는 **************************타입 캐스팅**************************이라 한다.
    - 개발자의 의도와는 상관없이 표현식을 평가하는 도중에 자바스크립트 엔진에 의해 암묵적으로 타입이 자동 변환 되기도 한다. 이를 ************************************************************암묵적 타입 변환(implicit coercion)************************************************************ 또는 **********타입 강제 변환**********이라 한다.
    - 명시적 타입 변환이나 암묵적 타입 변환이 기존 원시 값을 **직접 변경하는 것이 아니다.**
    타입 변환이란 기존 원시 값을 사용해 다른 타입의 새로운 원시 값을 생성하는 것이다.
    - 암묵적 타입 변환은 기존 변수 값을 재할당하여 변경하는 것이 아니다.
    자바스크립트 엔진은 표현식을 에러 없이 평가하기 위해 피연산자의 값을 암묵적 타입 변환해 새로운 타입의 값을 만들어 단 한 번 사용하고 버린다.
    - 중요한 것은 코드를 예측할 수 있어야 한다는 것이다.
    동료가 작성한 코드를 정확히 이해할 수 있어야 하고 자신이 작성한 코드도 동료가 쉽게 이해할 수 있어야 한다.
    - 암묵적 타입 변환
        - 표현식을 평가할 때 코드의 문맥에 부합하지 않는 다양한 상황이 발생할 수 있다.
            
            ```jsx
            // 피연산자가 모두 문자열 타입이어야 하는 문맥
            '10' + 2 // 102
            // 피연산자가 모두 숫자 타입이어야 하는 문맥
            5 * '10' // 50
            // 피연산자 또는 표현식이 불리언 타입이어야 하는 문제
            !0 // true
            if (1) { }
            ```
            
        - 문자열 타입으로 변환
            
            ```jsx
            1 + '2' // "12"
            ```
            
            - + 연산자는 피연산자 중 하나 이상이 문자열이면 문자열 연결 연산자로 동작한다.
            - 자바스크립트 엔진은 문자열 연결 연산자 표현식을 평가하기 위해 문자열 연결 연산자의 피연산자 중에서 문자열 타입이 아닌 피연산자를 문자열 타입으로 암묵적 타입 변환한다.
                
                ```jsx
                // 숫자 타입
                0 + ''; // "0"
                -0 + ''; // "0"
                1 + ''; // '1'
                -1 + ''; // '1'
                NaN + ''; // 'NaN'
                Infinity + ''; // 'Infinity'
                -Infinity + ''; // '-Infinity'
                
                // 불리언 타입
                true + ''; // 'true;
                false + ''; // 'false;
                
                // null 타입
                null + ''; // 'null'
                
                // undefined 타입
                undefined + ''; // 'undefined'
                
                // 심벌 타입
                (Symbol()) + '' // TypeError: Canot convert a Symbol value to string
                
                // 객체 타입
                ({}) + ''; // '[object Object]'
                Math + ''; // '[object Math]'
                [] + ''; // ""
                [10,20] + ''; // '10,20'
                (function() {}) + ''; // 'function(){}'
                Array + '' // 'function Array() { [native code] }'
                ```
                
        - 숫자 타입으로 변환
            - 산술 연산자의 역할은 숫자 값을 만드는 것이다.
                
                ```jsx
                1 - '1' // 0
                1 * '10' // 10
                1 / 'one' // NaN
                ```
                
            - 비교 연산자의 역할은 불리언 값을 만드는 것이다. > 비교 연산자는 피연산자의 크기를 비교하므로 모든 피연산자 타입은 코드의 문맥상 숫자 타입이어야한다.
                
                ```jsx
                '1' > 0 // true
                ```
                
            - 빈 문자열(’’), 빈 배열([]), null, false 는 0으로, true 는 1로 변환된다. **객체와 빈 배열이 아닌 배열, undefined는 변환되지 않아 NaN이 된다는 것에 주의**
                
                ```
                // 문자열 타입
                +''; // 0
                +'0'; // 0
                +'1'; // 1
                +'string'; // NaN
                
                // 불리언 타입
                +true; // 1
                +false; // 0
                
                // null 타입
                +null; // 0
                +undefined; // NaN
                
                // 심벌 타입
                +(Symbol()); // TypeError: Cannot conver a Symbol value to a number
                
                // 객체 타입
                +{}; // NaN
                +[]; // 0
                +[10,20]; // NaN
                +(function(){}) // NaN
                ```
                
        - 불리언 타입으로 변환
            - 자바스크립트 엔진은 조건식의 평가 결과를 불리언 타입으로 암묵적 타입 변환한다.
            - 이 때 불리언 타입이 아닌 값을 **Truthy 값(참으로 평가되는 값) or Falsy 값(거짓으로 평가되는 값)으로 구분한다.**
            - false 로 평가되는 Falsy 값 (6가지)
                - false
                - null
                - NaN
                - undefined
                - 0, -0
                - ''(빈 문자열)
    - 명시적 타입 변환
        - 개발자의 의도에 따라 명시적으로 타입을 변경하는 방법은 다양하다.
        - **표준 빌트인 생성자 함수**(String, Number, Boolean)를 **new 연산자 없이 호출하는 방법,
        빌트인 메서드를 사용하는 방법**, 
        **암묵적 타입 변환을 이용하는 방법**이 있다.
        - 문자열 타입으로 변환
            1. String 생성자 함수를 new 연산자 없이 호출하는 방법
            2. Object.prototype.toString 메서드를 사용하는 방법
            3. 문자열 연결 연산자를 사용하는 방법
            
            ```jsx
            // 1. String 생성자 함수 new 연산자 없이 호출하는 방법
            // 숫자 타입 => 문자열 타입
            String(1); // '1'
            String(NaN); // 'NaN'
            String(Infinity); // 'Infinity'
            // 불리언 타입 => 문자열 타입
            String(true); // 'true'
            String(false); // 'false'
            
            // 2. Object.prototype.toString 메서드를 사용하는 방법
            // 숫자 타입 => 문자열 타입
            (1).toString(); // '1'
            (NaN).toString(); // 'NaN'
            (Infinity).toString(); // 'Infinity'
            // 불리언 타입 => 문자열 타입
            (true).toString(); // 'true'
            (false).toString(); // 'false'
            
            // 3. 문자열 연결 연산자를 이용하는 방법
            // 숫자 타입 => 문자열 타입
            1 + ''; // '1'
            NaN + ''; // 'NaN'
            Infinity + ''; // 'Infinity'
            // 불리언 타입 => 문자열 타입
            true + ''; // 'true'
            false + ''; // 'false'
            ```
            
        - 숫자 타입으로 변환
            1. Number 생성자 함수를 new 연산자 없이 호출하는 방법
            2. parseInt, parseFloat 함수를 사용하는 방법(문자열만 숫자 타입으로 변환 가능)
            3. + 단항 산술 연산자를 이용하는 방법
            4. *  산술 연산자를 이용하는 방법
            
            ```jsx
            // 1. Number 생성자 합수를 new 연산자 없이 호출하는 방법
            // 문자열 타입 => 숫자 타입
            Number('0'); // 0
            Number('-1'); // -1
            Number('10.53'); // 10.53
            // 불리언 타입 => 숫자 타입
            Number(true); // 1
            Number(false); // 0
            
            // 2. parseInt, parseFloat 함수를 사용하는 방법
            // 문자열 타입 => 숫자 타입
            parseInt('0'); // 0
            parseInt('-1'); // -1
            parseInt('10.53'); // 10.53
            
            // 3. +단항 산술 연산자를 이용하는 방법
            // 문자열 타입 => 숫자 타입
            +'0'; // 0
            +'-1'; // 0
            +'10.53'; // 0
            // 불리언 타입 => 숫자 타입
            +true; // 1
            -false; // 0
            
            // 4. *산술 연산자를 이용하는 방법
            // 문자열 타입 => 숫자 타입
            '0' * 1; // 0
            '1' * 1; // 1
            '10.53' * 1; // 10.53
            // 불리언 타입 => 숫자 타입
            true * 1; // 1
            false * 1; // 0
            ```
            
    - 불리언 타입으로 변환
        1. Boolean 생성자 함수를 new 연산자 없이 호출하는 방법
        2. ! 부정 논리 연산자를 두 번 사용하는 방법
        
        ```jsx
        // 1. Boolean 생성자 합수를 new 연산자 없이 호출하는 방법
        // 문자열 타입 => 불리언 타입
        Boolean('x'); // true
        Boolean(''); // false
        Boolean('false'); // true
        // 숫자 타입 => 불리언 타입
        Boolean(0); // false
        Boolean(1); // true
        Boolean(NaN); // false
        Boolean(Infinity); // true
        // null 타입
        Boolean(null); // false;
        // undefined 타입
        Boolean(undefined); // false;
        // 객체 타입
        Boolean({}); // true
        Boolean([]); // true
        
        // 2. ! 부정 논리 연산자를 두 번 사용하는 방법
        // 문자열 타입 => 불리언 타입
        !!'x'; // true
        !!''; // false
        !!'false'; // true
        // 숫자 타입 => 불리언 타입
        !!0; // false
        !!1; // true
        !!NaN; // false
        !!Infinity; // true
        // null 타입
        !!null; // false;
        // undefined 타입
        !!undefined; // false;
        // 객체 타입
        !!{}; // true
        !![]; // true
        ```
        
- 단축 평가
    - 논리 연산자를 사용한 단축 평가
        - 논리곱(&&) 연산자는 두 개의 피연산자가 모두 true 로 평가될 때 true 를 반환한다.
        - 논리곱 연산자는 **논리 연산의 결과를 결정하는 두 번째 피연산자를 반환**한다.
        - 논리합(||) 연산자는 두 개의 피 연산자 중 하나만 true 로 평가돼도 true 를 반환한다.
        - 논리합 연산자는 **논리 연산의 결과를 결정한 첫 번째 피연산자를 반환**한다.
        - 논리연산자는 논리 연산의 결과를 결정하는 피연산자를 **타입 변환하지 않고 그대로 반환**한다.
        - **단축 평가**는 표현식을 평가하는 도중에 **평가 결과가 확정된 경우 나머지 평가 과정을 생략**하는 것을 말한다.
            
            
            | 단축 평가 표현식 | 평가 결과 |
            | --- | --- |
            | true || anything | true |
            | false || anything | anything |
            | true && anything | anything |
            | false && anything | false |
            | ‘Cat’ || ‘Dog’ | “Cat” |
            | ‘Cat’ && ‘Dog’ | “Dog” |
        - 단축평가는 다음 상황에서 유용하게 사용된다.
            - 객체를 가리키기를 기대하는 변수가 null 또는 undefined가 아닌지 확인하고 프로퍼티를 참조할 때
                - 객체를 가리키기를 기대하는 변수의 값이 객체가 아니라 null 또는 undefined인 경우 객체의 프로퍼티를 참조하면 타입 에러(TypeError)가 발생한다. 에러가 발생하면 프로그램이 강제 종료된다.
                    
                    ```jsx
                    var elem = null;
                    // elem이 null이거나 undefined와 같은 Falsy 값이면 null로 평가되고
                    // elem이 Truthy 값이면 elem.value로 평가된다.
                    var value = elem && elem.value; // null
                    ```
                    
            - 함수 매개변수에 기본값을 설정할 때
                - 함수를 호출할 때 인수를 전달하지 않으면 매개변수에는 undefined가 할당된다.
                    
                    ```jsx
                     function getStringLength(str){
                    		str = str || '';
                    		return str.length;
                    	}
                    
                    getStringLength(); // 0
                    getStringLength("hi"); // 2
                    
                    // ES6의 매개변수 기본값 설정
                    function getStringLength(str = ''){
                    		return str.length;
                     }
                    
                    getStringLength(); // 0
                    getStringLength("hi"); // 2
                    ```
                    
            
    - 옵셔널 체이닝 연산자( ?. )
        - 좌항의 피연산자가 null 또는 undefined인 경우 undefined 를 반환하고, 그렇지 않으면 우항의 프로퍼티 참조를 이어간다.
            
            ```jsx
            var elem = null;
            
            var value = elem?.value;
            console.log(value); // undefined
            ```
            
        - 논리 연산자 && 는 좌항 피연산자가 false로 평가되는 Falsy 값이면 좌항 피연산자를 그대로 반환한다. 하지만 0 이나 ‘’은 객체로 평가될 때도 있다.
        옵셔널 체이닝 연산자는 좌항 피연산자가 false 로 평가되는 Falsy값이어도 null 또는 undefined가 아니면 우항의 프로퍼티 참조를 이어간다.
            
            ```jsx
            var str ='';
            
            var length = str && str.length;
            // 문자열의 길이를 참조하지 못한다.
            console.log(length); // ''
            
            var length1 = str?.length;
            console.log(length1); // 0
            ```
            
    - null 병합 연산자
        - ES11에서 도입된 null 병합 연산자 `??` 는 좌항의 피연산자가 null 또는 undefined인 경우 우항의 피연산자를 반환하고, 그렇지 않으면 좌항의 피연산자를 반환한다.
            
            ```jsx
            var foo = null ?? 'default string';
            console.log(foo); // 'defalut string';
            ```
            
        - 논리합 연산자를 이용한 단축평가 시 좌항의 피연산자가 Falsy 값이면 예기치 못한 동작이 발생할 수 있다.
            
            ```jsx
            var foo = '' || 'default string';
            console.log(foo); // 'default string'
            
            // 그래서 null 병합 연산자를 사용하자.
            var foo = '' ?? 'default string';
            console.log(foo); // ""
            ```