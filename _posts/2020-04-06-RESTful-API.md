---
layout: post
title:  "RESTful API"
date:   2020-04-06
desc: "RESTful API의 정의와 진짜 RESTful API"
keywords: "BackEnd, api, network, http, rest, restful"
categories: [Back-end]
tags: [BackEnd, api, network, http, rest, restful]
icon: icon-html
---

REST가 뭘까요? REST api가 뭐죠? 그게 REST api 인가요?

평상시 이런 질문을 받았을 때는 꽤나 난감했습니다.

하나의 end point가 하나의 메세지를 내 놓는것? API 명세서가 있어야 하는 것? self descriptive 해야하는 것?

항상 헷갈렸고 명쾌한 답을 내놓기는 힘들었기에 정리해 봤습니다.

<br>

## REST 란

- **RE**presentational **S**tate **T**ransfer 의 약자

분산 하이퍼미디어 시스템(예: web)을 위한 아키텍쳐 스타일을 말합니다.

> 아키텍쳐 스타일 : 제약 조건의 집합



## RESTful API란

간단히 말해서 REST  아키텍쳐 스타일을 따르는 API를 RESTful API(REST api) 라 합니다.

즉 REST를 알아야 REST API가 뭔지 알게 되는 것입니다.



## RESTful API가 되기 위한 조건

- client - server
- stateless
- cache
- uniform interface
- layered system
- code-on-demand(*optional*)
  - 서버에서 코드를 클라이언트로 보내서 실행할 수 있어야 하는 것
    - 따라서 Javascript

오늘날의 대부분의 api는 위 조건들을 **거의** 잘 지키고 있는데 그 이유는 HTTP만 따라도 client-server, stateless, cache, layered system은 잘 지켜 지기 때문입니다. 

uniform interface가 가장 지켜지기 힘든데 이것도 하나의 스타일 입니다.



### Uniform Interface의 제약 조건

#### 1. Identification of resources

- 리소스가 uri로 식별되면 되는 것을 말합니다.

#### 2. Manipulation of resources through representations

- 리소스를 만들거나 업데이트 하거나 삭제할때 HTTP 메세지에 표현을 담아서 전송하는 것을 말합니다.

아래 2개는 현대 REST API들은 거의 모두가 지키지 못하고 있습니다. 사실상 대부분은 REST라고 우기는 상황인 것이죠.

#### 3. self-descriptive messages

- 메세지는 스스로를 설명해야 한다.

- example 1

  ```http
  GET / HTTP/1.1
  ```

  - 목적지가 빠져있어서 self descriptive 하지 못합니다.

  ```http
  GET / HTTP/1.1
  HOST : www.example.org
  ```

- example 2

  ```http
  HTTP/1.1 200 OK
  [{"op": "remove", "path": "/a/b/c" }]
  ```

  -  어떤 문법으로 작성됐는지 설명이 없기 때문에 self descriptive 하지 못합니다.

  ```http
  HTTP/1.1 200 OK
  Content-Type : application/json-patch+json
  [ { "op": "remove", "path": "/a/b/c" } ]
  ```

  - json-patch+json이라는 미디어 타입으로 정의된 명세라는 뜻입니다.
  - 오늘날의 대부분의 REST api들은 그냥 application/json이라고만 하지  어떻게 해석해야하는 지에 대한 명세를 나타내지 않음

#### 4. HATEOAS(Hypermedia As The Engine Of Application State)

- 애플리케이션의 상태는 hyperlink를 항상 통해서 전이되어야 한다.

----



- uniform interface가 필요한 이유
    - 독립적 진화를 하기 위해
    - 서버와 클라이언트가 각각 독립적으로 진화한다
    - 서버의 기능이 변경되어도 클라이언트를 업데이트 할 필요가 없다.
    - REST를 만들게 된 계기("How do I improve HTTP without breaking the Web?")


> #### Reference
> [![Video Label](http://img.youtube.com/vi/RP_f5dMoHFc/0.jpg)](https://youtu.be/RP_f5dMoHFc?t=0s)