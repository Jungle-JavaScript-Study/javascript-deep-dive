1. `this`란 무엇인가?
    <details>
    <summary>정답</summary>
    
    객체의 프로퍼티나 메서드를 참조하기 위해 자신이나 자신이 생성할 인스턴스를 가리키는 자기 참조 변수
    
    </details>

3. `this`를 생성하는 건 누구인가? 함수 내부에서는 어떻게 전달받는가?
    <details>
    <summary>정답</summary>
      
    자바스크립트 엔진에 의해 암묵적으로 생성되고 함수 호출할 때 암묵적으로 전달됨
        
    </details>
        
    
4. `this` 바인딩이 결정되는 시점은 언제인가?
    <details>
    <summary>정답</summary>
    
    함수 객체가 생성될 때가 아니라 함수 호출 시점에 결정됨
    
    </details>
          
    
5. `this`에 바인딩되는 값은 어떻게 결정되는가?
    <details>
    <summary>정답</summary>
    
     함수 호출 방식에 따라 동적으로 결정됨

    </details>
   <details>
    <summary>꼬리 질문</summary>
    
    this에 바인딩되는 값을 함수 호출 방식에 따라 4가지로 분류하여 설명하시오.

   <details>
   <summary>힌트</summary>
    
    일반 함수 호출, 메서드 호출, 생성자 함수 호출, 간접 호출
    
    </details>

    <details>
    <summary>정답</summary>
    
    ![image](https://github.com/Jungle-JavaScript-Study/JavaScript/assets/70076564/0cfbd56f-f70e-4f53-a781-39bc628027d7)
       
    </details>
    
    </details>

    
7. 전역에서 `this`가 호출되었을 때 바인딩되는 값을 2가지 말하시오.
    <details>
    <summary>정답</summary>

    strict mode가 적용되었을 때는 `undefined`, 아닐 때는전역 객체(브라우저에서는 `window`, Node.js에서는 `undefined`)

    </details>
        
8. 다음 코드에서 출력되는 값과 그 이유를 설명하시오.
    
    ```javascript
    // 1번
    var value = 1; 
    
    const obj = {
    	value: 2,
    	foo() {
    		console.log("1:", this); 
    
    		setTimeout(function () {
    			console.log("2:", this); 
    			console.log("3:", this.value); 
    		}, 100);
    	}
    };
    obj.foo();
    ```
    
    ```jsx
    // 2번
    var value = 1;
    
    const obj = {
    	value: 2,
    	foo() {
    		console.log("1:", this); 
    		console.log("2:", this.value);
    
    	function bar() {
    		console.log("3:", this);
    		console.log("4:", this.value);
    		bar();
    	}
    };
    
    obj.foo();
    ```
    
    <details>
    <summary>정답</summary>

    콜백함수, 중첩함수도 일반 함수로 호출되면 전역 객체가 바인딩된다.
        
    ```jsx
    //1번
    1: {value: 2, foo: *f*}
    2: window
    3: 1
    
    //2번
    1: {value: 2, foo: *f*}
    2: 2
    3: window
    4: 1
    ```
   
    </details>

    <details>
    <summary>꼬리 질문</summary>

    중첩 함수/콜백 함수에서의 `this`를 메서드의 `this`와 일치시키는 방법을 세가지 설명하시오. 

    <details>
    <summary>정답</summary>

    1. `this`를 객체 내에서 변수에 할당해서 사용
                
        ```jsx
        const obj = {
          value: 2,
          const that = this;
          setTimeout(function () {
          console.log(that.value);
          },100)
        }
        ```
        
    2. `function.apply/call/bind`로 명시적 바인딩
        
        ```jsx
        const obj = {
          value: 100,
          setTimeout(function () {
            console.log(this.value);
          }.bind(this),100)
        }
        ```
        
    3. 화살표 함수 내부의 `this`는 상위 스코프의 `this`
        
        ```jsx
        const obj = {
          value: 100,
          setTimeout(() => {
            console.log(this.value);
          },100)
        }
        ```

    </details>

    </details>
    
8. ECMAScript 사양에서 소스코드를 구분하는 4가지 타입을 설명하시오.
    <details>
    <summary>정답</summary>

    ![image](https://github.com/Jungle-JavaScript-Study/JavaScript/assets/70076564/d4626f3e-14d6-4fde-adf6-948823b160d2)

    </details>   
    
10. 소스코드의 실행 과정을 평가와 실행으로 나누어 설명하시오
    <details>
    <summary>정답</summary>

     코드 평가 (실행 컨텍스트 생성 → 선언문 평가해서 (실행 컨텍스트가 관리하는) 스코프에 등록) + 런타임 시작(코드 실행)(변수를 스코프에서 참조 → 실행 결과를 스코프에 등록)

    </details>

12. 실행 컨텍스트란?
    <details>
    <summary>정답</summary>

    소스코드를 실행하는데 필요한 환경을 제공하고 실행 결과를 관리하는 영역, 렉시컬 환경(식별자 관리하는 스코프) + 실행 컨텍스트 스택(코드 실행 순서 관리)로 구성됨

    </details>
        
13. 실행 컨텍스트는 어떤 구조로 관리되는가? 함수의 호출을 예로 들어 설명하시오.
    <details>
    <summary>정답</summary>

    스택, 코드가 실행될 때 해당 코드의 실행 컨텍스트를 실행 컨텍스트 스택에 저장해두고 함수가 호출되면 해당 함수의 실행 컨텍스트를 그 위로 쌓는다. 함수의 실행이 종료되면 해당 실행 컨텍스트를 스택에서 팝한다.

    </details>
        
14. 렉시컬 환경을 구성하는 두가지 컴포넌트에 대해 설명하시오
    <details>
    <summary>정답</summary>

     환경 레코드 - 식별자등록&바인딩된 값 관리<br>
     외부 렉시컬 환경에 대한 참조 - 상위 스코프를 가리킴. 이를 통해 스코프 체인 구현. 
        
    </details>

15. ``if``문 내에서 `let`으로 변수를 선언했을 때의 렉시컬 환경의 변화를 설명하시오.
    <details>
    <summary>정답</summary>

     `let`, `const`로 선언한 변수는 블록 레벨 스코프를 따르기 때문에 함수뿐만 아니라 반복문, try-catch문 등의 코드 블록도 지역  스코프로 인정한다. <br>
     `if`문의 코드 블록이 실행되면 블록 레벨 스코프 생성을 위해 선언적 환경 레코드를 갖는 렉시컬 환경을 생성해서 기존의 전역 렉시컬 환경을 교체한다. 이때 새롭게 생성된 렉시컬 환경의 외부 렉시컬 환경에 대한 참조는 if문의 실행되기 이전의 전역 렉시컬 환경을 가리킨다. `if`문 실행이 종료되면 `if`문이 실행되기 전의 렉시컬 환경으로 되돌린다.

    </details>
