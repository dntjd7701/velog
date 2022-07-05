React를 사용하면서 에러를 방지하기 위해 원하는 props를 확실하게 확인하고 싶다면 PropType을 이용할 수 있다. 


	설치 : npm i prop-type
    
    
---
```jsx
import PropTypes from 'prop-types';

function Hero({name, skill, favouritNumber}){
  return (
    <h2>{name}</h2>
    <h3>{skill}</h3>
	<h3>{favouritNumber}</h3>
  )
}

Hero.propTypes = {
  name:PropTypes.string.isRequired,
  skill:PropTypes.string.isRequired,
  favouritNumber:PropTypes.number.isRequired
  .
  .
  .
  .
}

function App(){
  return(
	  <div>
      	<Hero name="Dr.Strange" skill="masic" favouritNumber=7 />
      </div>
  )
  
}
```

>주의 !
propTypes를 지정할때 Hero.propTypes와 같이 소문자로 지정해줘야 한다. (React가 읽지를 못함)

위와 같이 다양한 형식으로 지정하여 props를 받을 수 있다. 
지정한 형식에 맞지 않거나, isRequired 등의 형식에 맞지 않을 때 에러를 통해 확인할 수 있다. 이를 통해 버그 수정을 방지하고, 에러가 발생하더라도 더욱 쉽게 에러를 확인하고 수정할 수 있다. 

그 외, defaultProps 등의 지정도 가능하다.



Details : [React 공식 문서](https://ko.reactjs.org/docs/typechecking-with-proptypes.html#gatsby-focus-wrapper)
---
