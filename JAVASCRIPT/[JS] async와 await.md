
## async 와 await
1. async
2. await
3. 요약 
---

### async
> <span style='color: orange'>특징</span>
- function 앞에 async를 사용하면 해당 함수는 항상 Promise를 반환합니다.
- Promise가 아닌 값을 반환하더라도 이행된 상태의(resolved promise)로 값을 감싸 이행된 Promise가 반환되도록 합니다.
- await를 사용할 수 있습니다.

	기본 예시

```javascript
async function f() {
  return 1;
}

f().then(alert); // 1
```

	명시적 promise 반환 예시
```javascript
async function f() {
  return Promise.resolve(1);
}

f().then(alert); // 1
```

_둘의 결과는 동일합니다._

#### <span style='color:pink'>_즉, async가 붙은 함수는 반드시 프라미스를 반환하고, 프라미스가 아닌 것은 프라미스로 감싸 반환합니다. _</span>

---
### await

> <span style='color: orange'>특징</span>
- async 함수 내에서만 동작합니다.
- await를 만나면 Promise가 처리될 때까지 기다립니다.
- Promise가 처리되길 기다리는 동안, 엔진이 다른 일(다른 스크립트를 실행, 이벤트 처리 등)을 할 수 있기 때문에, CPU 리소스가 낭비되지 않습니다.
- ‘thenable’ 객체를 받습니다.

	기본 문법
    
```javascript
async function f() {

  let promise = new Promise((resolve, reject) => {
    setTimeout(() => resolve("완료!"), 1000)
  });

  let result = await promise; // 프라미스가 이행될 때까지 기다림 (*)

  alert(result); // "완료!"
}
f();
```
><span style='color: red'>주의</span>
- await는 최상위 레벨 코드에서 작동하지 않습니다.
- 익명 async 함수로 코드를 감싸면 최상위 레벨 코드에도 await를 사용할 수 있습니다.


```javascript
// 최상위 레벨 코드에선 문법 에러가 발생함
let response = await fetch('/article/promise-chaining/user.json');
let user = await response.json(); (X)


(async () => {
  let response = await fetch('/article/promise-chaining/user.json');
  let user = await response.json();
  ...
})(); (O)
```


	 
promise.then처럼 await에도 thenable 객체(then 메서드가 있는 호출 가능한 객체)를 사용할 수 있습니다. thenable 객체는 서드파티 객체가 프라미스가 아니지만 프라미스와 호환 가능한 객체를 제공할 수 있다는 점에서 생긴 기능입니다. 서드파티에서 받은 객체가 .then을 지원하면 이 객체를 await와 함께 사용할 수 있습니다.


```javascript
class Thenable {
  constructor(num) {
    this.num = num;
  }
  then(resolve, reject) {
    alert(resolve);
    // 1000밀리초 후에 이행됨(result는 this.num*2)
    setTimeout(() => resolve(this.num * 2), 1000); // (*)
  }
};

async function f() {
  // 1초 후, 변수 result는 2가 됨
  let result = await new Thenable(1);
  alert(result);
}

f();
```


### 요약 
> 1. 함수는 언제나 프라미스를 반환합니다.
2. 함수 안에서 await를 사용할 수 있습니다.
3. Promise 앞에 await 키워드를 붙이면 자바스크립트는 Promise가 처리될 때까지 대기합니다.
4. 처리가 완료되면 조건에 따라 아래와 같은 동작이 이어집니다.
		1) reject : 예외가 생성됨(에러가 발생한 장소에서 throw error를 호출한 것과 동일(try~catch 혹은 .catch를 사용하여 에러 처리)
        2) resolve : Promise 객체의 resolve값을 반환
5. 가독성을 높이고 코드가 간결해집니다.



