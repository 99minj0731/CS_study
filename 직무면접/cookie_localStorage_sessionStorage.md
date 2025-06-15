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