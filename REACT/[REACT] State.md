
[자세한 코드 보기 ](https://github.com/dntjd7701/react-practice/tree/main/component)

### ex04: Component - React State

#### 01. 기본개념
#### 02. 제어 컴포넌트 /  비제어 컴포넌트(Anti-Pattern
#### 03. 상태(Stateful) 컴포넌트 vs Pure Component(바보, Dumb)
#### 04. Data Flow(Bottom-Up)

#### Run examples
```bash
$ npm run debug src={no}
```


---
### 01. 기본개념

>  State 란

- 컴포넌트 내부의 현재 상태를 나타내는, 쓰기 가능한 관리 데이터
	
    - 데이터의 형식은 상관 없다.

- 상태의 변경은 UI를 다시 **랜더링** 하게 한다.
- 클래스 컴포넌트에서는 contructor에서 default 값 세팅으로 생성한다.
- 함수 컴포넌트에서는 useState라는 후크 함수를 사용해서 초기화 한다. 
- 대체적으로 사용자 이벤트로 변경되거나 통신으로 변경된다.
- 컴포넌트는 this.state안에 여러 데이터를 가질 수 있다.(class component)
- this.state는 특정 컴포넌트 전용 데이터이며 변경을 위해서는 setState() 함수를 사용한다.(class component)
- 상태가 업데이트되면 컴포넌트의 반응형(Reactive) Rendering이 트리거가 되고 컴포넌트와 자식 컴포넌트가 다시 렌더링 된다.
	
    + 컴포넌트 내부의 state은 최소한으로 유지하는 것이 좋다.
    + 컴포넌트 내부의 state을 외부에 정확하게 나타내고 인터페이스의 동기화를 위해서 다시 렌더링한다.
- 컴포넌트가 동작(event)과 상호작용을 수행할 수 있는 메커니즘을 제공한다.
- 부모의 상태(State)가 변하면 자식을 포함하여 다시 랜더링한다.
- Top-Down property 전달은 Data Flow의 정형화된 방법이다.
- Bottom-Up Flow로 데이터 전달을 원할 때에는 property가 아닌 callback 함수를 사용한다.

- 컴포넌트 구조화를 잘 설계해야 하는 이유, state Component를 관련 있는 컴포넌트들로 묶어 부모화한다. 하나의 state Component에 모두 올려버리게되면 rendering되는 범주가 넓어지므로, 부분적으로 wrapping 처리를 잘해서 처리해야한다.** rendering되는 부분이 세분화되어 최대한 구조화하는 것이 좋다.**

> 예제 

_begin(초기값) step(증가치) 를 props로 넘겨 이벤트 발생시 초기값이 증가하는 예제
_ 
 
 
 1. Class Component
 
 	- 클래스형에서는 props를 constructor에서 세팅할 수 있다.
    - state는 꼭 객체로 값을 세팅해야한다.
---    
    
```jsx
import React, {Component} from 'react';

export default class extends Component{
    constructor(){
        super(...arguments);
        this.state = {
            value: this.props.begin
        }
    }
    onClickEventHandler() {
        // this.state.value = this.state.value + this.props.step
        // 위와 같이 하면 렌더가 되지 않는다. 

        this.setState({
            value: this.state.value + this.props.step
        });
    }
    render(){
        return(
            <div>
                <button onClick={ this.onClickEventHandler.bind(this) }>
                    <strong>+</strong>
                </button>
                { '  ' }
                <span>{ this.state.value }</span>
            </div>
        )
    }
}

```
 
 2. function Component
 
 	- useState라는 후크 함수 사용
	- 후크 함수는 값에 접근할 수 있는 이름과, 값을 변경할 수 있는 함수를 던져준다.

---

```jsx
import React, { useState } from 'react';

export default function({ begin, step }){
    const [ value, setValue ] = useState(begin); 
// 값에 접근할 수 있는 이름과, 값을 변경할 수 있는 함수를 던져준다.
// 배열의 객체 분해를 활용한다.
// props 또한 객체 분해를 활용하여 가독성을 높인다. 

    const onClickEventHandler = function() {
        setValue( value + step );
    }

return(
    <div>
        <button onClick={ onClickEventHandler }>
            <strong>+</strong>
        </button>
        { '  ' }
        <span>{ value }</span>
    </div>
)
}
```

---

### 02. 제어 컴포넌트

- form의 입력값은 제어를 할 수 있도록 하는것이 좋다. 
- `<input>, <textarea>, <option>`과 같은 폼 컴포넌트 중에 사용자 입력에 따라 state값이 변경되고 렌더링하는 컴포넌트를 제어(Controlled) 컴포넌트라고 한다.
- 폼 컴포넌트가 반드시 제어 컴포넌트로 작성해야 하는 것은 아니다. 상태를 제어하지 않는 비제어 컴포넌트로도 만들 수 있다.(Anti-Pattern)
- 폼 컴포넌트를 제어 컴포넌트로 만드는 것은 조금 복잡해 보이지만 다음과 같은 장점이 있다.
	
    + 컴포넌트의 인터페이스를 외부에서 직접 변경할 수 없고, 내부의 상태 변경으로 가능하다는 react의 컴포넌트 작성 원칙을 준수할 수 있다. 
    + Validation을 할 수 있다. 
    
---

> [src/02] 제어 컴포넌트

- font-awesome 사용
- [font-awesome 참고](https://velog.io/@dntjd7701/React-Font-Awesome-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0)

```jsx
import React, { useState } from 'react';
import './assets/Form.css';
import { FontAwesomeIcon } from "@fortawesome/react-fontawesome";
import { faCheckCircle, faTimesCircle } from '@fortawesome/free-solid-svg-icons';

export default function Form() {
    const [name, setName] = useState('');
    const [email, setEmail] = useState('');
    const [validEmail, setValidEmail] = useState(false);
    const [password, setPassword] = useState('');
    const [gender, setGender] = useState('female');
    const [bithYear, setbirthYear] = useState(1984);
    const [selfDescription, setSelfDescription] = useState('');
    const [agreeProv, setAgreeProv] = useState('no');


    const onChangeInputName = function(e) {
        // setName(e.target.value);
        // 10 자 제한(Validation)
        setName(e.target.value.substr(0,10));
    }
    const onChangeInputEmail =  function (e){
        setEmail(e.target.value);

        const re = /[0-9a-zA-Z]([-_.]?[0-9a-zA-Z])*@[0-9a-zA-Z]([-_.]?[0-9a-zA-Z])*.[a-zA-Z]$/i;
        // Ajax
        // const result = await fetch('/user/emailcheck?email' + e.target.value);
        // setValidEmail(!result.data);
        setValidEmail(re.test(e.target.value));
    }
    const onChangeInputPassword = function(e){
        setPassword(e.target.value.substr(0,10));
    }

    const onChangeInputGender = function (e){
        setGender(e.target.value);
    }

    const onChangeInputProv = function (e){
    //    API 호출
        const url = `/prov/agree?status=${e.target.value === 'no' ? 'yes' : 'no'}`;
        console.log(url);
        if(true){
            setAgreeProv(e.target.value === 'no' ? 'yes' : 'no');
        }
    }

    return (
        <form id="joinForm" name="joinForm" method="post" action="/do/not/post">
            {/* name */}
            <label htmlFor="name">이름</label>
            <input id="name" name="name" type="text" value={name} onChange={onChangeInputName}/>

            {/* email */}
            <label htmlFor="email">이메일</label>
            <input id="email" name="email" type="text" value={email} onChange={onChangeInputEmail}/>
            {/* etc */}
            {
                email === '' ? null :
                    validEmail ?
                        <FontAwesomeIcon icon={faCheckCircle} style={{marginLeft: 5, color: 'blue'}} size='lg'/> :
                        <FontAwesomeIcon icon={faTimesCircle} style={{marginLeft: 5, color: 'red'}} size='lg'/>
            }

            {/* password */}
            <label htmlFor="password">패스워드</label>
            <input id="password" name="password" type="password" value={password} onChange={onChangeInputPassword}/>

            {/* gender, radio box */}
            <fieldset>
                <legend>성별</legend>
                <label>여</label> <input type="radio" name="gender" value={"female"} checked={gender === 'female'} onChange={ onChangeInputGender }/>
                <label>남</label> <input type="radio" name="gender" value={"male"} checked={ gender === 'male'} onChange={ onChangeInputGender }/>
            </fieldset>

            {/* select/options */}
            <label htmlFor="birthYear">생년</label>
            <select id="birthYear" name='birthYear' value={ bithYear } onChange={ e => setbirthYear(e.target.value) }>
                <option value={ 1984 }>1984년</option>
                <option value={ 1985 }>1985년</option>
                <option value={ 1986 }>1986년</option>
                <option value={ 1987 }>1987년</option>
                <option value={ 1988 }>1988년</option>
                <option value={ 1989 }>1989년</option>
                <option value={ 1990 }>1990년</option>
            </select>

            {/* textarea */}
            <label htmlFor="birthYear">자기소개</label>
            <textarea id='selfDescription' name='selfDescription' value={ selfDescription } onChange={ e => setSelfDescription(e.target.value.substr(0,50))}/>


            <fieldset>
                <legend>약관동의</legend>
                <input
                    id="agree-prov"
                    type="checkbox"
                    name="agreeProv"
                    value={ agreeProv }
                    checked={ agreeProv === 'yes'}
                    onChange={ onChangeInputProv }
                />
                <label>서비스 약관에 동의합니다.</label>
            </fieldset>

            <input type="submit" value="가입"/>
        </form>
    );
}
```


> [src/03] 비제어 컴포넌트 

---

###  03. 상태(Stateful) 컴포넌트 vs Pure Component(바보, Dumb)

1. Stateful Comonent

	- 상태(state)를 관리하는 컴포넌트
    - 보통 상태를 관리하는 컴포넌트는 컴포넌트 계층에서 상위에 있다.
    - Top -> Down
    - 보통 상태 컴포넌트는 순수 컴포넌트를 하나 이상 래핑할 수 있다. 
    
2. Pure Component 

	- 상태 관리없이 속성(props)으로 화면만 랜더링 하는 컴포넌트다.
    - 재사용이 용이하고, 테스트하기도 좋다. 
    
    
3. 애플리케이션의 컴포넌트들은 상태 컴포넌트와 순수 컴포넌트로 분리하여 만드는 것이 좋다.
4. 어떤 컴포넌트가 상태 컴포넌트인지 인지하는 방법()

	- 상태를 기반으로 랜더링 하는 컴포넌트
    - 많은 하위 컴포넌트들은 포함하고 있는 공통(하나)의 상위 컴포넌트
    - 컴포넌트 계층 구조에서(hierachy) 상위에 있고 상태를 가져야만 하는 컴포넌트
    - **_못 찾겠으면_**, 상태를 관리하는 컴포넌트를 만들고 하위(pure) 컴포넌트를 래핑한다.


> 예제) Emaillist(list part, props)

[emaillist](https://github.com/dntjd7701/react-practice/tree/main/component/ex04/src/04)

---

### 04. Data Flow(Bottom-Up)

1. 리액트 어플리케이션에서의 데이터는 컴포넌트 계층 Top->Down로 props 전달이 data flow 기본 매커니즘이다.
2. 킹치만, 거의 모든 애플리케이션에서는 Bottom-Up로 데이터를 전달해야 하는 경우가 반드시 있다. 

> 예제) Emaillist(search part, callback)


[emaillist](https://github.com/dntjd7701/react-practice/tree/main/component/ex04/src/04)


---
