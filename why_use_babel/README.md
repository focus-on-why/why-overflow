# Babel이란?

**`Babel`** 은 소스 코드를 **웹 브라우저가 처리할 수 있는 JavaScript 버전으로 변환해주는 무료 오픈 소스 JavaScirpt 트랜스컴파일러**이다. ECMAScript 2015+(ES6+) 코드를 이전 버전의 JavaScript로 변환하는데 주로 사용된다.

즉, 지원되지 않는 구문을 이전 버전과 호환되는 버전으로 변환한다. 최신 버전의 JavaScript 문법은 브라우저가 이해하지 못하기 때문에 `babel`이 브라우저가 이해할 수 있는 문법으로 변환해주는 것이다.    
<br>

## 예시

* ### 화살표 함수   
    `ES6`의 화살표 함수는 일반 함수 선언으로 변환한다. 

    ```javascript
    // Babel Input: ES2015 arrow function
    [1, 2, 3].map(n => n + 1);

    // Babel Output: ES5 equivalent
    [1, 2, 3].map(function(n) {
    return n + 1;
    });
    ```

* ### JSX   
    `JSX` 같은 비표준 JavaScript 구문도 변환할 수 있다. `babel`은 `create-react-app`에도 기본으로 들어있기 때문에 React로 개발을 한다면 자연스럽게 babel을 사용하게 된다. 

    `React` 코드가 브라우저에서 실행되기 전에 특정 방식으로 변경되어야 하는데, 이때 필요한 것이 `JSX`로 적은 코드를 브라우저가 이해할 수 있는 형태로 변경하는 것이다.

    ```jsx
    // Babel Input
    const Title = (
    <h3 id="title" onMouseEnter={() => console.log("mouse enter")}>
        Hello, I'm a title
    </h3>
    );

    const Button = (
    <button
        style={{
        backgroundColor: "tomato"
        }}
        onClick={() => console.log("im clicked")}
    >
        Click me
    </button>
    );

    // Babel Output
    "use strict";

    const Title = /*#__PURE__*/React.createElement("h3", {
    id: "title",
    onMouseEnter: () => console.log("mouse enter")
    }, "Hello, I'm a title");
    const Button = /*#__PURE__*/React.createElement("button", {
    style: {
        backgroundColor: "tomato"
    },
    onClick: () => console.log("im clicked")
    }, "Click me");
    ```     
<br>

## 주의사항

`Babel`은 코드가 ES5 환경에서 실행될 것이라고 가정하기 때문에 ES5 기능을 사용한다. 그래서 IE의 낮은 버전과 같이 ES5에 대한 지원이 제한되거나 불가능한 환경을 사용하는 경우 [@babel/polyfill](https://babeljs.io/docs/en/babel-polyfill)을 사용하면 지원이 가능하다.      
<br>

# 정리

`Babel`은 최신 버전의 JavaScript 문법을 브라우저가 이해할 수 있도록 이전 버전의 JavaScript(ES5)로 변환해준다. 따라서 Babel을 사용하면 ES6, ES7 등의 최신 문법을 사용할 수 있기때문에 생산성이 향상된다.    
<br>

# 참고

- [https://babeljs.io/docs/en/](https://babeljs.io/docs/en/)

- [https://en.wikipedia.org/wiki/Babel_(transcompiler)](https://en.wikipedia.org/wiki/Babel_(transcompiler))