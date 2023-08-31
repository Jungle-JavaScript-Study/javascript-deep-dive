1. 호출 스케줄링이 무엇인가?
    <details>
    <summary>정답</summary>
    
    함수를 명시적으로 호출하지 않고 타이머 함수 `setTimeout`이나 `setInterval`을 이용해서 일정 시간이 지난 후 호출되도록 예약하는 방식
       
    </details>
    
1. 타이머 함수는 자바스크립트에 기본으로 탑재되어 있는 함수이다.(O/X)
    <details>
    <summary>정답</summary>
    
    X, 타이머 함수는 빌트인 함수는 아니지만 브라우저와 Nodejs 모두 전역 객체의 메서드로 제공하는 호스트 객체이다.
       
    </details>

1. 타이머 함수는 비동기로 동작하는가 동기로 동작하는가? 그 이유를 함께 설명하시오.
    <details>
    <summary>정답</summary>
    
    비동기, 자바스크립트 엔진은 싱글 스레드로 동작하기 때문에 여러개의 태스크를 동시에 실행할 수 없다.
       
    </details>

1. 타이머 함수는 전달된 시간이 지나면 즉시 콜백함수가 실행된다. (O/X)
    <details>
    <summary>정답</summary>

    X

      <details>
      <summary>꼬리 질문</summary>
      이유를 자바스크립트의 실행방식과 연관지어 설명하시오.
        
      <details>
      <summary>정답</summary>
      
      1. 타이머 함수의 4ms 이하의 지연 시간은 최소 지연 시간 4ms가 지정된다.<br>
      2. 타이머 함수에 전달되는 시간은 얼마 뒤에 태스크 큐에 콜백 함수를 등록할 것인가를 의미한다. `setTimeout`의 실행 컨텍스트가 콜 스택에 푸시되면 **자바스크립트 엔진**이 함수를 호출 스케줄링하고 콜 스택에서 팝된다.
         그 후 **브라우저**가 타이머를 설정하고, 타이머가 만료되면 콜백 함수를 **태스크 큐**에 푸시하는 것을 담당한다. 콜 스택의 함수가 전역 코드까지 모두 실행되고 나서 비게되면 **이벤트 루프**가 태스크 큐에서 대기하던 콜백함수를 콜스택에 푸시하고 이 때 실행된다.
         따라서 태스크 큐에 실행 컨텍스트가 많이 쌓여있다면 지연시간 이후 즉시 실행되지 않을 수 있다.
          [참고 - setTimeout(foo, 0)에서 foo는 정말 0ms 후에 실행될까?](https://velog.io/@edie_ko/javascript-eventloop)

      </details>
         
      </details>
       
    </details>

1. 호출 스케줄링을 취소하는 방법을설명하시오.
    <details>
    <summary>정답</summary>
    
    타이머 함수는 생성된 타이머를 식별할 수 있는 고유한 타이머 `id`를 리턴한다.(브라우저에서는 숫자, nodejs에서는 객체)<br>
    이 타이머 `id`를 저장해뒀다가 `clearTimeout`에 전달하면 해당 타이머를 취소할 수 있다.
       
    </details>

1. `setTimeout`과 `setInterval`의 차이에 대해 설명하시오.
    <details>
    <summary>정답</summary>
    
    `setTimeout`은 콜백 함수를 한번만 호출하고 `setInterval`은 `clearInterval`로 타이머를 취소할 때까지 타이머가 만료될 때마다 반복적으로 호출한다.
       
    </details>

1. 당신의 웹사이트에 검색 자동완성 기능을 만들었다. 그런데 입력할 때마다 서버에 http 요청이 가서 서버에 무리가 된다는 요청이 왔다. 어떻게 최적화를 할 수 있을까?
    <details>
    <summary>정답</summary>
    
    디바운스/스로틀로 일정 시간 내에 연속해서 발생하는 이벤트는 그룹화해서 과도한 이벤트핸들러의 호출을 방지한다.

    <details>
    <summary>꼬리 질문</summary>
    
    디바운스와 스로틀의 차이와 각각 적합한 활용처에 대해 설명하시오.
    <details>
    <summary>정답</summary>
    
    - 디바운스: 일정 시간 동안 이벤트가 발생하면 이전 타이머를 취소하고, 해당 시간 내에 더 이상 이벤트가 발생하지 않을 때 마지막 한번만 호출한다.
    - 스로틀: 정해진 시간이 경과하기 전에 이벤트가 발생하면 타이머를 등록하지 않고, 경과한 후 이벤트가 발생하면 새로운 타이머를 등록해 일정 시간동안 최대 한번만 호출되도록 한다.
    - => 디바운스는 자동완성, 버튼 중복 클릭 방지, `resize` 이벤트 등 / 스로틀은 무한 스크롤 등 `scroll` 이벤트
       <img width="623" alt="image" src="https://github.com/Jungle-JavaScript-Study/deep-dive/assets/70076564/409027da-bdd9-4aca-af74-ec632579bd8a">
       <img width="611" alt="image" src="https://github.com/Jungle-JavaScript-Study/deep-dive/assets/70076564/3d2a9eac-7adc-4e92-ae84-261b0d6820a8">

    </details>
    </details>
    </details>
    
1. 자바스크립트가 싱글스레드라는게 어떤 의미인지 자세히 설명하시오.
    <details>
    <summary>정답</summary>

    자바스크립트 엔진은 하나의 실행 컨텍스트 스택(=콜 스택)만을 갖는다.
    함수가 실행되는 것은 함수 코드 평가 과정에서 생성된 함수 실행 컨텍스트가 실행 컨텍스트 스택에 푸시되는 것을 의미하는데,
    자바스크립트는 이 스택이 하나라 한번에 하나의 태스크만 실행할 수 있고 나머지 대기 중인 태스크들은 호출된 순서대로 스택에 쌓여있다가
    현재 실행하던 태스크가 종료되어 실행 컨텍스트 스택에서 팝되면 최상위의 실행 컨텍스트가 실행된다.

      <details>
      <summary>꼬리 질문</summary>
      이 때 발생하는 블로킹을 어떻게 해결할 수 있는가?
      
      <details>
      <summary>정답</summary>
      
      비동기 방식을 사용해 현재 실행 중인 태스크가 종료될때까지 다음 태스크가 대기하지 않도록 한다.
         
      </details>
         
      </details>

      <details>
      <summary>꼬리 질문</summary>
      비동기 방식은 장점만 있는가?
      
      <details>
      <summary>정답</summary>
      
      X. 비동기 방식은 실행 순서가 보장되지 않는다. 또한 비동기 함수는 일반적으로 콜백패턴을 사용하기 때문에 콜백 헬을 발생시킬 수 있다.
         
      </details>
       
    </details>

    <details>
      <summary>꼬리 질문</summary>
      자바스크립트가 싱글스레드이면 어떻게 여러 태스크를 동시에 처리하는가? 예를 들어, 애니메이션이 있는 화면에서 마우스 드래그를 한다고 해서 애니메이션이 멈추지는 않는다. 이는 어떻게 실행되는 것일까?
      
      <details>
      <summary>정답</summary>

      자바스크립트 엔진은 단순히 태스크가 요청되면 콜 스택을 통해 요청된 작업을 순차적으로 실행하는 역할만 한다.
      비동기 처리에서 소스코드의 평가와 실행을 제외한 모든 다른 처리는 자바스크립트 엔진을 구동하는 환경(브라우저 혹은 Node.js)가 담당한다.
      브라우저는 태스크 큐(=이벤트 큐, 콜백 큐)와 이벤트 루프를 제공해서 태스크 큐에 비동기 함수의 콜백함수나 이벤트 핸들러를 일시적으로 보관해두었다가
      이벤트 루프가 콜 스택과 태스크 큐를 확인해 콜 스택이 비어있고 태스크 큐에 대기중인 함수가 있다면 FIFO 방식으로 태스크 큐의 함수를 콜스택으로 이동시킨다.
      <img width="448" alt="image" src="https://github.com/Jungle-JavaScript-Study/deep-dive/assets/70076564/d1ae4e2b-90a0-404a-9c6e-04cf8baa1d5f">

      => 자바스크립트가 싱글스레드라는 것은 브라우저가 싱글스레드라는 것이 아니라 브라우저에 내장된 자바스크립트 엔진이 싱글스레드로 동작한다는 의미이다. 브라우저는 멀티 스레드로 동작하기 때문에 자바스크립트를 비동기 방식으로 실행할 수 있는 것이다.
       타이머 함수는 브라우저에서 제공하는 Web API이다. 
      </details>
      </details>
    </details>

1. Ajax에 대해 설명하시오.
    <details>
    <summary>정답</summary>
    
    자바스크립트를 사용해서 브라우저가 서버에게 비동기 방식으로 데이터를 요청하고, 응답받은 데이터로 웹페이지를 동적으로 갱신하는 방식. 브라우저의 Web API인 XMLHttpRequest 객체를 기반으로 동작한다.
       
    </details>

1. Ajax가 없을 때는 어떤 방식으로 데이터를 받아왔는가?
    <details>
    <summary>정답</summary>
    
    이전의 웹페이지는 완전한 HTML을 서버로부터 전송받아 웹페이지 전체를 처음부터 다시 렌더링했다.
    
    <details>
    <summary>꼬리 질문</summary>
    Ajax와 비교해 이전 방식의 단점을 세가지 설명하시오.
    
    <details>
    <summary>정답</summary>
    
    - 이전 웹페이지와 차이가 없는 부분까지 서버로부터 전송받아 불필요한 데이터 통신이 일어난다
    - 변경할 필요가 없는 부분까지 다시 렌더링되어 화면 전환 시 깜빡이는 느낌을 준다
    - 서버와의 통신이 동기 방식으로 동작하기 때문에 서버로부터 응답이 올 때까지 다음 처리가 블로킹 된다

    </details>
       
    </details>
    
    </details>

1. JSON이 무엇인가?
    <details>
    <summary>정답</summary>

    Javscript Object Notation으로, 이름과는 다르게 자바스크립트에 종속되지 않는 언어 독립형 데이터 포멧이라 대부분의 언어에서 사용할 수 있다.
    클라이언트와 서버 간의 HTTP 통신을 위한 텍스트 데이터 포맷이다.

    <details>
    <summary>꼬리 질문</summary>
    JSON을 사용할 때의 주의점에는 무엇이 있는가?
      
      <details>
      <summary>정답</summary>
      
      문자열은 반드시 큰따옴표로 묶어야 한다.(작은 따옴표 불가) 키도 문자열이기 때문에 큰따옴표로 묶어야 한다.<br>
      객체나 배열은 `JSON.stringify`로 직렬화 할 수 있다. 역직렬화는 `JSON.parse()`로 할 수 있다.
         
      </details>
         
      </details>
    
    </details>

1. `ajax`, `axios`,  `XMLHttpRequest`, `fetch`의 차이에 대해 설명하시오.
    <details>
    <summary>정답</summary>
    
    - `ajax`: 기술이라기보다는 통신 '방식'으로, `XMLHttpRequest` 객체, HTML, Javascript 등 여러 기술을 이용해서 비동기로 필요한 부분의 데이터만 받아오는 방식. 
    - `XHR`: 서버와 통신할 때 사용하는 객체로, 페이지의 새로고침 없이도 데이터를 가져올 수 있다. 이름의 'x'는 XML을 의미하지만, JSON 등의 다른 형식으로 받아올 수도 있다.
    - `fetch`: ES6에서 도입된 자바스크립트 내장 라이브러리
    - `axios`: 비동기 통신을 위한 자바스크립트 라이브러리로, `response timeout` 등의 추가 기능을 제공한다.
       
    </details>
