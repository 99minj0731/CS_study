### 📝 브라우저 렌더링 과정

<details>
<summary> 브라우저 렌더링의 순서를 설명해주세요. </summary>
</br>
먼저 서버로부터 HTML 문서를 전달받으면, 브라우저 엔진은 위에서 아래로 순차적으로 파싱하며 태그와 속성을 발견합니다.  
이 태그와 속성들은 트리 형태로 변환되어 메모리에 저장되는데, 이를 DOM 트리라고 합니다.  
HTML 파싱 중 CSS링크 또는 스타일 태그를 만나면, 이를 파싱하여 CSSOM 트리로 변환합니다.  
문서의 파싱이 완료되면, DOM과 CSSOM 트리를 결합하여 렌더 트리를 생성합니다.  
렌터 트리는 브라우저 상에서 요소의 위치와 크기를 결정하는 리플로우 과정을 거치며, 마지막으로 요소의 색상, 경계선 등 시각적 요소를 그리는 페인팅 과정이 진행됩니다. 
</br></br> 
</details>

<details>
<summary> HTML파싱 중간에 script 태그를 만나면 어떻게 되나요? </summary>
</br>
파싱 중간에 script 태그를 만나면, 브라우저는 해당 스크립트를 로드하고 실행하기 위해 파싱을 일시 중단합니다.  
외부 스크립트의 경우, 스트립트를 로드하고 실행한 후 파싱을 재개하며, 내부 스크립트의 경우, 실행이 완료될때까지 파싱이 중단됩니다. 이로 인해 파싱 속도가 저하되고, DOM 트리가 완성되기 전에 스크립트가 DOM을 조작할 가능성이 있어, 예기치 못한 상황이 발생할 수 있습니다. 이러한 문제를 방지하기 위해 'async', 'defer' 같은 속성을 사용하여 파싱에 미치는 영향을 최소화할 수 있습니다. 
</br></br> 

</details>

<details>
<summary> async와 defer 속성에 대해 설명해주세요.  </summary>
</br>
'async'와 'defer'는 스크립트를 비동기적으로 로드하는 속성입니다. 이들은 HTML 파싱이 중단되는 현상과 DOM 트리가 완성되기 전에 스크립트가 실행되는 것을 방지하기 위해 사용됩니다.  
'async' 속성은 스크립트가 로드되는 즉시 실행하는 반면, 'defer' 속성은 스크립트를 비동기적으로 로드하되, HTML 파싱이 완료된 후 스크립트를 실행합니다.  
따라서 'async'는 스크립트 로드 순서 상관없이 실행되는 경우에 적합하고, 'defer'는 스크립트의 실행 순서가 중요할 때 적합합니다. 
</br></br> 

- defer : 안정적, 가장 많이 씀   
두 스크립트가 병렬로 다운되지만 HTML 파싱 완료 후 -> 작성 순서대로 실행됨
```
<!DOCTYPE html>
<html>
  <head>
    <script src="script1.js" defer></script>
    <script src="script2.js" defer></script>
  </head>
  <body>
    <h1>페이지 제목</h1>
  </body>
</html>
```

- async : 순서가 중요하지 않은 경우에만 사용  
두 스크립트는 병렬로 다운되지만 다운되는 순서대로 실행됨 -> 순서 보장 안됨  
DOM이 아직 안만들어졌을 수도 있음 -> 에러 위험 
```
<!DOCTYPE html>
<html>
  <head>
    <script src="script1.js" async></script>
    <script src="script2.js" async></script>
  </head>
  <body>
    <h1>페이지 제목</h1>
  </body>
</html>
```

</details>

### 📝 DOM

<details>
<summary> DOM의 개념을 설명하세요. </summary>
</br>
Document Object Model의 약자.  
HTML이나 XML같은 마크업 언어로 작성된 문서를 자바스크립트와 같은 프로그래밍 언어가 조작할 수 있도록 하는 트리 구조 인터페이스를 의미합니다.  
DOM은 계층적 구조를 가진 노드 트리로 구성됩니다.
</br></br> 
</details>

