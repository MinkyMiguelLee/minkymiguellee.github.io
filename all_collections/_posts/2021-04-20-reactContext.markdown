---
layout: post
title: "React - Context?"
date: 2021-04-20 17:44:00 +0100
categories: ["study", "React.js"]
---

• Context란?

> 일반적인 React 애플리케이션에서 데이터는 위에서 아래로 (즉, 부모로부터 자식에게) props를 통해 전달되지만, 애플리케이션 안의 여러 컴포넌트들에 전해줘야 하는 props의 경우 (예를 들면 선호 로케일, UI 테마) 이 과정이 번거로울 수 있다. context를 이용하면, 트리 단계마다 명시적으로 props를 넘겨주지 않아도 많은 컴포넌트가 이러한 값을 공유하도록 할 수 있다

• React를 활용해 기존에 개발/운영하던 M심의Bot 프로젝트의 리팩토링을 진행하면서, Component간 데이터를 주고 받아야 할 때. 특히 형제 Component간 데이터를 주고받기 위해서 상당히 번거로운 과정을 거쳐야 한다는 것을 알게 되었다.

> • callback function과 data를 props를 통해 자식인 A 컴포넌트에게 전달하고, 자식 컴포넌트가 데이터를 수정하고, 데이터가 수정된 시점에 부모 컴포넌트가 그 데이터를 또 다른 자식인 B 컴포넌트에게 전달하고...
> • 이럴 때 Context라는 개념을 사용하면 데이터를 주고 받을 때 위와 같은 번거로운 과정을 거치지 않아도 마치 전역 변수처럼 특정 블록단위 내에서 데이터를 자유롭게 공유할 수 있다.
> &nbsp; > &nbsp;

• 아직 사용해보지는 않았지만, Context를 사용해야 할 요인이 충분한 Component가 몇 개 있으니 해당 Component들에 Context를 적용할 예정이다.
&nbsp;
&nbsp;

• 사용해본 후 사용법과 후기를 작성해야겠다.
&nbsp;
&nbsp;
[reactJS Context](https://ko.reactjs.org/docs/context.html)
