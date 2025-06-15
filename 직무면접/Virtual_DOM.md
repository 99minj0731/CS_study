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
먼저, 어플리케이션이 제일 처음 렌더링 될 때, 어플리케이션의 초기 상태를 담은 virtual DOM을 메모리 상에 하나 생성합니다.  
이후, 어플리케이션이 실행되면서 state나 props가 변경된 부분이 있는 경우, 새로운 버전의 Virtual DOM을 메모리 상에 하나 더 생성합니다.  
새로운 버전의 Virtual DOM이 생성된 후, 이전 버전의 Virtual DOM과 비교하는 과정인 Diffing에 돌입하고, 변경점을 찾아냅니다.  
이 과정에서 두 Virtual DOM 트리의 각 노드를 비교하여 어떤 부분이 변경되었는지 확인합니다.  변경점을 찾아낸 이후에는, 실제 DOM에 적용하는 과정인 Reconcillation에 돌입합니다.  
이 과정에서 변경된 부분만 실제 DOM에 업데이트하기 때문에, 브라우저 성능이 향상될 수 있는 것입니다.  
Reconciliation이 완료된 이후, 또 다른 변경점이 생기면, 구 버전의 Virtual DOM은 폐기되고, 새로운 변경 사항을 반영한 최신 버전의 Virtual DOM이 다시 생성됩니다. 
</details>