<details>
<summary> DOM은 왜 필요한가요? </summary>
</br>
동적인 웹 페이지를 구현하려면 자바스크립트와 같은 프로그래밍 언어가 문서에 접근하고, 제어할 수 있는 수단이 있어야 합니다. 하지만, 마크업 언어로 작성된 문서에는 이러한 수단이 없기때문에 문서에 접근하고, 제어할 수 있는 수단인 DOM이 필요합니다.
</br></br> 
</details>

<details>
<summary> DOM을 통해 어떤 동작을 할 수 있는지 예를 들어주세요. </summary>
</br>
만약 button element가 클릭되었을 때, 특정 함수를 호출하도록 Event Handler를 추가할 수 있고, 웹 페이지 내에 새로운 요소를 추가하거나, 삭제, 수정할 수 있습니다.
</br></br> 
</details>

<details>
<summary> DOM은 왜 계층적 구조로 표현하는지 설명해주세요. </summary>
</br>
계층적 구조에서는 노드들 간의 관계가 부모, 자식, 형제 등으로 명확하게 정의됩니다.  
이는 노드의 추가, 제거, 이동 작업을 쉽게 할 수 있도록 도와줍니다. 또한, 이벤트가 발생한 요소로부터 이벤트가 올라가는 이벤트 버블링, 반대로 이벤트가 내려가는 이벤트 캡처링 동작은 계층적 구조에서 효율적으로 동작하기 때문에, DOM을 계층적 구조로 표현하는 것입니다. 
</br></br> 
</details>

### 📝 Virtual DOM

<details>
<summary> Virtual DOM의 개념에 대해 설명해주세요. </summary>
</br>
Virtual DOM은 웹 성능을 최적화하기 위해 사용되는 DOM  관리 방법으로, 웹 어플리케이션의 상태 변경 시, 객체 형태의 가상 DOM을 통해 변경된 부분만 찾아내어 이를 실제 DOM에 적용하는 기능을 합니다.  
Virtual DOM의 동작 순서는 Diffing과 Reconiliation, 크게 두 가지로 구분할 수 있습니다.  
Diffing이란, Virtual DOM에서 변경점을 찾아내는 과정을 의미하고, Reconciliation이란, 찾아낸 변경점을 실제 DOM에 적용하는 과정을 의미합니다. 
</br></br>
</details>

<details>
<summary> Virtual DOM이 동작하는 예시를 간략히 설명해주세요. </summary>
</br>
먼저, 어플리케이션이 제일 처음 렌더링 될 때, 어플리케이션의 초기 상태를 담은 virtual DOM을 메모리 상에 하나 생성합니다.  
이후, 어플리케이션이 실행되면서 state나 props가 변경된 부분이 있는 경우, 새로운 버전의 Virtual DOM을 메모리 상에 하나 더 생성합니다.  
새로운 버전의 Virtual DOM이 생성된 후, 이전 버전의 Virtual DOM과 비교하는 과정인 Diffing에 돌입하고, 변경점을 찾아냅니다.  
이 과정에서 두 Virtual DOM 트리의 각 노드를 비교하여 어떤 부분이 변경되었는지 확인합니다.  변경점을 찾아낸 이후에는, 실제 DOM에 적용하는 과정인 Reconciliation에 돌입합니다.  
이 과정에서 변경된 부분만 실제 DOM에 업데이트하기 때문에, 브라우저 성능이 향상될 수 있는 것입니다.  
Reconciliation이 완료된 이후, 또 다른 변경점이 생기면, 구 버전의 Virtual DOM은 폐기되고, 새로운 변경 사항을 반영한 최신 버전의 Virtual DOM이 다시 생성됩니다. 
</br></br>
</details>

