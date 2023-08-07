### CH. 28 Number

- Number 생성자 함수
    - Number : 표준 빌트인 객체로, 원시 타입인 숫자를 다룰 때 유용한 프로퍼티와 메서드를 제공한다.
    - Number 생성자 함수에 인수를 전달하지 않고 new 연산자와 함께 호출하면 [[NumberData]] 내부 슬롯에 0을 할당한 Number 래퍼 객체를 생성한다.
    인수로 숫자가 아닌 값을 전달하면 인수를 숫자로 강제 변한한 후 생성한다.
    숫자로 변환할 수 없다면 NaN을 할당해 Number 객체를 생성한다.
    - new 연산자를 사용하지 않고 Number 생성자 함수를 호출하면 Number 인스턴스가 아닌 숫자를 반환한다.
        
        ```jsx
        let numObj = new Number('10');
        console.log(numObj); // Number {[[PrimitiveValue]]: 10}
        
        numObj = new Number('Hello');
        console.log(numObj); // Number {[[PrimitiveValue]]: NaN}
        
        // 문자열 타입 => 숫자 타입
        Number('0');     // -> 0
        Number('-1');    // -> -1
        Number('10.53'); // -> 10.53
        
        // 불리언 타입 => 숫자 타입
        Number(true);  // -> 1
        Number(false); // -> 0
        ```
        
- Number 프로퍼티
    - Number.EPSILON
        - Number.EPSILON 은 1과 1보다 큰 숫자 중에서 가장 작은 숫자와의 차이(2.2204460492503130808472633361916 * 10^-16)
        - 부동소수점으로 인해 발생하는 오차를 해결하기 위해 사용한다.
            
            ```jsx
            function isEqual(a, b){
              // a와 b를 뺀 값의 절대값이 Number.EPSILON보다 작으면 같은 수로 인정한다.
              return Math.abs(a - b) < Number.EPSILON;
            }
            
            isEqual(0.1 + 0.2, 0.3); // -> true
            ```
            
    - Number.MAX_VALUE
        - 자바스크립트에서 표현할 수 있는 가장 큰 양수 값
        (1.7976931348623157 * 10^308)
        - Number.MAX_VALUE 보다 큰 숫자는 Infinity 이다.
            
            ```jsx
            Number.MAX_VALUE; // -> 1.7976931348623157e+308
            Infinity > Number.MAX_VALUE; // -> true
            ```
            
    - Number.MIN_VALUE
        - 자바스크립트에서 표현할 수 있는 가장 작은 양수 값(5 * 10^-324)
        - Number.MIN_VALUE 보다 작은 숫자는 0이다.
            
            ```jsx
            Number.MIN_VALUE; // -> 5e-324
            Number.MIN_VALUE > 0; // -> true
            ```
            
    - Number.MAX_SAFE_INTEGER
        - 자바스크립트에서 안전하게 표현할 수 있는 가장 큰 정수값(9007199254740991)
    - Number.MIN_SAFE_INTEGER
        - 자바스크립트에서 안전하게 표현할 수 있는 가장 작은 정수값(-9007199254740991)
    - Number.POSITIVE_INFINITY
        - 양의 무한대를 나타내는 숫자값 INFINITY 와 같다.
    - Number.NEGATIVE_INFINITY
        - 음의 무한대를 나타내는 숫자값 -INFINITY와 같다.
    - Number.NaN
        - 숫자가 아님(Not-a-Number)를 나타내는 숫자값
