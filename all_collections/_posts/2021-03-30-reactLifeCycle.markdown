---
layout: post
title: "React - Functional Style Lifecycle"
date: 2021-03-30 17:44:00 +0100
categories: ["study", "React.js"]
---

• class style react에서 render 완료 후의 작업을 위해 사용하는 componentDidUpdate,
componentDidMount와 같이, 함수형에서는 useEffect()를 사용할 수 있다.

```js
useEffect(function () {
  // useEffect는 첫 번째 인자로 함수를 받아야 한다.
});
```

• side effect는 여러 개를 사용할 수 있다.
&nbsp;
• clean up은 side effect가 다시 한 번 실행될 때 실행해야 하는 작업을 함수 형태로 정의하고,
이를 useEffect의 return 값으로 설정하면 이 return된 함수가 side effect가 두 번째
실행되는 순간 수행되는 것을 말한다.

```js
useEffect(function () {
  // useEffect가 처음 수행될 때엔 여기만 실행된다.
  return function cleanUp() {
    // useEffect가 두 번째 실행되는 순간, 이 부분에 정의한 작업이 수행된다.
    // 이 부분이 수행된 이후, useEffect의 바깥쪽 부분이 다시 수행되는 것.
    // 이 부분은 class style lifecycle의 componentWillUnmount와 동일한 개념이다.
  };
});
```

&nbsp;
• skipping effect를 통해 성능을 최적화할 수 있다. 이는 class style lifecycle의
shouldComponentUpdate와 동일한 개념이다.

```js
  useEffect(function(){
    return function cleanUp(){}
  }, [이 배열의 원소들이 이전과 달라졌을 때만 function()이 수행된다]);
```

&nbsp;
• skipping effect를 응용하여, component가 생성될 때만(componentDidMount일 때만)
실행되도록 side effect를 정의할 수 있다. 이 때, 이 side effect의 clean up은
componentWillUnmount와 동일하게 작동한다.

```js
// 이 side effect의 두 번째 인자, 즉 배열에 빈 배열을 전달하면 update일 때는
// 실행되지 않고 최초 1회만 실행된다.
useEffect(function () {
  return function cleanUp() {};
}, []);
```
