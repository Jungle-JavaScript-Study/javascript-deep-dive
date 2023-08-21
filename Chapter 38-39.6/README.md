1. 브라우저의 렌더링 순서를 설명하시오.
    <details>
    <summary>정답</summary>
    
    리소스 요청-서버 응답-HTML 파싱-DOM 트리 빌드-CSSOM 트리 빌드-자바스크립트 파싱(AST 생성)-렌더링 트리 형성-HTML 요소의 레이아웃 계산-화면에 페인트-합성&렌더-레이아웃&리페인트
       
    </details>

2. 주소창에 URL을 입력하고 엔터를 누르면 브라우저는 어떻게 리소스를 받아오는가?
    <details>
    <summary>정답</summary>
      
    URL의 호스트 이름이 DNS를 통해 IP 주소로 변환되고 이 IP 주소를 갖는 서버에 요청을 전송한다.
    루트 요청을 받은 서버는 암묵적으로 `index.html`을 응답한다.
        
    </details>

3. 다음 주소의 URI 구성 요소를 설명해보시오.
   `https://mydomain.com:80/docs/search?category=javascript&lang=co#intro`
    <details>
    <summary>정답</summary>
      
    <img width="586" alt="image" src="https://github.com/Jungle-JavaScript-Study/deep-dive/assets/70076564/bec548d3-0d15-4690-b184-8f5440431cc6">
 
    </details>
    
4. 브라우저의 네트워크 탭에 index.html 이외의 리소스가 응답된 것은 무엇인가?
    <details>
    <summary>정답</summary>
    
    브라우저의 렌더링 엔진이 HTML을 파싱하는 도중에 외부 리소스를 로드하는 태그를 만나면 파싱을 일시정지하고 해당 리소스 파일을 서버에 요청해 받은 응답이다.
    
    </details>

11. 자바스크립트가 포함된 html을 실행하는 것은 누구인가?
    <details>
    <summary>정답</summary>
      
    브라우저의 **렌더링 엔진**이 HTML을 파싱&실행하다가 중간에 자바스크립트 태그가 있으면 파싱을 중단하고 **V8** 등의 **자바스크립트 엔진**에 제어권을 넘긴다. 자바스크립트 엔진이 자바스크립트를 파싱해서 AST 생성과 바이트트코드 실행을 완료하고 나면 다시 렌더링 엔진으로 제어권을 넘겨서 HTML 파싱이 중지된 부분부터 재개한다.
        
    </details>

5. HTTP 프로토콜에 대해 설명해보시오.
    <details>
    <summary>정답</summary>
      
    웹에서 브라우저와 서버가 통신하기 위해 만든 규약
        
    </details>

    <details>
    <summary>꼬리 질문</summary>
      
    HTTP 프로토콜은 누가 정하는가?

    <details>
    <summary>정답</summary>
      
    월드와이드웹 프로젝트를 제안한 팀 버너스 리가 처음 제안. 이후로는 국제 기술 표준화 기구인 IETF가 정한다.
    IETF의 HTTP Working Group에서 합의된 내용이 새로운 HTTP 버전의 표준으로 제정됨.
        
    </details>
        
    </details>

7. HTTP 1.1과 2.0의 차이가 무엇인가?
    <details>
    <summary>정답</summary>
    
    - 다중 요청과 응답: 1.1은 커넥션 당 하나의 요청과 응답만 처리하기 때문에 여러개의 요청/응답을 한번에 전송할 수 없음. 2.0은 리소스의 동시 전송이 가능해져서 페이지 로드 속도가 빨라짐.
    - 헤더 압축: 1.1에서는 헤더가 텍스트로 전송되지만, 2.0에서는 헤더를 압축하여 크기를 줄임.
    - 서버 푸시: 2.0에서는 서버가 클라이언트의 요청에 의해 아직 요청되지 않은 자원을 미리 보내줄 수 있는 서버 푸시 기능을 제공

    </details>

    <details>
    <summary>꼬리 질문</summary>
      
      1.0과 1.1의 차이는?
     
      <details>
      <summary>정답</summary>
  
      - Keep-Alive 연결: 1.0은 매 요청마다 새로운 연결을 열었지만, 1.1에서는 연결을 재사용해서 여러 요청과 응답을 처리할 수 있음
      - 파이프라인 요청: 클라이언트가 요청을 보낼 때 기다리지 않고 연속적으로 요청을 보내면 서버는 순차적으로 응답을 반환
      - 캐싱을 위한 헤더, 압축을 위한 헤더 등이 추가
          
      </details>
        
    </details>

9. 렌더 트리에 대해 설명하시오.
    <details>
    <summary>정답</summary>
      
    DOM과 CSSOM을 렌더링하기 위해 트리 형태로 결합한 것. 화면에 렌더링되는 노드만으로 구성되기 때문에 실제로 보이지 않는 `meta` 태그나 `display:none`으로 설정된 노드 등은 포함되지 않는다.
        
    </details>

10. 리렌더링이 일어나는 것은 언제인가?
    <details>
    <summary>정답</summary>
    
    1) javascript 코드로 노드가 생성되거나 삭제될 때
    2) 브라우저 창의 크기가 변경되어 뷰포트가 변경될 때
    3) HTML 요소의 위치나 크기가 변경될만한 스타일 변경이 있을 때
    
    </details>

