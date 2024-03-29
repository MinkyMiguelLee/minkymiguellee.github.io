---
layout: post
title: "about node.js"
date: 2024-01-25 10:31:00 +0100
categories: ["study", "node.js"]
---

1. node.js 란?
   1. 오픈 소스 크로스 플랫폼 환경으로, 개발자로 하여금 클라이언트의 브라우저 밖에서 웹앱을 실행시킬 수 있도록 한다.
   2. node.js를 사용함으로써 서버사이드에서 웹앱을 생성할 수 있다
   3. 비디오 스트리밍 사이트와 같은 I/O 집약적인 웹앱을 사용할 수 있게 한다.
   4. Node.js는 이벤트 기반 모델을 사용하기 때문에 데이터 집약적인 애플리케이션을 위한 완벽한 솔루션이다.
   5. Node.js 는 Chrome V8 JavaScript 엔진으로 빌드된 JavaScript 런타임이다. Node.js는 이벤트 기반, 논 블로킹 I/O 모델을 사용해 가볍고 효율적이다. Node.js의 패키지 생태계인 npm은 세계에서 가장 큰 오픈 소스 라이브러리 생태계이기도 한다.
   6. Node js는 단일 Thread 이벤트 기반 모델 이다.
2. node.js를 사용하는 이유?
   1. Node.js는 앱 개발 회사가 확장 가능한 네트워크 프로그램을 쉽게 만들기 위해 사용하는 기술.
   2. 이러한 자바스크립트 런타임 환경을 사용함으로써 얻을 수 있는 장점은
      1. 데이터 타입 및 통합 프로그래밍 언어 제공
      2. 빠름
      3. 비동기적임
      4. 훌륭한 동시성
      5. 블록되지 않음
3. node.js의 주요 기능
   1. 싱글스레드이지만 확장 가능함
   2. 빠른 코드 실행
   3. 버퍼링이 없음
   4. MIT 라이센스
   5. Event driven
   6. 비동기 API
4. node.js의 작동 원리
   1. 클라이언트가 웹서버에 웹앱과의 상호작용을 시작하기 위한 요청을 전송함. 이러한 요청은 blocking 이거나 non-blocking으로 수행됨
   2. 데이터 쿼리
   3. 데이터 업데이트
   4. 데이터 삭제
   5. 들어온 모든 요청은 node.js가 받아 이벤트 큐에 추가한다
   6. 이벤트 루프에 의해 요청이 하나씩 처리된다. 여기서 요청이 간단한 요청인지, 외부 리소스를 요구하는지 하나씩 검사하고 확인한다.
5. event-driven 프로그래밍이란?
   1. 이벤트가 각각의 함수를 트리거링하도록 개발하는 프로그래밍 접근법
   2. 클릭, 타이핑 등 모든 것이 이벤트가 될 수 있다
   3. event-driven programming에서는 이벤트가 트리거될 때마다 등록되는 콜백 함수를 가진다
6. Thread 기반 vs. Event callback 방식
   1. Node.js는 Thread 풀을 가지긴 하나 애플리케이션 자체에는 Multi-thread 개념이 없다.
      1. 따라서 많은 처리를 위해 Event callback 방식을 사용한다
   2. **Thread 기반** 웹 모델은 요청이 웹 서버로 도착하면 현재 Thread 풀에 가용한 Thread에게 그 작업을 할당한다(Multi-Thread).
      1. 그리고 해당 요청에 대한 처리는 동일한 Thread에서 지속된다.
      2. 예를 들어, File을 받아오는 작업과 Data를 받아오는 작업이 있다고 하면 2개의 작업을 처리하기 위해 2개의 Thread가 생성이 되고 각각의 Thread에서 File을 받아오는 작업과 Data를 받아오는 작업을 처리하게 된다.
      3. 즉, Multi-Thread 방식은 서버의 요청 처리를 쓰레드에서 처리하도록 하여 병렬처리를 가능하도록 하는 방식이다.
      4. 쓰레드는 서버 CPU 자원을 시분할 형태로 나누어 가짐으로써 독립실행이 가능하며 다른 요청을 동시에 받을 수 있게 한다.
   3. 일반적으로 클라이언트의 요청마다 Thread를 발생시키다보니, 이 말은 동시 접속자 수가 많을 수록 Thread가 많이 발생한다는 의미이며 그만큼 메모리 자원도 많이 소모한다는 의미이다. 그러나 서버의 자원은 제한되어 있으므로 일정 수 이상의 Thread는 발생시킬 수 없다.
      1. 또한, 하나의 Thread에서 CPU를 사용하고 있다고 하면, 다른 Thread는 해당 작업이 끝날 때까지 기다려야 한다는 것이다. 즉, 동기적으로 일을 처리하게 된다.
   4. 이런 문제를 비동기처리로 처리하는게 Node js의 원리이다.
      1. 제어권을 다음 요청으로 바로 넘기기 때문에, IO 처리인 경우 Blocking 되지 않으며 다음 요청을 처리할 수 있다.
      2. 다시 정리해서, 단일 Thread를 사용하여 이벤트 루프를 도는데, 이벤트 큐(Task Queue)에 추가되어 있는 작업들을 순서대로 Thread에 할당해서 처리하는 방식이다.
      3. 클라이언트에서 요청이 들어오면 비동기 처리를 위해, 이벤트가 발생하고 서버의 이벤트 루프에 메시지 형태로 전달된다.
      4. 그러면, 이벤트 루프가 이를 처리할 동안, 제어권을 넘겨주고 다음 요청을 진행한다.
      5. 해당 요청이 완료되면 CallBack을 이용해, 완료 되었음을 알려준다.
