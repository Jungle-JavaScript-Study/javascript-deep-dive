## Ch 26~28 질문리스트

- ES6 이전과 이후의 함수는 어떻게 달라졌나요 ?
    <details>
    <summary>정답</summary>

    - ES6 이전의 모든 함수는 callable이면서 constructor 이다.
    - ES6 에서는 함수를 사용 목적에 따라 세 가지 종류로 명확히 구분했다.
    → 일반 함수는 constructor 이지만 메서드와 화살표 함수는 non-constructor 이다.
    
    </details>
    <details>
    <summary>꼬리질문</summary>

    - 어떤 문제가 생기기 때문에 함수의 종류를 구분하였나요 ?


        <details>
        <summary>정답</summary>

        - 객체에 바인딩된 함수 즉,메서드도 callable이며 constructor 이므로 prototype 프로퍼티를 가지며, 프로토타입 객체도 생성한다. 
        콜백함수도 마찬가지로 constructor 이기 때문에 불필요한 프로토타입 객체를 생성한다.  
        → 이는 혼란스러우며 실수를 유발할 가능성이 있고 성능에도 좋지 않다.

        </details>
    </details>

- 자바스크립트의 배열은 일반적인 자료구조 배열과 다른데, 어떤 점이 다른가요 ?
    <details>
    <summary>정답</summary>

    - 자료구조에서 말하는 배열은 동일한 크기의 메모리 공간이 빈틈없이 연속적으로 나열된 자료구조이지만(밀집 배열(dense array))
    - 자바스크립트에서의 배열은 사실은 객체로,
    배열의 요소를 위한 각각의 메모리 공간은 동일한 크기를 갖지 않아도 되며, 연속적으로 이어져있지 않을수도 있다.(희소 배열(sparse array))

    </details>
    <details>
    <summary>꼬리질문</summary>

    - 그러면 일반적인 배열과 자바스크립트 배열의 장단점에 대해서 말해주세요.

        <details>
        <summary>정답</summary>

        - 일반적인 배열은 인덱스로 요소에 빠르게 접근할 수 있지만, 요소를 삽입, 삭제 하는 경우에 효율적이지 않다.
        → 그래서 삽입,삭제가 많으면, 리스트를 쓰기도 한다.
        - 자바스크립트 배열은 해시테이블로 구현된 객체이므로 인덱스로 요소에 접근하는 경우 일반적인 배열보다 조금 느릴수밖에 없지만,
        요소를 삽입, 삭제 하는 경우에 일반적인 배열보다 빠르다.
        +) 여러 타입의 요소를 저장할 수 있다.

        </details>
    </details>

- 자바스크립트에서 배열을 생성하는 방법에 대해서 말해주세요.
    <details>
    <summary>정답</summary>
    
    - 배열 리터럴
    - Array 생성자 함수
    - Array.of (ES6 에서 도입)
    - Array.from (ES6 에서 도입)
    
    </details>


- 자바스크립트에서 배열의 요소를 삭제하는 방법에 대해서 설명해주세요.
    <details>
    <summary>정답</summary>
    
    - 자바스크립트의 배열은 사실 객체이기 때문에 delete 연산자를 사용해 특정 요소를 제거할 수 있습니다.  
    하지만, delete 연산자는 객체의 프로퍼티를 삭제하기 때문에, 희소 배열이 되며 length 프로퍼티 값은 변하지 않는다.  
    → 따라서 희소 배열을 만들지 않으면서 배열의 특정 요소를 완전히 삭제하려면 Array.prototype.splice 메서드를 사용하는 것이 좋습니다.
    
    </details>

- Array.prototype.sort 를 이용해 아래 코드를 정렬하면 어떤 결과가 나오나요 ?  
    왜 그런 결과가 나오나요 ?
    
    ```javascript
    const points = [40, 100, 1, 5, 2, 25, 10];
    
    points.sort();
    
    console.log(points); // ??
    ```

    <details>
    <summary>정답</summary>
    
    ```javascript
    const points = [40, 100, 1, 5, 2, 25, 10];
    
    points.sort();
    
    console.log(points); // [1, 10, 100, 2, 25, 40, 5]
    ```
        
    - sort 메서드의 기본 정렬순서는 유니코드 코드 포인트의 순서를 따르기 때문에, 
    배열의 요소가 숫자 타입이라 할지라도 배열의 요소를 일시적으로 문자열로 변환한 후 유니코드 코드 포인트의 순서를 기준으로 정렬합니다.  
    → 그래서 숫자 요소를 정렬 할 때에는 sort 메서드에 **************************************************************************정렬 순서를 정의하는 비교 함수를 인수로 전달**************************************************************************해야 합니다.  

        
    ```javascript
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
            
    
    </details>
    <details>
    <summary>꼬리질문</summary>

    - 자바스크립트의 sort는 어떤 정렬알고리즘을 사용하나요 ?

        <details>
        <summary>정답</summary>

        - ES10 이전에는 quicksort 알고리즘을 사용하였었고,   
        ES10 이후에는 timsort 알고리즘을 사용하여 정렬합니다.

        </details>


        <details>
        <summary>꼬리질문</summary>

        - 그러면 그 알고리즘에 대해서 설명해주세요.

            <details>
            <summary>정답</summary>

            - 퀵 정렬 알고리즘의 원리
                1. 배열에서 임의의 요소를 선택(pivot)
                2. 피벗을 기준으로 배열을 두 부분으로 나누어 피벗보다 작은 요소를 왼쪽, 피벗보다 큰 요소를 오른쪽으로 정렬(분할)
                3. 피벗을 제외한 왼쪽 배열과 오른쪽 배열에 대해 같은 과정 반복
                4. 모든 배열의 크기가 0이나 1일 때까지 반복
                - 시간복잡도
                    - 평균 O(n log n)
                    - 최악 O(n^2)
                    ( 이미 정렬된 배열 )
            - 팀정렬 알고리즘의 원리 ( 파이썬과 자바 기본 정렬 알고리즘 )
                - 팀소트 = 합병정렬 + 삽입정렬
                1. 작은 덩어리(run)으로 나눈다
                2. 삽입 정렬로 런 정렬
                3. 정렬된 런들을 병합
                4. 필요에 따라 다시 분할 병합
                - 시간복잡도
                    - 평균 O(n log n)
                    - 최악 O(n log n)

            </details>
        </details>
    </details>

- Number메서드 중 Number.isFinite 와 Number.isNaN이 있는 것으로 아는데, 
빌트인 전역 함수 isFinite와 isNaN 함수와의 다른점이 무엇인가요 ?
    <details>
    <summary>정답</summary>
    
    - 빌트인 전역 함수 isFinite와 isNaN 은 전달 받은 인수를 숫자로 암묵적 타입 변환하여 검사를 수행하지만,  
    Number 메서드는 전달받은 인수를 숫자로 암묵적 타입변환을 하지 않는다.
    ( 숫자가 아닌 인수가 주어졌을 때 반환값은 언제나 false 이다. )
    
    </details>