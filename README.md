<div align=center>

# reactStudy

</div>


<h4> 배열로 정해서 반복데이터 관리</h4>

#

    const coinPanelList = [
      {idx:0,         symbol: 'BNB',          imgPath: 'bsc'},
      {idx:0,         symbol: 'ETH',          imgPath: 'eth'},
      {idx:0,         symbol: 'KLAY',         imgPath: 'klay'},
    ]

정해주고

    Array(coinPanelList && coinPanelList.length)

코인판넬리스트에서 랭쓰 전부를 가져오겠다 함수 선언

    value={{
      isActive: idx == selectMarketIdx,
      symbol: coinPanelList[idx].symbol,
      img: coinPanelList[idx].imgPath,
    }}

symbol: coinPanelList[idx].000 

000안에 코인판넬리스트명을 적어주면 안에 정보를 가져온다

만약 위에 함수 값에 색상을 넣어주고싶다면 

위에 변수 뒤에 {idx:0,         symbol: 'BNB',          imgPath: 'bsc',       backcolor: '000'},
                          (구조)            (바꿀 컨텐츠)             (바꿀 컨텐츠)            (바꿀 컨텐츠)

을 넣어주고 벨류 값에 똑같이

      value={{
        isActive: idx == selectMarketIdx,
        symbol: coinPanelList[idx].symbol,
        img: coinPanelList[idx].imgPath,
        color: coinPanelList[idx].backColor

      }}

를 넣어주고 

해당되는 js페이지로 넘어가 const [backcolor, setBackcolor] = useState('')