<details>
</br>
<summary> 그럼 state나 props가 변경될 때마다 Diffing과 Reconciliation이 수행되는 건가요? </summary>
React를 비롯하여 Virtual DOM을 사용하는 대부분의 프레임워크에서는 Batch 업데이트를 지원하고 있습니다.  
따라서, 짧은 시간 안에 여러 개의 state와 props가 동시에 변경되면, 이를 각각 처리하는 것이 아니라, 한꺼번에 모아서 처리합니다. 
</br></br>
</details>

<details>
</br>
<summary> Virtual DOM을 사용하는 것이 그렇지 않은 것보다 좋은가요? </summary>
항상 그런 것은 아닙니다.  
간단한 어플리케이션의 경우에는 Virtual DOM을 사용하면 오히려 메모리 공간을 차지합니다.  
다만, DOM 트리가 복잡하고, 상태 변경도 빈번하게 일어나는 대규모 어플리케이션에서 사람의 인지 능력으로는 정확히 어떤 DOM을 업데이트해야 하는지 식별하기 어렵기 때문에, Virtual DOM을 사용하는 것입니다.  
따라서, 어플리케이션 복잡도와 요구 사항에 맞게 Virtual DOM 적용 여부를 결정하는 것이 좋습니다. 
</br></br>
</details>

### 📝 리플로우와 리페인트

<details>
<summary> 리플로우란 무엇인지 설명해주세요. </summary>
</br>
리플로우란, 웹 페이지 내에서 요소의 위치 또는 크기에 변화가 있을 때, 변화된 레이아웃을 다시 계산하여 렌더 트리에 적용하는 과정을 의미합니다. width, height, padding 그리고 border-width와 같은 크기 관련 속성, position, top, left와 같은 위치 관련 속성, display, flex 속성과 같은 레이아웃 관련 속성, font-size, font-weight과 같은 폰트 크기 관련 속성이 리플로우를 유발하는 속성입니다. 
</br></br> 
</details>

<details>
<summary> 리페인트란 무엇인지 설명해주세요. </summary>
</br>
리페인트란, 웹 페이지 내에서 요소의 시각적인 표현에 변화가 있을 때, 변화된 시각적 표현을 가시 계산하여 렌더 트리에 적용하는 과정을 의미합니다. color, background-color 같은 색상 관련 속성, border-color, border-radious와 같은 테두리 관련 속성이 리페인트를 유발하는 속성입니다.  
</br></br> 
</details>

<details>
<summary> 리플로우와 리페인트의 성능상 차이점을 설명해주세요. </summary>
</br>
부모 노드의 레이아웃 변화는 자식 노드의 레이아웃까지 영향을 미치기 때문에, 리페인트와는 달리, 리플로우가 발생하면 하위 렌더트리를 다시 계산하고 재구성하는 과정이 필요합니다. 따라서, 리플로우는 그 자체만으로도 부하가 큰 작업입니다. 또한, 리플로우가 발생하면 일반적으로 리페인트도 다시 발생하기 때문에, 성능에 큰 영향을 끼친다고 할 수 있으며, 렌더링 성능을 최적화하기 위해선 피플로우를 최소화해야 합니다. 또한, 리플로우는 주로 CPU를 활용하는 반면, 리페인트는 GPU를 활용한다는 차이도 있습니다.
</br></br> 

- CPU ? </br>
CPU란 컴퓨터의 뇌라고 할 수 있음.  
복잡한 계산과 명령을 순차적으로 처리함.  
하나씩 정확하고 빠르게 계산함.  
웹 서핑, 문서 작성, 게임 등 대부분의  일반적인 작업을 처리함. 

- GPU ? </br>
GPU란 컴퓨터의 시각 처리 장치임.  
동시에 많은 계산을 병렬로 처리함.  
그래픽을 그리거나, 3D 게임이나 AI 학습 같은 많은 데이터 처리에 적합함.  
주로 게임 그래픽이나 영상 처리, AI 계산 등에 사용 됨.  
</br></br> 
</details>