7. Blocking vs. Non-blocking / Async vs. Sync
   1. **Blocking/non-blocking** 은 `제어권을 넘겨주는가 마는가`의 문제이다.
   2. **Async/Sync** 는 `작업이 완료되었다는 것을 신경 쓰는지 안쓰는지`의 차이이다.
   3. A에서 B를 호출했다고 하자, 그럴때 `B가 바로 제어권을 다시 A에게 넘겨준다면 non-blocking 이다`.
   4. 그러나, `B가 끝나고 나서 A에게 제어권을 다시 넘겨준다면 Blocking`이다.
   5. 즉 Node js는 요청이 왔을 때, 이벤트 루프에 이벤트를 주고난 후, 이벤트 루프가 바로 다음 요청에게 제어권을 넘겨주고 이벤트 루프는 해당 이벤트를 처리한다. 따라서 non-blocking 이라고 볼 수 있다.
   6. 또한, A에서 B를 호출할 때, A에서 callback을 넘겨주고 B가 작업을 완료한 후, callback을 실행하게 되고, A는 해당 완료를 신경쓰지 않는다면 Async 이다.
   7. 반면에, B가 모두 처리한 후 리턴하거나 만약 바로 제어권을 넘겨주었다하더라도 해당 처리가 끝났는지 계속해서 확인한다면 Sync이다.
   8. 즉, Node js의 경우 요청에 대한 처리를 이벤트루프가 완료하고 callback으로 처리한다음 끝이나기 때문에, Async라고 볼 수 있다.
8. 이벤트 큐 / 이벤트 루프 과정 정리
   1. 흔히, URL을 이용해 우리는 서버에 원하는 **요청** 을 하게 된다.
      1. URL은 Uniform Resource Locator
      2. URI는 Uniform Resource Identifier
   2. **REST API** 라는 네트워크 아키텍쳐를 사용했다고 할 때, 원하는 **행위(Verb)** 즉, HTTP Method에 따라, URI에 **표현(Representations)** 된 **자원(Resource)** 를 이용해, 만들어 둔 Routing이 시작되고, 담당하는 함수를 찾아 실행이 되기 시작한다. (해당사항도 **Event Loop** 가 실행한다. )
   3. 요청은 여러개가 들어올 수 있는데, 이는 **Socket Connection** 이라고 하며, Multiplexing으로 실행이 된다. 즉, 여러 개의 socket이 동시에 연결되어 있는 상태에서 하나의 Thread( **Event Loop** )는 어느 socket으로부터 메시지가 들어오는지 보다가, socket에서 메시지가 들어오면, 그 메시지를 꺼내 받아서 처리한다.
   4. 여기서 실행은 HTTP 모듈로 실행이 될 것인데, 이 자체가 비동기 함수이므로, 실행 할 때, 앞서 **Call Stack** 과 **Task Queue** 의 실행이 이루어진다. 예를 들면, 먼저 전역 Context에서 server.run이 실행되어 Listen 상태가 될 것이고, 요청이 들어왔을 때, 연결이 확립되었을 때 **Task Queue(Event Queue)** 로 **CallBack** 이 가면서 실행이 될 것이다. 그럼 내부 실행컨텍스트에 따라 콜 스택에 저장되며 실행이 된다.
   5. 실행이 될 때, Non-Blocking I/O의 동작이라면, Call Stack이 없어진다면 **Event Loop** 가 동작하며 Event를 처리할 것이고, Blocking I/O 의 경우, 예를 들면, **파일 읽기**, **데이터베이스 질의**, **소켓 요청**, **원격 서비스 접속** 과 같은 작업이 있으면, **Event Loop** 는 해당 작업을 **백그라운드의 Thread pool** 에서 하나의 Thread 꺼내어 그곳으로 보낸다.
   6. 그리고 그 Thread에서 작업이 끝나 Return되면, Thread는 **Event Queue** 에 CallBack을 주고 Release된다.

[dd0c8bbf-68fd-44e9-8b99-ce907c940e3a.pdf](notion://www.notion.so/minkymiguellee/about%20node%20js%203776221616864eac863736867eb91e0f/dd0c8bbf-68fd-44e9-8b99-ce907c940e3a.pdf)
