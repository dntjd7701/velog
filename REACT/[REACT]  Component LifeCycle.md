[자세한 코드 보기 ](https://github.com/dntjd7701/react-practice/tree/main/component)

[LifeCycle diagram 보기 ](https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)

### Class Component LifeCycle

1. **Mount LifeCycle**

	- constructor
    - getDerivedStateFromProps(nextProps, prevState): props로 받아온 값을 state에 동기화 한다.[react ver16.3]
    - render
    - ***componentDidMount***: 컴포넌트 생성을 마치고 첫 렌더링 작업이 끝난 후

    
![](https://images.velog.io/images/dntjd7701/post/c7ef121d-0c14-4100-bf4d-1fad929ec97b/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-08-05%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%2012.50.45.png)
    
    
![](https://images.velog.io/images/dntjd7701/post/5466217c-a714-4008-a3ee-b7f5d50b98e7/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-08-05%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%2012.51.42.png)
    

2. **Update LifeCycle**

    - getDerivedStateFromProps(): props로 받아온 값을 state에 동기화 한다.[react ver16.3]
    - shouldComponentUpdate(nextProps, nextState): state이 변경 되었을 때, 랜더링 여부를 결정한다.
    - render()
    - getSnapshotBeforeUpdate: render() 호출 후, DOM에 변화를 반영하기 직전에 호출
    - componentDidUpdate: DOM 업데이트가 끝난 직후, DOM 작업이 가능하다.
    

![](https://images.velog.io/images/dntjd7701/post/b8a51fc7-e803-4446-b4cc-d9ef2bd39464/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-08-06%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%2012.55.17.png)
    
    
3. **Unmount LifeCycle**

![](https://images.velog.io/images/dntjd7701/post/e05b6dba-21b2-484b-8902-39f803b22a21/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-08-06%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%2012.55.28.png)



4. 예제: [src/01](https://github.com/dntjd7701/react-practice/tree/main/component/ex05/src/01)


	moun가 될때의 함수의 흐름과 update, unmount될 때 각자 가지는 함수의 흐름을 LifeCycle이라고 한다. 
    
 > 코드 예제
 
 ```jsx
import React, { Component, useState } from 'react';

export default class LifeCycle extends Component {
    constructor() {
        super(...arguments);
        this.h3Ref = null;
        this.state = {
            color: null
        }
        // this.handColorChange = this.handleColorChange.bind(this);
        console.log(`[MOUNT-01]`);
    }

    /**
     *  nextProps: 다음 property 값이 가질 값을 예정함.
     *  props 로 받아온 값을 state 에 동기화.
     *   render() 는 발생하지 않는다.
     *   null 을 가질 경우 아무 것도 반환하지 않는다.
     */
    static getDerivedStateFromProps(nextProps, prevState) {
        console.log(`[MOUNT-02][UPDATE-01] : getDerivedStateFromProps(nextProps= ${nextProps.color}, prevState= ${prevState.color})`);
        return nextProps.color !== prevState.color ? nextProps.color : null;
    }

    /**
     *  state 이 변경 되었을 때, re-rendering 여부를 결정한다.
     *  현재 데이터: this.props, this.state
     *  변경될 데이터: nextProps, nextState
     *  로 접근이 가능하다.
     */
    shouldComponentUpdate(nextProps, nextState){
        console.log(`[UPDATE-02] : shouldComponentUpdate(${nextProps.color}, ${nextState.color})`);
        // if(nextProps === this.props || this.state === nextState){
        //     return false;
        // }
        return true;
    }

    render() {
        console.log(`[MOUNT-03][UPDATE-03] : render()`);
        return (
            <h3 style={{
                    width: 500,
                    height: 300,
                    backgroundColor: this.props.color
                }}
                ref={ (ref) => {this.h3Ref = ref;} }
                /**
                *
                */

            />
        );
    }


    /**
     *  render 메소드 호출 직후, DOM 에 변화를 반영하기 직전에 호출[v16.3]
     *  반환 값은 다음 메소드 componentDidUpdate() 의 3번째 파라미터로 전달된다.
     *  변경 전의 props, state 접근이 가능하다.
     *  주로 업데이트 직전의 값을 참고해서 할 일이 있을 때 오버라이딩한다.
     *
     * @param prevProps
     * @param prevState
     */

    getSnapshotBeforeUpdate(prevProps, prevState) {
        console.log(`[UPDATE-04] : getSnapshotBeforeUpdate(prevProps= ${prevProps.color},prevState= ${prevState.color})`);
        return prevProps.color !== this.state.color ? this.h3Ref.style.backgroundColor : null;
    }

    /**
     *  사용자가 변화된 UI를 확인,
     *  DOM 업데이트가 끝난 직후, DOM 작업이 가능하다.
     *  변경 전의 props,state 접근이 가능하다.
     * @param prevProps
     * @param prevState
     * @param snapshot
     */

    componentDidUpdate(prevProps, prevState, snapshot) {
        // const hexColor =
        // "10,20,30" -> [10,20,30] -> reduce('#' -> '#0a' -> '#0af5' -> '#0xf5ee')
        console.log(`[UPDATE-04] : componentDidUpdate(prevProps= ${prevProps.color},prevState= ${prevState.color}, snapshot= ${snapshot})`);
    }


    /**
     *  컴포넌트 생성을 마치고 첫 렌더링 작업이 끝난 후
     *  다른 자바스크립트 라이브러리 또는 프레임워크 함수 호출 또는
     *  1. 이벤트 등록
     *  2. 타이머 설정
     *  3. 네트워크 통신
     *  등을 할 수 있다.
     */
    componentDidMount() {
        console.log(`[MOUNT-04] : componentDidMount()`);
    }

    /**
     *  컴포넌트를 DOM 에서 제거 할 때, <br/>
     *  componentDidMount 에서 등록한 이벤트, 타이머, 직접 생성한 DOM 엘리먼트 등을 제거(Clean-Up)
     */

    componentWillUnmount() {
        console.log(`[UNMOUNT] : componentWillUnmount()`);
    }
}

```
 
 
 ---

### Function Component LifeCycle : Hook

1. Alternative 1 : getDerivedStateFromProps
2. After Rendering function(entire rendering)

	- 상태 변화 -> 렌더링 -> 함수
    
3. 어떤 특정 값의 변화에 반응하는 After Rendering function

	- 어떤 특정 상태값 변화 -> 렌더링 -> 함수

4. Alternative 2 : componentDidMount & componentWillUnmount 대체 
5. 예제 : [src/02](https://github.com/dntjd7701/react-practice/tree/main/component/ex05/src/02)


>  코드 : Hook


```jsx
import React, { Fragment ,useState, useRef, useEffect } from 'react';


export default function Hook({ color }){
    const [ boxColor, setBoxColor ] = useState(null);
    const [ title, setTitle ] = useState('');
    const h3Ref = useRef(null);

    /**
     *  1. Alternative 1 : getDerivedStateFromProps
     */
    if(boxColor !== color) {
        setBoxColor(color);
    }

    /**
     *  2. After Rendering function(entire rendering)
     *
     *  - Mount, Update 에 호출이 된다.
     *  - class component lifecycle(componentDidMount, componentDidUpdate)
     */
    useEffect( () => {
        console.log('After Rendering');
    });


    /**
     *  3. 어떤 특정 값(boxColor)의 변화에 반응하는 After Rendering function **
     *
     *   - 관심 분리
     */
    useEffect( () => {
        console.log('Update Color(DB) Using APIs...');
    }, [boxColor]);


    /**
     *  4. Alternative 2 : componentDidMount & componentWillUnmount 대체
     *
     *   -
     */
    useEffect( () => {
        console.log('After Mount(componentDidMount)');

        return (function(){
            console.log('After Unmount(componentWillUnmount)');
        }); // 함수 리턴 부분, componentWillUnmount

    }, []); // [] 자체로 componentDidMount 가 된다.


    return (
        <Fragment>
            <h3 style={{
                width: 500,
                height: 300,
                backgroundColor: color
            }}
                ref={h3Ref}
            />
            <input
                type='text'
                value={ title }
                onChange={ (e) => setTitle(e.target.value) }
            />
        </Fragment>
    );
}
```


> 코드 : App

```jsx
import React, { Fragment, useState } from 'react';
import Hook from "./Hook";

export default function App() {
    const [color, setColor] = useState('#000');
    // 랜더링이 다시 시작 되면서 변경된 값을 그대로 가지고 있다.(새로 초기값이 들어가는게 아닌.)
    const [showColorBox, setShowColorBox] = useState(true);

    return (
        <Fragment>
            <h2>ex05: Hook of Functional Component</h2>
            <button onClick={ () => setColor(`#${Math.floor(Math.random() * 16777215).toString(16)}`)}> change color</button>
            <br/>
            <br/>
            <input type='checkbox' value={ showColorBox } checked={ showColorBox } onChange={ () => setShowColorBox(!showColorBox) }/> Color Box 박스 보기

            {
                showColorBox ?
                <Hook color={color}/> :
                    null
            }
        </Fragment>
    );
}
```

---