<details>
<summary> 리플로우를 최소화하기 위한 방법은 무엇이 있을까요? </summary>
</br>
리플로우를 최소화하기 위해, DOM 업데이트를 하나로 묶어 Batch Update하는 방법을 생각해볼 수 있습니다. 또한, offsetHeight, offsetWidth와 같은 자바스크립트의 레이아웃 속성에 여러 번 접근하면 리플로우가 발생할 수 있기 때문에, 이런한 속성들은 변수에 저장해 두고 재사용해야 합니다. 마지막으로, 가급적 레이아웃 변경이 적은 요소를 사용해야 합니다. position 속성을 예로 들면 fixed나 absolute 같은 값들을 사용할 수 있습니다. 
</br></br> 
</details>

### 📝 CORS와 Preflight의 개념

<details>
<summary>CORS란 무엇인지 설명해주세요.</summary>
</br>
CORS란 Cross Origin Resource Sharing의 약자로, 교차 출처 리소스 공유라고 부릅니다. </br> 2009년에 HTML5 표준으로 채택된 프로토콜이며, SOP에 의해 제한된 교차 출처 간 리소스 공유를 허용하기 위한 방법입니다. </br> 애플리케이션의 요구 사항이 복잡해지면서, 다른 도메인의 리소스를 활용하는 경우가 많아졌기 때문에 등장한 프로토콜로, 서버에서 CORS 관련 헤더를 설정하여 다른 도메인에서의 리소스 요청을 허용할 수 있습니다. </br> CORS에러는 CORS 헤더를 적절히 설정하지 않은 상태에서 교차 출처 리소스를 요청하는 경우 발생할 수 있습니다. </br>

CORS란 다른 웹사이트 주소에서 정보를 요청할 때 허락받는 시스템. 원래는 보안 때문에 "다른 사이트 거 가져오지마!"라는 규칙이 있었지만 요즘은 API처럼 다른 도메인에서 정보 가져올 일이 많기때문에 서버가 "괜찮아, 가져가도 돼"라고 허락해주는 것이 CORS임. 허락을 해주지 않으면 브라우저가 막음 -> CORS 에러

- 프로토콜?  
서버와 브라우저가 서로 어떻게 대화할지 약속한 규칙 </br>
데이터를 어떻게 주고받을지 정한 **통신 방식의 규칙** 
예를 들어 “너 파일 줄게”, “이미지 요청할게” 이런거를 할 때의 규칙 </br>
CORS는 그 규칙 중 하나 </br>

- 도메인?  
웹사이트 주소 </br>
http:// => 보통 웹사이트 </br>
https:// => 보안이 적용된 웹사이트 </br>
다른 도메인에서 요청한다 ⇒ A라는 웹사이트가 B라는 웹사이트에 있는 파일(리소스)를 가져오려고 한다. </br>
이걸 막 하면 보안 문제가 생기니까 서버에서 내 자료를 다른 사이트에서도 써도 돼요라는 허락(CORS 허용)을 해줘야함. </br>

- 헤더? </br>
요청하거나 응답할 때 같이 보내는 **메모지** 같은 역할 </br>
이건 "JSON"이에요, 이건 다른 사이트가 요청했어요. 허락했어요 같은 **작은 설명서** </br></br>

</details>

<details>
<summary>SOP란 무엇인지 설명해주세요.</summary>
</br>
Same Origin Policy의 약자로, 동일 출처 정책을 의미합니다. </br> 1990년대 후반에 등장한 보안 정책으로, 현재 출처와 동일한 출처의 리소스만 접근할 수 있도록 하는 정책입니다. </br> 여기서 동일 출처란, 도메인과 프로토콜, 포트 번호가 모두 같은 경우를 의미하며, 하나라도 다를 경우 동일 출처 정책에 의해 리소스 접근이 제한됩니다. </br></br>

- 포트 번호? </br>
컴퓨터가 통신하는 문(문 번호) </br>
서버가 어떤 문을 통해 데이터를 주고받을지 지정하는 번호 </br>
예: https://www.example.com → 내부적으로는 :443으로 접속함 </br></br>

