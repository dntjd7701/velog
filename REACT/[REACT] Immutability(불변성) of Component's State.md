### 기본 개념
1. 절대 컴포넌트의 상태를 직접적으로 변화 시켜서는 안된다.
2. 컴포넌트의 상태는 불변적으로 다루어야한다.
3. 항상 setState, useState Hook 함수 호출에서 반환하는 setter를 사용한다.

### 이유
1. 직접적으로 this.state를 변경하면 React의 상태 관리를 우회하게 된다. 
	-> 이러한 요소들은 React 원리를 어기는 것이 되고, 어플리케이션의 오작동을 유발할 수 있다.
2. this.state를 직접 조작한 내용은 this.setState 호출로 무효화가 된다.
3. 나중에 성능 개성의 여지가 없다. 

	- 객체의 동변경 유무 검사 시 객체의 동질성 비교 -> 고비용
    - 객체의 동변경 유무 검사 시 객체의 동일성 비교 -> 저비용


### 결론

> 변경하지 말고 교체하라 !!

	주의 !) 함수형 프로그래밍을 지원하는 자바스크립트에서는 위의 내용이 표준이 아니다. 
	->  의도치 않게 변경할 가능성이 있다.
    

### Violation Example

```jsx
this.setState({
  emails: [{}, {}, {}]
});

const emails = this.state.emails;
emails.push({});

//this.setState({
//  emails: [...this.state.emails, {}]
//});
```
- setEmails([...messages ...json.data])


	- Array.prototype.concat(),concat() 메서드는 인자로 주어진 배열이나 값들을 기존 배열에 합쳐서 새 배열을 반환합니다. 

---

### How I
1. 비파괴 배열 메소드 및 연산자 :** map, filter, concat, ...(spread)**
2. [src/01](https://github.com/dntjd7701/react-practice/blob/main/component/ex06/src/01.js)

### How II
1. Object.assign을 이용하여 변경이 적용된 새로운 객체를 생성하는 방법
2. [src/02](https://github.com/dntjd7701/react-practice/blob/main/component/ex06/src/02.js)
3. [src/03](https://github.com/dntjd7701/react-practice/blob/main/component/ex06/src/03.js)


### Nested Object ***
1. **I, II**는 Nested Object가 있는 경우 까다롭다.
	- Object.assign은 deep copy를 지원 하지 않는다.(reference만 받는다.)
    - deep clone은 고비용이다.
    - 직접 하는 방법은 관리가 어렵고 코드에 실수가 있을 수 있다. 
    
2. 자바스크립트 언어적 특징 때문에 할 수 없다.
3. React Addon에 복잡하고 중첩된 객체의 변경을 도와주는 immutality helper를 사용한다.

5. [src/04](https://github.com/dntjd7701/react-practice/blob/main/component/ex06/src/04.js)

> 설치 

```bash
$ npm i react-addons-update
```

```jsx
import update from 'react-addons'update';


const newObject = update(objectInState, { [where]: { [what}: updateValue });
```
- what 명령
**	1) $push** [배열 요소 추가]
    2) $splice
    3) $unshift
**  4) $set ** [속성 변경]
	5) $merge
    6) apply
