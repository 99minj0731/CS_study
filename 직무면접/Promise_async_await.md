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