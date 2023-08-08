### CH. 31 RegExp

- 정규 표현식 (Regular Expression)
    - **정규 표현식은 일정하나 패턴을 가진 문자열의 집합을 표현하기 위해 사용하는 형식 언어(formal language)다.**
    - 정규 표현식은 자바스크립트 고유의 언어가 아니며, 대부분의 프로그래밍 언어와 코드 에디터에 내장되어 있다.
    ( 자바스크립트는 펄(Perl)의 정규 표현식 문법을 ES3부터 도입했다. )
    - **정규 표현식은 문자열을 대상으로 패턴 매칭 기능**을 제공한다.
    ( 특정 패턴과 일치하는 문자열을 검색하거나 추출 또는 치환할 수 있다. )
- 정규 표현식의 생성
    - 정규 표현식 객체는 정규 표현식 리터럴과 RegExp 생성자 함수를 사용해 생성할 수 있다.
        
        ![정규표현식은 패턴과 플래그로 구성된다.](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bac57bd0-b6f4-4fd4-a8b3-9470ebe8b89a/Untitled.png)
        
        정규표현식은 패턴과 플래그로 구성된다.
        
        ```jsx
        const target = 'Is this all there is?';
        
        // 패턴: is
        // 플래그: i => 대소문자를 구별하지 않고 검색한다.
        const regexp = /is/i;
        
        // test 메서드는 target 문자열에 대해 정규표현식 regexp의 패턴을 검색하여 매칭 결과를 불리언 값으로 반환한다.
        regexp.test(target); // -> true
        
        // RegExp 생성자 함수를 사용하여 RegExp 객체를 생성할 수도 있다.
        const target = 'Is this all there is?';
        
        const regexp = new RegExp(/is/i); // ES6
        // const regexp = new RegExp(/is/, 'i');
        // const regexp = new RegExp('is', 'i');
        
        regexp.test(target); // -> true
        ```
        
- RegExp 메서드
    - RegExp.prototype.exec
        - 인수로 전달받은 문자열에 대해 정규 표현식의 패턴을 검색하여 매칭 결과를 배열로 반환한다.
        ( 매칭 결과가 없는 경우 null 을 반환한다. )
        ( 문자열 내의 모든 패턴을 검색하는 g 플래그를 지정해도 첫 번째 매칭 결과만 반환한다. )
            
            ```jsx
            const target = 'Is this all there is?';
            const regExp = /is/;
            
            regExp.exec(target); // -> ["is", index: 5, input: "Is this all there is?", groups: undefined]
            ```
            
    - RegExp.prototype.test
        - 인수로 전달받은 문자열에 대해 정규 표현식의 패턴을 검색하여 매칭 결과를 불리언 값으로 반환한다.
            
            ```jsx
            const target = 'Is this all there is?';
            const regExp = /is/;
            
            regExp.test(target); // -> true
            ```
            
    - String.prototype.match
        - String 표준 빌트인 객체가 제공하는 match 메서드는 대상 문자열과 인수로 전달받은 정규 표현식과의 매칭 결과를 배열로 반환한다.
            
            ```jsx
            const target = 'Is this all there is?';
            const regExp = /is/;
            
            target.match(regExp); // -> ["is", index: 5, input: "Is this all there is?", groups: undefined]
            
            // String.prototype.match 메서드는 g 플래그가 지정되면 모든 매칭 결과를 배열로 반환한다.
            const target = 'Is this all there is?';
            const regExp = /is/g;
            
            target.match(regExp); // -> ["is", "is"]
            ```
            
- 플래그
    - 패턴과 함께 정규 표현식을 구성하는 플래그는 **정규 표현식의 검색 방식을 설정하기 위해 사용한다.**
    - 플래그는 옵션이므로 선택적으로 사용할 수 있으며, 순서와 상관없이 하나 이상의 플래그를 동시에 설정할 수도 있다.
    - 어떠한 플래그를 사용하지 않은 경우 대소문자를 구별해서 패턴을 검색한다.
    - 그리고 문자열에 패턴 검색 매칭 대상이 1개 이상 존재해도 첫 번째 매칭한 대상만 검색하고 종료한다.
    
    | 플래그 | 의미 | 설명 |
    | --- | --- | --- |
    | i | Ignore case | 대소문자를 구별하지 않고 패턴을 검색한다. |
    | g | Global | 대상 문자열 내에서 패턴과 일치하는 모든 문자열을 전역 검색한다. |
    | m | Multi line | 문자열의 행이 바뀌더라도 패턴 검색을 계속한다. |
    | u | Unicode | 패턴이 유니코드 문자 시퀀스로 처리되도록 한다. |
    | y | Sticky | 대상 문자열의 ‘lastIndex’에서만 검색을 시작한다.
    ( 특정 위치에서 일치하는 항목을 찾을 때 유용하다. ) |
    | s | DotAll | 일반적으로 . 문자는 줄바꿈 문자를 제외한 모든 문자와 일치하지만,
    s 플래그가 있는 경우 . 문자는 줄바꿈 문자를 포함한 모든 문자와 일치하게 된다. |