</details>

<details>
<summary> SOP가 없을 경우 가능한 보안 취약점은 무엇인가요? </summary>
</br>
사용자 인증 정보에 해당하는 세션 ID 같은 정보들이 쿠키에 포함되어 있을 수 있기 때문에 이 세션 정보를 탈취하여 Cross Site Scripting 혹은, CSRF와 같은 해킹 공격에 이용할 수 있습니다. </br> SOP 정책을 통해 리소스를 다른 도메인에서 접근하지 못하도록 제한한다면, 이러한 해킹 공격을 어느 정도 완화할 수 있습니다. </br> </br>

- 세션 ID? </br>
로그인한 사용자를 기억하기 위한 번호표.  </br>
다른 페이지로 넘어가도 서버는 세션 ID라는 고유 번호를 만들어서 로그인했다라는 것을 서버가 알아보는 것.  </br>
즉, 로그인 상태를 유지하게 해주는 열쇠 </br>

- 쿠키? </br>
브라우저가 서버로부터 받은 세션 ID같은 것을 쿠키에 저장.  </br>
다음 요청 때 해당 쿠키를 자동으로 같이 보냄 -> 서버는 "너구나!"라고 인식 </br>
쿠키는 로그인 상태, 최근 본 상품, 설정 같은 것을 저장할 때도 사용됨 </br>
=> 세션ID (열쇠), 쿠키 (그 열쇠를 담아놓은 주머니) </br>

- XSS (Cross Site Scripting)?  </br>
사이트에 악성 스크립트를 심는 해킹 방법 </br>
사용자의 브라우저 정보를 해커가 탈취할 수 있게 만든는 위험한 공격 </br>

- CSRF (Cross Site Request Forgery)? </br>
내가 의도하지 않은 요청이 "내 계정"으로 날아가는 해킹 </br>
신뢰된 사용자의 인증정보를 악용하여 공격하는 방식 </br></br>

</details>

<details>
<summary> CORS 프로토콜이 동작하는 원리를 설명해주세요. </summary>
</br>
서버는 응답 처리 코드에서 CORS 관련 헤더를 설정할 수 있습니다. </br>
이 헤더를 통해 요청을 허용할 도메인과, HTTP 메서드, 그리고 요청 헤더의 종류를 정의할 수 있습니다. </br> 이후, 브라우저에서 서버로 리소스를 요청할 때, 이 헤더에 설정한 정보와 일치하지 않는다면, 브라우저에서 CORS에러가 발생하는 것입니다. </br> CORS 프로토콜 스펙에서 정의한 비교적 보안적으로 민감하지 않다고 판단되는 요청들이 있는데, 이를 단순 요청이라고 칭하며, 이 요청을 제외한 CORS 요청에는 실제 요청을 전송하기 전, 요청 허가를 위한 preflight 요청이 발생할 수 있습니다.</br></br>

</details>

<details>
<summary> Preflight 요청이란 무엇인지 설명해주세요. </summary>
</br>
preflight 요청은 보안적으로 민감한 CORS 요청에 대해, 요청이 가능한지를 먼저 확인하는 과정입니다.</br> 브라우저에서 자동으로 실행되는 요청으로, OPTIONS 메서드를 사용하며, 서버에서 설정한 CORS 관련 설정들을 Header 값으로 확인할 수 있습니다.</br> 이 과정을 통해, 허용되지 않는 요청에 대한 처리 부하를 낮출 수 있습니다. 즉 Preflight는 브라우저 성능 최적화용!</br></br>
</details>

<details>
<summary> 모든 CORS 프로토콜마다 Preflight 요청이 일어나나요?</summary>
</br>
보안적으로 민감하지 않은 단순 요청이거나, 이전에 응답받은 Preflight 응답이 캐싱되어 있는 경우 Preflight 요청이 일어나지 않습니다.</br> 브라우저에서 자동으로 실행되는 요청으로, OPTIONS 메서드를 사용하며, 서버에서 Access-Control-Max-Age라는 헤더 값을 초 단위로 설정할 수 있고, 이전 요청의 응답값이 아직 캐싱되어 있다면, 같은 요청에 대해서는 Preflight 요청이 일어나지 않습니다.</br> </br>

