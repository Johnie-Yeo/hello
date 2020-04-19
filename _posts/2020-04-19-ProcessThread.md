---
layout: post
title:  "[OS] Process & Thread"
date:   2020-04-19
desc: "Process "
keywords: "OS, process, thread"
categories: [Computer-science]
tags: [OS, process, thread]
icon: icon-html
---

# Process와 Thread

>  개인적으로는 IT 직군 채용을 위한 기술면접의 단골 질문을 꼽을때 반드시 나오는 질문이 process와 thread에 대해 얘기해보라 인것 같습니다. 굉장히 기본을 묻는 것인데다 너무 전통적인 질문인데 언제까지 이걸 물어볼까 싶긴 하네요. 



## Process

`메모리에 적재되어 실행되고 있는 프로그램`을 말합니다. 

프로그램과 프로세스의 차이는 Java의 Class와 Instance의 관계와 유사하다고도 할 수 있습니다. 프로그램은 명령어 리스트를 가지고 디스트에 저장되어 있는 정적 파일이고 프로세스는 이 프로그램이 실행중인 작업을 의미합니다. 때문에 Java의 클래스가 여러 인스턴스를 만들어 낼 수 있는 것처럼, 하나의 프로그램으로 여러 프로세스를 띄울 수 있습니다.

프로세스는 운영체제로부터 시스템 자원을 할당받는 단위이기도 합니다. 프로그램이 실행되어 메모리에 적재될 때 Code(Text), Data, Stack, Heap 영역을 할당받으며 여기에 프로그램카운터를 포함하여 프로세스라고 합니다.



<img src="{{ site.img_path }}/process_thread/process.png" style="width:60vw;"/>

<br>

## Multi-process

하나의 응용프로그램을 여러개의 프로세스로 구성하여 각 프로세스가 하나의 작업을 처리하도록 하는 것입니다.

장점으로는 여러 자식 프로세스중 하나에 문제가 생겨도 각각의 독립적인 프로세스이기 때문에 나머지 프로세스에게는 절대 영향이 가지 않는다는 점입니다.

하지만 독립적인 환경은 단점을 불러오기도 합니다.

`Context Switching`으로 인한 오버헤드 때문인데요, Context Switching이란 CPU가 어떤 하나의 프로세스를 실행하고 있는 상태에서 인터럽트 요청에 의해 다음 우선 순위의 프로세스가 실행되어야 할 때 기존의 프로세스의 상태 또는 레지스터 값(Context)을 저장하고 CPU가 다음 프로세스를 수행하도록 새로운 프로세스의 상태 또는 레지스터 값(Context)을 교체하는 작업을 말합니다.

Context Switching이 일어나면 그 과정에서 캐시 메모리 초기화 등 비싼 작업이 진행됩니다. 프로세스는 모두 독립된 자원을 할당받았기 때문에 공유 메모리가 없어 Context Switching이 일어나면 캐시에 있는 데이터가 모두 리셋하고 다시 캐시 정보를 불러와야 하는 점때문에 오버헤드가 크다는 것입니다.

<br>

## Thread

간단히 말하면 `프로세스에서 실행되는 흐름의 단위` 입니다.

프로세스에서 실행되고 있는 여러 흐름의 최소 단위를 말하며 하나의 프로세스는 최소 하나의 스레드를 갖습니다.

Thread는 프로세스가 OS로부터 할당받은 자원을 이용하는 실행의 단위이기도 합니다.

Thread는 프로세스 내에서 각각의 stack만 따로 할당받고 code, data, heap은 Thread간 공유됩니다.

<img src="{{ site.img_path }}/process_thread/thread.png" style="width:60vw;"/>

<br>

## Multi-thread

하나의 응용프로그램을 여러개의 쓰레드로 구성하고 각 쓰레드가 하나의 작업을 처리하도록 하는 것을 말합니다.

멀티쓰레드의 장점은 시스템 자원 소모가 감소하여 **자원의 효율성**이 증대된다는 것입니다. 프로세스를 생성하여 자원을 할당하는 시스템 콜이 줄어들어 지원을 효율적으로 관리할수 있습니다.

또다른 장점은 시스템 처리량이 증가하여 **처리 비용이 감소** 한다는 것입니다. 쓰레드 간의 통신이 프로세스간의 통신보다 비용이 적습니다. 쓰레드는 프로세스 내의 Stack을 제외한 모든 메모리 영역을 공유하기 때문입니다. 또 스레드 사이의 작업량이 작아 Context Switching도 상대적으로 빠릅니다.

하지만 다음과 같은 단점도 있습니다.

구현이 쉬운 만큼 설계에 오류가 날 확률이 높아 상당히 많은 신경을 써야합니다.

디버깅이 어렵고 쓰레드 동기화 문제로 자원 공유의 문제가 발생할수 있습니다.

또 하나의 쓰레드에 문제가 발생하면 전체 프로세스에 영향이 간다는 점도 있습니다.

> 쓰레드 동기화란 작업들 간 수행 시기를 맞추는 것을 말합니다. 작업이 동시에 일어나거나 일정 간격을 두고 일어나도록 시간 간격을 조절하는 것입니다. 
>
> 공유자원을 동시에 접근하는 문제 해결등을 위해 필요합니다.

<br>

<br>

> #### Reference
>
> - [Process와 Thread의 차이](https://shoark7.github.io/programming/knowledge/difference-between-process-and-thread)
> - [프로세스(Process)와 스레드(Thread)](https://velog.io/@naljajm/프로세스Process와-스레드Thread-btk169s36j)
> - [프로세스와 쓰레드의 차이](https://juyoung-1008.tistory.com/47)
> - [OS - Context Switch(컨텍스트 스위치)가 무엇인가?](https://jeong-pro.tistory.com/93)
> - [스레드 동기화](https://skmagic.tistory.com/263)

