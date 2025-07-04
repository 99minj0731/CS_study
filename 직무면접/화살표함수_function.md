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