- 패턴
    - 정규 표현식은 “일정한 규칙(패턴)을 가진 문자열의 집합을 표현하기 위해 사용하는 형식 언어다.
    - 패턴은 /로 열고 닫으며 문자열의 따옴표는 생략한다.
    ( 따옴표를 포함하면 따옴표까지도 패턴에 포함되어 검색된다. )
    - 문자열 검색
        - 정규 표현식의 패턴에 문자 또는 문자열을 지정하면 검색 대상 문자열에서 패턴으로 지정한 문자 또는 문자열을 검색한다.
        RegExp 메서드를 사용하여 검색 대상 문자열과 정규 표현식의 매칭 결과를 구하면 검색이 수행된다.
            
            ```jsx
            const target = 'Is this all there is?';
            
            // 'is' 문자열과 매치하는 패턴. 플래그가 생략되었으므로 대소문자를 구별한다.
            const regExp = /is/;
            
            // target과 정규 표현식이 매치하는지 테스트한다.
            regExp.test(target); // -> true
            
            // target과 정규 표현식의 매칭 결과를 구한다.
            target.match(regExp);
            // -> ["is", index: 5, input: "Is this all there is?", groups: undefined]
            
            const target = 'Is this all there is?';
            
            // 'is' 문자열과 매치하는 패턴. 플래그 i를 추가하면 대소문자를 구별하지 않는다.
            const regExp = /is/i;
            
            target.match(regExp);
            // -> ["Is", index: 0, input: "Is this all there is?", groups: undefined]
            
            const target = 'Is this all there is?';
            
            // 'is' 문자열과 매치하는 패턴.
            // 플래그 g를 추가하면 대상 문자열 내에서 패턴과 일치하는 모든 문자열을 전역 검색한다.
            const regExp = /is/ig;
            
            target.match(regExp); // -> ["Is", "is", "is"]
            ```
            
    - 임의의 문자열 검색
        - . 은 임의의 문자 한 개를 의미한다. 
        문자의 내용은 무엇이든 상관 없다
            
            ```jsx
            const target = 'Is this all there is?';
            
            // 임의의 3자리 문자열을 대소문자를 구별하여 전역 검색한다.
            const regExp = /.../g;
            
            target.match(regExp); // -> ["Is ", "thi", "s a", "ll ", "the", "re ", "is?"]
            ```
            
    - 반복 검색
        - {m,n}은 앞선 패턴이 최소 m번, 최대 n번 반복되는 문자열을 의미한다.
        콤마 뒤에 공백이 있으면 정상 동작하지 않는다.
            
            ```jsx
            const target = 'A AA B BB Aa Bb AAA';
            
            // 'A'가 최소 1번, 최대 2번 반복되는 문자열을 전역 검색한다.
            const regExp = /A{1,2}/g;
            
            target.match(regExp); // -> ["A", "AA", "A", "AA", "A"]
            
            // {n}은 앞선 패턴이 n번 반복되는 문자열을 의미한다. ( 즉, {n}은 {n,n}과 같다. )
            const target = 'A AA B BB Aa Bb AAA';
            
            // 'A'가 2번 반복되는 문자열을 전역 검색한다.
            const regExp = /A{2}/g;
            
            target.match(regExp); // -> ["AA", "AA"]
            
            // {n,}은 앞선 패턴이 최소 n번 이상 반복되는 문자열을 의미한다.
            const target = 'A AA B BB Aa Bb AAA';
            
            // 'A'가 최소 2번 이상 반복되는 문자열을 전역 검색한다.
            const regExp = /A{2,}/g;
            
            target.match(regExp); // -> ["AA", "AAA"]
            
            // +는 앞선 패턴이 최소 한번 이상 반복되는 문자열을 의미한다. ( 즉, + 는 {1,}과 같다. )
            const target = 'A AA B BB Aa Bb AAA';
            
            // 'A'가 최소 한 번 이상 반복되는 문자열('A, 'AA', 'AAA', ...)을 전역 검색한다.
            const regExp = /A+/g;
            
            target.match(regExp); // -> ["A", "AA", "A", "AAA"]
            
            // ?는 앞선 패턴이 최대 한 번(0번 포함) 이상 반복되는 문자열을 의미한다. ( 즉, ?는 {0,1}과 같다. )
            const target = 'color colour';
            
            // 'colo' 다음 'u'가 최대 한 번(0번 포함) 이상 반복되고 'r'이 이어지는 문자열 'color', 'colour'를 전역 검색한다.
            const regExp = /colou?r/g;
            
            target.match(regExp); // -> ["color", "colour"]
            ```
            
    - OR 검색
        - |는 or의 의미를 갖는다.
            
            ```jsx
            const target = 'A AA B BB Aa Bb';
            
            // 'A' 또는 'B'를 전역 검색한다.
            const regExp = /A|B/g;
            
            target.match(regExp); // -> ["A", "A", "A", "B", "B", "B", "A", "B"]
            
            // 분해되지 않은 단어 레벨로 검색하기 위해서는 +와 함께 사용한다.
            const target = 'A AA B BB Aa Bb';
            
            // 'A' 또는 'B'가 한 번 이상 반복되는 문자열을 전역 검색한다.
            // 'A', 'AA', 'AAA', ... 또는 'B', 'BB', 'BBB', ...
            const regExp = /A+|B+/g;
            
            target.match(regExp); // -> ["A", "AA", "B", "BB", "A", "B"]
            
            // 범위를 지정하려면 []내에 -를 사용한다.
            const target = 'A AA BB ZZ Aa Bb';
            
            // 'A' ~ 'Z'가 한 번 이상 반복되는 문자열을 전역 검색한다.
            // 'A', 'AA', 'AAA', ... 또는 'B', 'BB', 'BBB', ... ~ 또는 'Z', 'ZZ', 'ZZZ', ...
            const regExp = /[A-Z]+/g;
            
            target.match(regExp); // -> ["A", "AA", "BB", "ZZ", "A", "B"]
            
            // 대소문자를 구별하지 않고 검색하는 방법
            const target = 'AA BB Aa Bb 12';
            
            // 'A' ~ 'Z' 또는 'a' ~ 'z'가 한 번 이상 반복되는 문자열을 전역 검색한다.
            const regExp = /[A-Za-z]+/g;
            
            target.match(regExp); // -> ["AA", "BB", "Aa", "Bb"]
            
            // 숫자를 검색하는 방법
            const target = 'AA BB 12,345';
            
            // '0' ~ '9'가 한 번 이상 반복되는 문자열을 전역 검색한다.
            const regExp = /[0-9]+/g;
            
            target.match(regExp); // -> ["12", "345"]
            ```
            
            - \d는 숫자를 의미한다. 
            ( 즉, \d는 [0-9]와 같다. )
            - \D는 숫자가 아닌 문자를 의미한다.
            - \w는 알파벳, 숫자, 언더스코어를 의미한다.
            ( 즉, \w는 [A-Za-z0-9]와 같다. )
            - \W는 알파벳, 숫자, 언더스코어가 아닌 문자를 의미한다.
            
            ```jsx
            const target = 'AA BB 12,345';
            
            // '0' ~ '9' 또는 ','가 한 번 이상 반복되는 문자열을 전역 검색한다.
            let regExp = /[\d,]+/g;
            
            target.match(regExp); // -> ["12,345"]
            
            // '0' ~ '9'가 아닌 문자(숫자가 아닌 문자) 또는 ','가 한 번 이상 반복되는 문자열을 전역 검색한다.
            regExp = /[\D,]+/g;
            
            target.match(regExp); // -> ["AA BB ", ","]
            
            const target = 'Aa Bb 12,345 _$%&';
            
            // 알파벳, 숫자, 언더스코어, ','가 한 번 이상 반복되는 문자열을 전역 검색한다.
            let regExp = /[\w,]+/g;
            
            target.match(regExp); // -> ["Aa", "Bb", "12,345", "_"]
            
            // 알파벳, 숫자, 언더스코어가 아닌 문자 또는 ','가 한 번 이상 반복되는 문자열을 전역 검색한다.
            regExp = /[\W,]+/g;
            
            target.match(regExp); // -> [" ", " ", ",", " ", "$%&"]
            ```
            
    - NOT 검색
        - [ … ] 내의 ^은 not의 의미를 갖는다.
            
            ```jsx
            const target = 'AA BB 12 Aa Bb';
            
            // 숫자를 제외한 문자열을 전역 검색한다.
            const regExp = /[^0-9]+/g;
            
            target.match(regExp); // -> ["AA BB ", " Aa Bb"]
            ```
            
    - 시작 위치로 검색
        - [ … ] 밖의 ^은 문자열의 시작을 의미한다.
            
            ```jsx
            const target = 'https://poiemaweb.com';
            
            // 'https'로 시작하는지 검사한다.
            const regExp = /^https/;
            
            regExp.test(target); // -> true
            ```
            
    - 마지막 위치로 검색
        - $는 문자열의 마지막을 의미한다.
            
            ```jsx
            const target = 'https://poiemaweb.com';
            
            // 'com'으로 끝나는지 검사한다.
            const regExp = /com$/;
            
            regExp.test(target); // -> true
            ```
            