- 캐싱?   
자주 사용하는 데이터를 임시로 저장해 두고, 다음에 더 빠르게 사용하려는 것. </br>
웹에서는 서버에 매번 요청하지 않고, 이전에 받아온 응답 데이터를 잠깐 저장해두는 방식</br>
- OPTIONS 메서드란?  
브라우저가 먼저 "이 요청 해도 돼?"하고 서버에게 허락을 구하는 HTTP 메서드. </br>
Preflight 요청은 실제 요청 전에 OPTIONS 메서드로 먼저 날아감. </br>
- Access-Control-Max-Age  
Preflight 응답을 얼마나 오래 캐시할지(저장할지)정하는 시간.</br>
서버가 설정한 시간에 따라, 브라우저는 해당 시간 동안 Preflight 요청을 생략함. </br>
이 설정이 없다면, 브라우저는 매번 OPTIONS 요청을 보내야 해서 성능이 떨어짐. </br></br>

</details>

<details>
<summary> 단순 요청이 무엇인지 설명해주세요. </summary>
</br>
요청의 메서드가 GET, HEAD, POST 중 하나이며, 헤더와 Content-Type이 CORS프로토콜에서 지정한 값인 경우가 단순 요청에 해당합니다.</br> 이 경우는 Preflight 과정을 통한 권한 조회 과정 없이 CORS 요청이 가능합니다. </br></br>

- HEAD?  
  GET 요청처럼 정보를 요청하지만, 헤더만 받고, 실제 내용(body)는 받지 않는 요청 방식.  
  언제 사용? 파일 용량, 수정 시간 같은 메타 정보만 필요할 때  
  ex. 이미지 용량 확인, 웹 페이지 존재 여부 검사 등  

- Content-Type이란?  
  서버나 클라이언트가 보내는 데이터가 어떤 형식인지 알려주는 '데이터 설명서'



</details>

### 📝 Promise와 async-await

<details>
<summary> Promise의 개념에 대해 설명해주세요. </summary>
</br>
Promise는 비동기 연산의 상태를 나타내는 객체입니다.  
비동기 처리가 진행중이면 pending, 성공이면 fulfilled, 실패면 rejected라는 상태값을 가집니다. Promise는 비동기 프로그래밍을 then과 catch를 통해 간결하게 표현할 수 있도록 ES6에서 새로 도입되었습니다.  
</br></br>

- Promise  
비동기 작업을 처리하고, 그 상태를 담는 객체  
- then/catch  
Promise 객체에서 결과를 처리하는 메서드
- async/await  
Promise를 더 쉽게 쓸 수 있게 해주는 문법
</br></br>
</details>

<details>
<summary> Promise 등장 이전에는 어떤 방식으로 비동기 처리를 했는지 설명해주세요. </summary>
</br>
Promise 등장 이전에는 비동기 작업을 처리하는 함수에 성공 콜백과, 실패 콜백을 각각 넘겨서 완료 상태에 따른 처리를 했습니다.  
이런 방식이다 보니, 두 개 이상의 비동기 작업이 순서를 갖고 실행되어야 할 때, 콜백 함수 안에 또 다른 콜백 함수가 점점 중첩되는 callback hell 현상이 발생하여, 코드 가독성 및 유지보수성 저하의 요인이 되었습니다. 
</br></br> 
</details>

<details>
<summary> async-await에 대해 설명해주세요. </summary>
</br>
Promise의 완료를 기다리기 위한 문법으로, async 키워드로 정의한 함수 내에서 호출되는 Promise 앞에 await 키워드를 사용하면, 해당 Promise가 완료될 때까지 코드의 실행을 일시정지 할 수 있습니다. 이를 통해, 비동기 코드를 마치 동기 코드처럼 쉽게 작성할 수 있습니다.
</br></br>
</details>