- Number 메서드
    - Number.isFinite
        - 인수로 전달된 숫자값이 Infinity 인지 -Infinite 인지를 검사해 그 결과를 불리언 값으로 반환
            
            ```jsx
            // 인수가 정상적인 유한수이면 true를 반환한다.
            Number.isFinite(0);                // -> true
            Number.isFinite(Number.MAX_VALUE); // -> true
            Number.isFinite(Number.MIN_VALUE); // -> true
            
            // 인수가 무한수이면 false를 반환한다.
            Number.isFinite(Infinity);  // -> false
            Number.isFinite(-Infinity); // -> false
            
            Number.isFinite(NaN); // -> false
            
            // Number.isFinite는 인수를 숫자로 암묵적 타입 변환하지 않는다.
            Number.isFinite(null); // -> false
            
            // isFinite는 인수를 숫자로 암묵적 타입 변환한다. null은 0으로 암묵적 타입 변환된다.
            isFinite(null); // -> true
            ```
            
            <aside>
            💡 빌트인 전역 함수 isFinite 와 차이점은, 전역함수 isFinite는 전달 받은 인수를 숫자로 압묵적 타입 변환하여 검사를 수행하지만, 
            Number.isFinite는 전달받은 인수를 숫자로 암묵적 타입 변환하지 않는다.
            → 숫자가 아닌 인수가 주어졌을 때 변환값은 언제나 false
            
            </aside>
            
    - Number.isInteger
        - 인수로 전달된 숫자값이 정수인지 검사하여 그 결과를 불리언 값으로 반환
        ( 검사하기 전에 인수를 숫자로 암묵적 타입 변환하지 않는다. )
            
            ```jsx
            // 인수가 정수이면 true를 반환한다.
            Number.isInteger(0)     // -> true
            Number.isInteger(123)   // -> true
            Number.isInteger(-123)  // -> true
            
            // 0.5는 정수가 아니다.
            Number.isInteger(0.5)   // -> false
            // '123'을 숫자로 암묵적 타입 변환하지 않는다.
            Number.isInteger('123') // -> false
            // false를 숫자로 암묵적 타입 변환하지 않는다.
            Number.isInteger(false) // -> false
            // Infinity/-Infinity는 정수가 아니다.
            Number.isInteger(Infinity)  // -> false
            Number.isInteger(-Infinity) // -> false
            ```
            
    - Number.isNaN
        - 인수로 전달된 숫자값이 NaN인지 검사하여 그 결과를 불리언 값으로 반환
            
            ```jsx
            // 인수가 NaN이면 true를 반환한다.
            Number.isNaN(NaN); // -> true
            
            // Number.isNaN은 인수를 숫자로 암묵적 타입 변환하지 않는다.
            Number.isNaN(undefined); // -> false
            
            // isFinite는 인수를 숫자로 암묵적 타입 변환한다. undefined는 NaN으로 암묵적 타입 변환된다.
            isNaN(undefined); // -> true
            ```
            
            <aside>
            💡 빌트인 전역 함수 isNaN은 전달받은 인수를 숫자로 암묵적 타입 변환하여 검사를 수행하지만 Number.isNaN 메서드는 전달받은 인수를 숫자로 암묵적 타입변환하지 않는다.
            → 숫자가 아닌 인수가 주어졌을 때 반환값은 언제나 false
            
            </aside>
            
    - Number.isSafeInteger
        - 인수로 전달된 숫자값이 안전한 정수인지 검사하여 그 결과를 불리언 값으로 반환
        (  안전한 정수값 : -(2^53 - 1) ~ (2^53 - 1) 사이의 정수값 )
        - 검사 전에 인수를 숫자로 암묵적 타입 변환하지 않는다.
            
            ```jsx
            // 0은 안전한 정수이다.
            Number.isSafeInteger(0); // -> true
            // 1000000000000000은 안전한 정수이다.
            Number.isSafeInteger(1000000000000000); // -> true
            
            // 10000000000000001은 안전하지 않다.
            Number.isSafeInteger(10000000000000001); // -> false
            // 0.5은 정수가 아니다.
            Number.isSafeInteger(0.5); // -> false
            // '123'을 숫자로 암묵적 타입 변환하지 않는다.
            Number.isSafeInteger('123'); // -> false
            // false를 숫자로 암묵적 타입 변환하지 않는다.
            Number.isSafeInteger(false); // -> false
            // Infinity/-Infinity는 정수가 아니다.
            Number.isSafeInteger(Infinity); // -> false
            ```
            
    - Number.prototype.toExponential
        - 숫자를 지수 표기법으로 변환하여 문자열로 반환, 인수로 소수점 이하로 표현할 자릿수를 전달할 수 있다.
            
            ```jsx
            (77.1234).toExponential();  // -> "7.71234e+1"
            (77.1234).toExponential(4); // -> "7.7123e+1"
            (77.1234).toExponential(2); // -> "7.71e+1"
            
            // 숫자 리터럴과 함께 Number 프로토타입 메서드를 사용할 경우 에러발생
            77.toExponential(); // -> SyntaxError: Invalid or unexpected token
            
            // 숫자 리터럴과 함께 메서드를 사용할 경우 혼란을 방지하기 위해 그룹 연산자를 사용할 수 있다.
            (77).toExponential(); // -> "7.7e+1"
            
            ```
            
    - Number.prototype.toFixed
        - 숫자를 반올림하여 문자열로 반환한다. 
        반올림하는 소수점 이하 자릿수를 나타내는 0~20사이의 정수값을 인수로 전달할 수 있다.
        (인수를 생략하면 기본값 0이 지정된다.)
            
            ```jsx
            // 소수점 이하 반올림. 인수를 생략하면 기본값 0이 지정된다.
            (12345.6789).toFixed(); // -> "12346"
            // 소수점 이하 1자리수 유효, 나머지 반올림
            (12345.6789).toFixed(1); // -> "12345.7"
            // 소수점 이하 2자리수 유효, 나머지 반올림
            (12345.6789).toFixed(2); // -> "12345.68"
            // 소수점 이하 3자리수 유효, 나머지 반올림
            (12345.6789).toFixed(3); // -> "12345.679"
            ```
            
    - Number.prototype.toPrecision
        - 인수로 전달받은 전체 자릿수까지 유효하도록 나머지 자릿수를 반올림하여 문자열로 반환한다.
        인수로 전달받은 전체 자릿수로 표현할 수 없는 경우 지수 표기법으로 결과를 반환한다.
        전체 자릿수를 나타내는 0~21 사이의 정수값을 인수로 전달할 수 있다. 
        (인수를 생략하면 기본값 0이 지정된다.)
            
            ```jsx
            // 전체 자리수 유효. 인수를 전달하지 않으면 기본값 0이 전달된다.
            (12345.6789).toPrecision(); // -> "12345.6789"
            // 전체 1자리수 유효, 나머지 반올림
            (12345.6789).toPrecision(1); // -> "1e+4"
            // 전체 2자리수 유효, 나머지 반올림
            (12345.6789).toPrecision(2); // -> "1.2e+4"
            // 전체 6자리수 유효, 나머지 반올림
            (12345.6789).toPrecision(6); // -> "12345.7"
            ```
            
    - Number.prototype.toString
        - 숫자를 문자열로 변환하여 반환한다.
        진법을 나타내는 2~36 사이의 정수값을 인수로 전달할 수 있다.
        ( 인수를 생략하면 기본값 10진법이 지정된다. )
            
            ```jsx
            // 인수를 생략하면 10진수 문자열을 반환한다.
            (10).toString(); // -> "10"
            // 2진수 문자열을 반환한다.
            (16).toString(2); // -> "10000"
            // 8진수 문자열을 반환한다.
            (16).toString(8); // -> "20"
            // 16진수 문자열을 반환한다.
            (16).toString(16); // -> "10"
            ```