- 자주 사용하는 정규표현식
    - 특정 단어로 시작하는지 검사
        
        ```jsx
        const url = 'https://example.com';
        
        // 'http://' 또는 'https://'로 시작하는지 검사한다.
        /^https?:\/\//.test(url); // -> true
        
        /^(http|https):\/\//.test(url); // -> true
        ```
        
    - 특정 단어로 끝나는지 검사
        
        ```jsx
        const fileName = 'index.html';
        
        // 'html'로 끝나는지 검사한다.
        /html$/.test(fileName); // -> true
        ```
        
    - 숫자로만 이루어진 문자열인지 검사
        
        ```jsx
        const target = '12345';
        
        // 숫자로만 이루어진 문자열인지 검사한다.
        /^\d+$/.test(target); // -> true
        ```
        
    - 하나 이상의 공백으로 시작하는지 검사
        - \s는 여러 가지 공백 문자(스페이스, 탭 등)을 의미한다.
        ( 즉, \s는 [\t\r\n\v\f] 와 같은 의미다. )
        
        ```jsx
        const target = ' Hi!';
        
        // 하나 이상의 공백으로 시작하는지 검사한다.
        /^[\s]+/.test(target); // -> true
        ```
        
    - 아이디로 사용 가능한지 검사
        
        ```jsx
        const id = 'abc123';
        
        // 알파벳 대소문자 또는 숫자로 시작하고 끝나며 4 ~ 10자리인지 검사한다.
        /^[A-Za-z0-9]{4,10}$/.test(id); // -> true
        ```
        
    - 메일 주소 형식에 맞는지 검사
        
        ```jsx
        const email = 'ungmo2@gmail.com';
        
        /^[0-9a-zA-Z]([-_\.]?[0-9a-zA-Z])*@[0-9a-zA-Z]([-_\.]?[0-9a-zA-Z])*\.[a-zA-Z]{2,3}$/.test(email); // -> true
        
        // [인터넷 메시지 형식 규약인 RFC 5322](https://www.emailregex.com/) 에 맞는 정교한 패턴 매칭이 필요하다면 다음과 같은 복잡한 패턴을 사용할 필요가 있다.
        (?:[a-z0-9!#$%&'*+/=?^_`{|}~-]+(?:\.[a-z0-9!#$%&'*+/=?^_`{|}~-]+)*|"(?:[\x01-\x08\x0b\x0c\x0e-\x1f\x21\x23-\x5b\x5d-\x7f]|\\[\x01-\x09\x0b\x0c\x0e-\x7f])*")@(?:(?:[a-z0-9](?:[a-z0-9-]*[a-z0-9])?\.)+[a-z0-9](?:[a-z0-9-]*[a-z0-9])?|\[(?:(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.){3}(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?|[a-z0-9-]*[a-z0-9]:(?:[\x01-\x08\x0b\x0c\x0e-\x1f\x21-\x5a\x53-\x7f]|\\[\x01-\x09\x0b\x0c\x0e-\x7f])+)\])
        ```
        
    - 핸드폰 번호 형식에 맞는지 검사
        
        ```jsx
        const cellphone = '010-1234-5678';
        
        /^\d{3}-\d{3,4}-\d{4}$/.test(cellphone); // -> true
        ```
        
    - 특수 문자 포함 여부 검사
        
        ```jsx
        const target = 'abc#123';
        
        // A-Za-z0-9 이외의 문자가 있는지 검사한다. 특수문자는 A-Za-z0-9 이외의 문자다.
        (/[^A-Za-z0-9]/gi).test(target); // -> true
        
        // 다음 방식으로 대체해 사용할 수도 있다.
        (/[\{\}\[\]\/?.,;:|\)*~`!^\-_+<>@\#$%&\\\=\(\'\"]/gi).test(target); // -> true
        
        // 특수 문자를 제거한다.
        target.replace(/[^A-Za-z0-9]/gi, ''); // -> abc123
        ```