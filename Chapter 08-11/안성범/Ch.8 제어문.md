### CH. 8 제어문

- 제어문은 조건에 따라 코드 블록을 실행(조건문)하거나 반복 실행(반복문)할 때 사용한다.
- 블록문
    - 블록문은 0개 이상의 문을 중괄호로 묶은 것 ( 코드 블록 or 블록이라고 부르기도 함 )
    - 자바스크립트는 블록문을 하나의 실행 단위로 취급한다. ( 블록문은 단독으로 사용할 수도 있으나 일반적으로 제어문이나 함수를 정의할 때 사용한다.)
- 조건문
    - 조건문은 주어진 조건식의 평가 결과에 따라 코드 블록(블록문)의 실행을 결정한다.
    - 조건식은 불리언 값으로 평가될 수 있는 표현식이다.
    - if … else 문
        - if … else 문은 주어진 조건식(불리언 값으로 평가될 수 있는 표현식)의 평가 결과, 즉 논리적 참 or 거짓에 따라 실행할 코드 블록을 결정한다.
            
            ```jsx
            if (조건식) {
            	// 조건식이 참이면 이 코드 블록이 실행된다.
            } else {
            	// 조건식이 거짓이면 이 코드 블록이 실행된다.
            }
            ```
            
        - if 문의 조건식은 불리언 값으로 평가되어야 한다.
        만약 if 문의 조건식이 불리언 값이 아닌 값으로 평가되면 자바스크립트 엔진에 의해 암묵적으로 불리언 값으로 강제 변환되어 실행할 코드 블록을 결정한다.
        
        ```jsx
        if (조건식1) {
        	// 조건식 1 이 참이면 이 코드 블록이 실행된다.
        } else if (조건식2) {
        	// 조건식 2 가 참이면 이 코드 블록이 실행된다.
        	} else {
        	// 조건식 1과 2가 모두 거짓이면 이 코드 블록이 실행된다.
        }
        ```
        
        - 만약 코드 블록 내의 문이 하나뿐이라면 중괄호를 생략할 수 있다.
        - 대부분의 if … else 문은 삼항 조건 연산자로 바꿔 쓸 수 있다.
        삼항 조건 연산자는 값으로 평가되는 표현식을 만든다. → 삼항 조건 연산자 표현식은 값처럼 사용할 수 있기 때문에 변수에 할당할 수 있다.
            
            ```jsx
            var num = 2;
            
            var kind = num ? (num > 0 ? '양수' : '음수' ) : '영';
            
            console.log(kind); // 양수
            ```
            
    - switch 문
        - switch 문은 주어진 표현식을 평가하여 그 값과 일치하는 표현식을 갖는 case 문으로 실행 흐름을 옮긴다.
        - case 문은 상황을 의미하는 표현식을 저장하고 콜론으로 마친다.
        그리고 그 뒤에 실행할 문들을 위치시킨다.
        - switch 문의 표현식과 일치하는 case 문이 없다면 실행 순서는 default문으로 이동한다.
        
        ```jsx
        switch (표현식) {
        	case 표현식1:
        		switch 문의 표현식과 표현식1이 일치하면 실행될 문;
        		break;
        	case 표현식2:
        		switch 문의 표현식과 표현식2가 일치하면 실행될 문;
        		break;
        	default:
        		switch 문의 표현식과 일치하는 case 문이 없을 때 실행될 문;
        }
        ```
        
        - if … else 문의 조건식은 불리언 값으로 평가되어야 하지만, switch 문의 표현식은 불리언 값보다는 문자열이나 숫자인 경우가 많다.
        
        ```jsx
        var month = 11;
        var monthName;
        
        switch (month) {
        case 1: monthName = 'January';
        case 2: monthName = 'February';
        case 3: monthName = 'March';
        case 4: monthName = 'April';
        case 5: monthName = 'May';
        case 6: monthName = 'June';
        case 7: monthName = 'July';
        case 8: monthName = 'August';
        case 9: monthName = 'September';
        case 10: monthName = 'October';
        case 11: monthName = 'November';
        case 12: monthName = 'December';
        default: monthName = 'Invalid month';
        }
        
        console.log(monthName); // Invalid month
        ```
        
        - 이는 switch 문의 표현식의 평가 결과와 일치하는 case 문으로 실행 흐름이 이동하여 문을 실행한 것은 맞지만 문을 실행한 후 switch 문을 탈출하지 않고 switch 문이 끝날 때까지 이후의 모든 case 문과 default 문을 실행했기 때문이다. - 폴스루(fall through)
        - case 문에 해당하는 문의 마지막에 break 문을 사용하지 않았기 때문이다.
        break 키워드로 구성된 break 문은 코드 블록에서 탈출하는 역할을 한다.
        break 문이 없다면 case 문의 표현식과 일치하지 않더라도 실행 흐름이 다음 case 문으로 연이어 이동한다.
        - default 문에는 break 문을 생략하는 것이 일반적이다.
        - **조건식이 너무 많아서** if … else 문보다 switch 문을 사용했을 때 가독성이 더 좋다면 switch 문을 사용하는 편이 좋다.
    - 반복문
        - 반복문은 조건식의 평가 결과가 참인 경우 코드 블록을 실행한다.
        - 자바스크립트는 for 문, while 문, do … while 문을 제공한다.
            - 자바스크립트는 배열을 순회할 때 사용하는 forEach 메서드, 
            객체의 프로퍼티를 열거할 때 사용하는 for … in 문, 
            ES6 에서 도입된 이터러블을 순회할 수 있는 for … of 문
            과 같이 **반복문을 대체할 수 있는 다양한 기능을 제공**한다.
        - for 문
            - for 문은 조건식이 거짓으로 평가될 때까지 코드 블록을 반복 실행한다.
            
            ```jsx
            for (변수 선언문 또는 할당문; 조건식; 증감식) {
            	조건식이 참인 경우 반복 실행될 문;
            }
            ```
            
            - for 문의 변수 선언문, 조건식, 증감식은 모두 옵션이므로 반드시 사용할 필요는 없다. 단, 어떤 식도 선언하지 않으면 무한루프가 된다.
            - for 문 내에 for 문을 중첩해 쓸 수 있다 (다중 for문)
        - while 문
            - while 문은 주어진 조건식의 평가 결과가 참이면 코드 블록을 계속해서 반복 실행한다.
            - for 문은 반복 횟수가 명확할 때 주로 사용하고 while 문은 반복 횟수가 불명확할 때 주로 사용한다.
        - do … while 문
            - do … while 문은 코드 블록을 먼저 실행하고 조건식을 평가한다.
            따라서 **코드 블록은 무조건 한 번 이상 실행**된다.
        - break 문
            - break 문은 코드 블록을 탈출한다.
            조금 더 자세히는 **레이블 문, 반복문(for, for … in, for … of, while, do … while) 또는 switch 문의 코드 블록을 탈출**한다.
            - 중첩된 for 문의 내부 for 문에서 break 문을 실행하면 내부 for 문을 탈출하여 외부 for 문으로 진입한다.
            이 때 내부 for 문이 아닌 외부 for 문을 탈출하려면 레이블 문을 사용한다.
            
            ```jsx
            // outer 라는 식별자가 붙은 레이블 for 문
            outer: for (var i = 0; i < 3; i ++) {
            	for (var j = 0; j < 3; j++) {
            		// i + j === 3 이면 outer 라는 식별자가 붙은 레이블 for 문을 탈출한다.
            		if (i + j === 3) break outer;
            		console.log(`inner [${i}, ${j}]`);
            	}
            }
            
            console.log('Done!');
            ```
            
            - **레이블문은 중첩된 for 문 외부로 탈출할 때 유용**하지만 그 밖의 경우에는 일반적으로 권장하지 않는다.
        - Continue 문
            - continue 문은 반복문의 코드 블록 실행을 현 지점에서 중단하고 반복문의 증감식으로 실행 흐름을 이동시킨다.
            break 문처럼 반복문을 탈출하지는 않는다.
            - if 문 내에서 실행해야 할 코드가 한 줄이라면 continue 문을 사용했을 때 보다 간편하고 가독성도 좋다.