를 입력한 뒤 useEffect(() => {
   if문 안에 setBackcolor(_data.value.color) ( 데이터 벨류 안에 컬러 값을 받아오겠다. )

}

그리고 style 문법 안에 backgroundColor: backcolor( 벨류값 이름 )을 입력하면 입력한 색상값 
순서대로 바뀌게 된다.

#

<h4>input 상태 관리하기</h4>

#

input 에 입력하는 값이 하단에 나타나게 하고, 초기화 버튼을 누르면 input 의 값이 비워지도록 구현을 해보자.

여기엔 생략되있지만 useState에 대해 배웠다, 이번에도 useState를 사용한다. input의 
' onChange ' 라는 이벤트를 사용하는데 이벤트에 등록하는 함수에서는 이벤트 객체 ' e '를 파라미터로 받아와서 사용할 수 있다. 이 객체의 e.target 은 이벤트가 발생한 DOM인 input DOM을 가르키게 된다. 이 DOM 의 value 값, 즉 e.target.value를 조회하면 현재 input에 입력한 값이 무엇인지 알 수 있다.

이 값을 useState 를 통해서 관리를 해주면 된다.
 
▼▼▼

    import React, { useState } from 'react';

    function InputSample() {
      const [text, setText] = useState('');

      const onChange = (e) => {
        setText(e.target.value);
      };

      const onReset = () => {
        setText('');
      };

      return (
        <div>
          <input onChange={onChange} value={text}  />
          <button onClick={onReset}>초기화</button>
          <div>
            <b>값: {text}</b>
          </div>
        </div>
      );
    }

    export default InputSample;

input의 상태를 관리할 때에는 input 태그의 value 값도 설정해주는 것이 중요하다. 그렇게 해야, 상태가 바뀌었을때 input의 내용도 업데이트 된다.

#

<h4>여러개의 input 상태 관리하기</h4>

#

지난 튜토리얼에서 우리는 input 상태를 관리하는 방법에 대해 알아보았다. 이번엔 input이 여러개 일때 어떻게 관리해야 하는지 알아보겠다.

input이 비어져 있을 때 인풋에 대한 설명을 보여주는 placeholder 값도 설정 해 보겠다.
기존에 만들었던 상태는 지우고, onChange와 onReset 함수는 비워라

      import React, { useState } from 'react';

      function InputSample() {
        const onChange = (e) => {
        };

        const onReset = () => {
        };


        return (
          <div>
            <input placeholder="이름" />
            <input placeholder="닉네임" />
            <button onClick={onReset}>초기화</button>
            <div>
              <b>값: </b>
              이름 (닉네임)
            </div>
          </div>
        );
      }

      export default InputSample;


#

<h4>isActive를 호출할 때 {({isActive})}를 입력해주면 직관적이지 않기 때문에 람다함수를 써주어야한다.</h4>

#

    {(_panel) => 
    _panel.isActive ? <MinusCircleOutlined style={{fontSize:'32px'}} /> : <PlusCircleOutlined style={{fontSize:'32px'}} />
    
▼▼▼

_panel이라는 람다함수를 써서 화살표 함수 뒤에 .isActive라고 다시 입력을 해주어야 직관적이다.
_panel의 isActive를 호출해 주겠다가 된다. 하지만 {({isActive})} 이렇게 써버리면 무엇을 호출해줄지 불명확하기 때문에 직관적이지가 않다.


#

<h4>로컬 깃 파일이 충돌 났을 경우</h4>

#

깃 파일이 충돌 났을 경우

▼▼▼

1. 충돌 파일을 선택하여 backup파일로 정리해놓는다.

2. 충돌 파일을 선택하여 Revert를 해서 서버에 마지막으로 commit되어있는 파일을 불러온다.

3. winmarge를 해서 두 파일을 비교해본다.
 (  어떤 것이랑 비교하는지 알기 위해 파일 순서 잘 기억해야 된다.  )

4. 수정 된 부분을 보고 어떤 것이 더 최근에 수정한 파일인지 비교한다. 
그리고 최근에 수정한 파일로 접목시킨다.

5. revart를 한 후 pull을 받아서 현재 서버에 저장 되어있는 commit을 받아온다. 


#

<h4>useState([])의 의미는 배열데이터를 비우겠다라는 뜻이다.</h4>

#

useEffect 를 사용 할 때에는 첫번째 파라미터에는 함수, 두번째 파라미터에는 의존값이 들어있는 배열(deps)을 넣는다. 만약에 deps 배열을 비우게 된다면, 컴포넌트가 처음 나타날때에만 useEffect에 등록한 함수가 호출된다. 그리고 useEffect 에서는 함수를 반환 할 수 있는데 이를 cleanup 함수라고 부른다. cleanup 함수는 useEffect 에 대한 뒷정리를 해준다고 이해하면 된다. deps 가 비어있는 경우에는 컴포넌트가 사라질 때 cleanup 함수가 호출된다.

컴포넌트가 마운트 됐을때 (처음 나타났을 때), 언마운트 됐을 때(사라질 때), 그리고 업데이트 될 때(특정 props가 바뀔 때) 특정 작업을 처리하는 방법에 대해 알아보겠습니다.

1. 화면이 처음 떴을때 실행.
    - deps에 [] 빈배열을 넣을 때.
    - life cycle중 componentDidmount처럼 실행
2. 화면이 사라질 때 실행(clean up함수).
    - componentWillUnmount처럼 실행
3. deps에 넣은 파라미터값이 업데이트 됐을때 실행.
    - componentDidUpdate처럼 실행.
    
#    

<h4>useRef hook</h4>

#

useRef hook은 dom을 선택하는 용도 외에도, 다른 용도가 한가지 더 있다, 바로 컴포넌트 안에서 조회 및 수정 할 수 있는 변수를 관리하는 것이다.

useRef로 관리하는 변수는 값이 바뀐다고 해서 컴포넌트가 리렌더링되지 않는다. 리액트 컴포넌트에서의 상태는 상태를 바꾸는 함수를 호출하고 나서 그 다음 렌더링 이후로 업데이트 된 상태를 조회 할 수 있는 반면, useRef로 관리하고 있는 변수는 설정 후 바로 조회 할 수 있다.

useMemo의 첫번째 파라미터에는 이떻게 연산할지 정의하는 함수를 넣어주면 되고, 두번째 파라미터에는 deps 배열을 넣어주면 되는데, 이 배열 안에 넣은 내용이 바뀌면, 우리가 등록한 함수를 호출해서 값을 연산해주고, 만약에 내용이 바뀌지 않았다면 이전에 연산한 값을 재사용하게 된다.

useCallback은 지난 시간에 배웠던 useMemo와 비슷한 Hook이다
useMemo는 특정 결과값을 재사용 할 때 사용하는 반면, useCallback은 특정 함수를 새로 만들지 않고 재사용하고 싶을 때 사용한다.

#

<h4>prop의 기본 사용법</h4>

#

props

예를 들어서, App 컴포넌트에서 Hello 컴포넌트를 사용 할 때 name이라는 값을 전달해주고 싶다고 가정해 보자, 그러면 이렇게 코드를 작성하면 된다.

▼▼▼

<h4>App.js</h4>

    import React from 'react';
    import Hello from './Hello';

    function App() {
      return (
        <Hello name="react" />
      );
    }

    export default App;

이제 Hello 컴포넌트에서 name값을 사용 하고 싶을 땐 어떻게 하면 되는지 보자

<h4>Hello.js</h4>

    import React from 'react';

    function Hello(props) {
      return <div>안녕하세요 {props.name}</div>
    }

    export default Hello;

컴포넌트에서 전달되는 props 는 파라미터를 통하여 조회 할 수 있다. props 는 객체 형태로 전달되며, 만약 name 값을 조회하고 싶다면 props.name 을 조회하면 된다. 

여러개의 props, 비구조화 할당

Hello 컴포넌트에 또 다른 props 를 전달해보자. color 라는 값을 설정해보자

<h4>App.js</h4>

    import React from 'react';
    import Hello from './Hello';

    function App() {
      return (
        <Hello name="react" color="red"/>
      );
    }

    export default App;

    그 다음에는, Hello 컴포넌트에서 color 값을 조회해서 폰트의 색상으로 설정을 해보겠습니다.

    Hello.js

    import React from 'react';

    function Hello(props) {
      return <div style={{ color: props.color }}>안녕하세요 {props.name}</div>
    }

    export default Hello;

props 내부의 값을 조회 할 때 마다 props.를 입력하고 있는데, 함수의 파라미터에서 비구조화 할당 
(혹은 구조 분해라고도 부른다) 문법을 사용하면 조금 더 코드를 간결하게 작성 할 수 있습니다.

<h4>Hello.js</h4>

    import React from 'react';

    function Hello({ color, name }) {
      return <div style={{ color }}>안녕하세요 {name}</div>
    }

    export default Hello;




defaultProps 로 기본값 설정

컴포넌트에 props 를 지정하지 않았을 때 기본적으로 사용 할 값을 설정하고 싶다면 컴포넌트에 defaultProps라는 값을 설정하면 된다.

Hello.js

    import React from 'react';

    function Hello({ color, name }) {
      return <div style={{ color }}>안녕하세요 {name}</div>
    }

    Hello.defaultProps = {
      name: '이름없음'
    }

    export default Hello;


    한번 App에서 name 이 없는 Hello 컴포넌트를 렌더링해보자.

    App.js

    import React from 'react';
    import Hello from './Hello';

    function App() {
      return (
        <>
          <Hello name="react" color="red"/>
          <Hello color="pink"/>
        </>
      );
    }

    export default App;