<details>
<summary> async-await 를 사용할 때 주의해야할 점을 알려주세요. </summary>
</br>
await의 에러 핸들링은 try-catch 블록에서 실행할 수 있습니다. 또한, await는 Promise가 완료될 때까지 함수의 실행을 중단하기 때문에, 실행 흐름을 잘 고려하여 적재적소에 사용해야합니다. 예를 들어, 여러 비동기 작업이 순차적으로 진행될 필요가 없는 경우에는, await 대신 Promise.all 함수를 사용하는 것이 바람직합니다.  
Promise.all 함수는 여러 개의 api를 동시에 요청할 때나, 이미지나 파일을 병렬로 불러올 때 그리고 모든 결과가 모두 있어야 다음 작업을 할 수 있을 떄 사용할 수 있습니다. 
</details>

### 📝 cookie, localStorage, sessionStorage

<details>
<summary> cookie의 특징에 대해 설명해주세요. </summary>
</br>
쿠키는 웹 클라이언트에서 사용하는 저장 수단으로, 'key, value' 쌍으로 데이터가 저장됩니다.  
쿠키는 HTTP 요청시 자동으로 헤더에 포함되어 전송되기 때문에, 주로 인증 정보와 같이 서버와의 통신에 필요한 데이터를 저장하며, 많은 용량의 쿠키가 저장되어 있을 경우, 통신 과정에서 오버헤드가 발생할 수 있기 때문에, 일반적으로 쿠키 한 개의 용량을 4KB 정도로 제한합니다.  
또한, 쿠키는 'Expires' 혹은 'Max-Age' 속성을 통해 데이터 저장 시 만료 날짜를 지정할 수 있고, 'Path' 속성을 통해 같은 도메인 내에서도 쿠키가 전송될 URL의 범위를 설정할 수 있다는 특징이 있습니다. 
</br></br> 

- 헤더란?  
웹에서 클라이언트(브라우저)와 서버가 서로 주고받는 부가 정보  
- 오버레드란?  
필요한 데이터 외에 추가로 생기는 부담이나 부가 비용 
</details>

<details>
<summary> localStorage와 sessionStorage의 공통점에 대해 설명해주세요. </summary>
</br>
localStorage와 sessionStorage는 HTML5에서 새롭게 도입된 Web Storage로, document 객체로도 접근할 수 있는 쿠키와는 달리, 자바스크립트를 통해서만 데이터 저장과 접근이 가능합니다.  
key, value 형태로 약 5MB까지 저장이 가능하며, HTTP 요청 시 자동으로 데이터를 전송하지 않기 때문에, 비교적 대용량의 데이터를 클라이언트측에서 관리하고 싶을 때 사용합니다. 쿠키와는 달리 명시적으로 만료 날짜를 지정할 수 없습니다. 
</br></br>  

- document 객체로 접근?  
document.cookie라는 방식으로 DOM객체를 통해 접근 가능하다는 뜻.
```
// 쿠키 설정
document.cookie = "username=민정";

// 쿠키 읽기
console.log(document.cookie); // 👉 "username=민정"
```
</details>

<details>
<summary> localStorage와 sessionStorage의 차이점에 대해 설명해주세요. </summary>
</br>
localStorage는 탭이나 브라우저를 닫아도 데이터가 제거되지 않으며, 도메인만 동일하다면, 2개 이상의 탭이 열러 있어도 이들 간에 데이커가 공유된다는 특징이 있습니다.  
반면, sessionStorage는 탭이나 브라우저가 닫히면 데이터가 자동으로 제거되며, 동일한 탭 내에서만 데이터가 유지된다는 특징이 있습니다.  
</br></br> 
</details>

### 📝 화살표함수와 function 키워드의 차이점