11. script 태그의 위치가 중요한 이유는 무엇인가?
    <details>
    <summary>정답</summary>
      
    브라우저가 파싱을 동기적으로 실행하기 때문에 script 태그가 위에 있으면 DOM 생성이 지연돼서 로딩 시간이 오래걸린다. 또, 이 때 자바스크립트 코드에서 DOM API를 사용하면 변경하려는 DOM이 아직 생성되지 않은 상태라 문제가 생길 수 있다.

    </details>

    <details>
    <summary>꼬리 질문</summary>
      
      위의 문제를 해결하기 위한 방법을 말해보시오.
  
      <details>
      <summary>정답</summary>
        
      1) 자바스크립트를 `body` 요소의 최하단에 위치시키기
      2) `script` 태그에 `async`나 `defer` 사용해서 **외부** 자바스크립트 파일 비동기적으로 로드하기
         - `async`: 자바스크립트 파일이 로드된 직후에 HTML 파싱을 중단하고 실행됨 -> 순서가 보장되지 않음
         - `defer`: 자바스크립트 파일 로드 후 DOM 생성이 완료될 때까지 기다렸다가 `DOMContentLoaded` 이벤트가 발생하면 실행됨
          
      </details>
        
    </details>

4. DOM이 무엇인가?
    <details>
    <summary>정답</summary>
    
    HTML 문서를 파싱해서 브라우저가 이해할 수 있도록 HTML 요소 노드의 계층 구조를 표현한 트리형태의 자료구조
    
    </details>

5. 노드 객체의 주요 타입을 설명하시오.
    <details>
    <summary>정답</summary>
      
    - document node: DOM트리의 최상위에 존재하는 루트 노드로서 다른 노드에 접근하기 위한 엔트리포인트 역할을 한다. 전역 객체인 `window`의 `document`프로퍼티에 바인딩된 객체를 가리키기 때문에 하나의 HTML에 `document` 객체는 하나만 존재한다.
    - element node: HTML 요소를 가리키는 객체로, 부자 관계를 가진다.
    - attribute node: HTML 요소의 어트리뷰트를 가리키는 객체로, 해당 요소 노드에만 연결되어 있어 부모 노드는 가지지 않는다.
    - text node: 텍스트를 가리키는 객체, 요소 노드의 자식 노드이자 리프노드이다.
        
    </details>

4. 특정 요소 노드를 취득할 수 있는지 확인하는 방법은?
    <details>
    <summary>정답</summary>
    
    `Element.prototype.matches` 메서드로 CSS 선택자를 전달해 확인
    
    </details>

5. `HTMLCollection`과 `NodeList`에 대해 설명하시오.
    <details>
    <summary>정답</summary>
      
    둘 다 DOM API가 여러개의 결과값을 리턴하기 위한 객체인데, `HTMLCollection`은 항상 live 객체이지만 `NodeList`는 특정한 경우에만 live 객체로 동작한다.<Br>
    일반적으로 `getElementsBy~`로 노드를 취득하면 `HTMLCollection`을 리턴받고, `querySelecteorAll`로 얻으면 `NodeList`를 받는다.
    </details>

    <details>
    <summary>참고 사항</summary>

    `getElementsByName`은 `NodeList`를 얻음.<br>
    `childNodes` 프로퍼티로 자식 노드를 얻을 때는 live 객체인 `NodeList`를 얻음.<br>
    [stackoverflow-when is nodelist live and when is it static?](https://stackoverflow.com/questions/28163033/when-is-nodelist-live-and-when-is-it-static)
        
    </details>

4. `childNodes`롸 `children` 프로퍼티의 차이에 대해 설명하시오.
    <details>
    <summary>정답</summary>
    
    - `childeNodes`는 `Node` 요소의 프로퍼티로, `NodeList`를 리턴하며 텍스트노드도 포함된다.
    - `children`은 `Element` 요소의 프로퍼티로 `HTMLCollection`를 리턴하며 텍스트노드는 포함하지 않는다.
    
    </details>

5. `innerHTML`과 `innerAdjacentHTML`에 대해 설명하시오.
    <details>
    <summary>정답</summary>

    둘 다 문자열의 HTML 마크업을 파싱해서 DOM에 반영하기때문에 XSS 공격의 위험이 있다.
    `innerHTML`은 요소 노드의 모든 자식을 제거하고 새롭게 집어넣기때문에 리렌더링 과도하게 발생한다. 또한 삽입 위치를 지정할 수 없다. `innerAdjacentHTML`은 기존 요소를 제거하지 않으면서 위치를 지정해서 새로운 요소를 삽입할 수 있다.
        
    </details>

4. 요소 노드를 여러 개 동적으로 추가할 때 주의할 점을 설명하시오.
    <details>
    <summary>정답</summary>
    
    여러 요소 노드를 각각 생성해서 추가하면 DOM이 변경될 때마다 리플로우와 리페인트가 일어나 성능에 좋지 않다. 이 때 컨테이너 노드로 감싸 컨테이너 노드만 추가해서 해결할 수 있는데, 불필요한 요소가 추가되므로 `DocumentFragment`노드를 사용해 DOM에 추가하면 자신은 제거되고 자식 노드만 DOM에 추가되도록 할 수 있다.
    
    </details>
