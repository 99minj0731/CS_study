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