<details>
<summary> 화살표 함수와 function 키워드의 차이점을 설명해주세요. </summary>
</br>
먼저, 화살표 함수는 코드 블럭을 사용하지 않을 경우, return 문을 명시할 필요가 없습니다.  
또한, function 키워드는 arguments 객체를 통해 함수 인자에 접근할 수 있지만, 화살표 함수는 arguments 객체를 갖지 않기 때문에, 나머지 매개 변수를 통해 함수 인자에 접근할 수 있습니다.  
마지막으로, 함수 호출 방식에 다라 this의 참조가 다르게 동작하는 function 키워드와는 달리, 화살표 함수는 this가 항상 상위 스코프의 this를 참조합니다. 
</br></br> 

- 일반 함수 (function)
```
function add(a, b) {
  return a + b
}
```

- 화살표 함수 (=>)  
```
const add = (a, b) => a + b
```

- arguments 객체
``` 
//일반 함수

function printArg () {
  console.log(arguments) // 모든 인자가 담긴 유사 배열
}
printArg(1, 2, 3) //[1, 2, 3]
```

```
//화살표 함수 

const printArg = () => {
  console.log(argument) // 에러발생, 화살표 함수는 arguments객체를 가지지 않음
}

const printArg = (...args) => {
  console.log(args) //[1, 2, 3]
}
printArg(1, 2, 3)
```

- this 바인딩  
일반 함수는 this가 누가 호출했느냐에 따라 달라짐.  
``` 
const obj = {
  name: "민정", 
  sayHi: function() {
    console.log(this.name) // '민정'
  }
}
obj.sayHi()
```  
화살표 함수는 this가 항상 상위 스코프에서 정해진 this를 그대로 사용 
```
const obj = {
  name: "민정", 
  sayHi: () => {
    console.log(this.name) // undefined(this는 obj가 아님)
  }
}
obj.sayHi()
```

- 차이  
function은 this가 동적으로 바뀜(호출하는 대상에 따라)  
화살표 (=>)는 this가 고정돼 있음 (자기 바깥쪽 스코프의 this 사용)

</details>

<details>
<summary> 왜 화살표 함수에서는 this가 항상 상위 스코프를 참조하도록 하였을까요? </summary>
</br>
function 키워드로 정의한 함수는 호출 방식에 따라 this 바인딩이 다르게 동작하기 때문에, this 값을 예측하기 어렵다는 문제가 있습니다.  
따라서, 화살표 함수에서는 this가 항상 상위 스코프를 참조하도록 개선하여, this 바인딩의 일관된 동작을 보장하고, 코드 흐름에 따라 this의 참조값을 예측하기 쉽도록 만든 것입니다. 
</br></br> 
</details>

<details>
<summary> function 키워드 함수의 this 바인딩은 어떤 식으로 동작하나요? </summary>
</br>
일반적인 함수 호출의 경우는 this가 전역 객체를 가리키며, 객체의 메서드로 호출되는 경우는 해당 객체를 가리키게 됩니다.  
또한, 함수가 이벤트 핸들러로써 호출되는 경우에는 이벤트가 발생한 요소를 가리킵니다.  
이처럼, function 키워드로 정의한 함수는 this 바인딩의 일관성이 부족하기 때문에, ED6 이전에는 apply나 call, bind와 같은 함수를 통해 명시적으로 this 바인딩을 수행했습니다.  
</br></br> 

- 일반 함수 호출
```
function sayHi() {
  console.log(this) // 브라우저: window, Node.js: global
}
```
- 객체의 메서드로 호출될 때 : this는 그 객체
``` 
const person = {
  name: "철수",
  sayHi: function() {
    console.log(this.name) 
  }
}
person.sayHi() // 객체가 호출 -> this는 person
``` 
- 이벤트 핸들러로 호출될 때 : this는 이벤트가 발생한 요소
```
<button onclick="handleClick()">클릭</button>

<script>
  function handleClick() {
    console.log(this); // 이벤트 핸들러 안에서는 this가 그 이벤트를 발생시킨 DOM 요소를 가리킴
  }
</script>
```
</details>