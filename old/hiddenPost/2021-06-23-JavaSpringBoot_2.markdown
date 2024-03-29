---
layout: post
title: "Java SpringBoot(2) - View 환경설정"
date: 2021-06-23 10:00:00 +0100
categories:
---

# Java SpringBoot(2) - View 환경설정 & template engine

&nbsp;
&nbsp;
• **1. Welcome Page**

- Spring Boot는 static과 Template화 된 웰컴 페이지를 모두 지원한다. 먼저, Spring Boot는 지정된 정적 파일 위치에서 index.html을 찾아본다. 이 떄, 해당 위치에 파일이 존재하지 않으면 index 템플릿을 찾아보게 된다. 둘 중 하나라도 찾는 데 성공한다면 그 페이지가 자동으로 어플리케이션의 웰컴 페이지로 사용된다.

&nbsp;
• **2. controller & template**
&nbsp;

```java

    // [HelloController]

    package com.miguel.hellospring.controller;

    import org.springframework.stereotype.Controller;
    import org.springframework.ui.Model;
    import org.springframework.web.bind.annotation.GetMapping;

    @Controller // 컨트롤러임을 명시
    public class HelloController {

        @GetMapping("hello") // /hello 에 매핑
        public String hello(Model model){
            model.addAttribute("data", "hello!!"); // 'data'를 'hello!!'로 치환
            return "hello"; // template 'hello.html'을 찾아 해당 템플릿을 실행하라(render 하라) 는 것.
        }
    }
```

&nbsp;
&nbsp;
![SpringBoot Template structure](../../../../assets/images/template_structure.png)
&nbsp;

- 컨트롤러에서 리턴 값으로 문자를 반환하면, 뷰 리졸버(viewResolver)가 화면을 template에서 찾아 처리한다.
- 스프링 부트 템플릿엔진 기본 viewName 매핑 ->
  'resources:templates/'+{viewName}+'.html'
