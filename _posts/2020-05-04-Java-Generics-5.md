---
layout: post
title:  "[Java] Generics - 5"
date:   2020-05-04
desc: "Java의 Generics에 대해 알아봅시다"
keywords: "Java, Generics, Inheritance, and Subtypes"
categories: [Language]
tags: [Java, Generics, Inheritance, and Subtypes]
icon: icon-html

---

# Generics, Inheritance, and Subtypes

Java에서는 타입간 호환되는 경우는 한 타입의 객체를 다른 타입의 객체에 할당 할 수 있습니다.

```java
Object someObject = new Object();
Integer someInteger = new Integer(10);
someObject = someInteger;   // OK
```

객체지향에서는 이러한 것을 "is a"관계라고 합니다. **Integer** *is a* **Object** 이므로 이러한 할당이 가능합니다. 하지만 Integer은 Number이기도 하기에 다음과 같은 코드도 가능합니다.

```java
public void someMethod(Number n) { /* ... */ }

someMethod(new Integer(10));   // OK
someMethod(new Double(10.1));   // OK
```

이러한 동작은 generics에서도 그대로 동작합니다. generic type 호출을 할때 Number을 type argument로 하며 Number와 호환된다면 어떠한 경우라도 add의 인자로 작동할 수 있습니다.

```java
Box<Number> box = new Box<Number>();
box.add(new Integer(10));   // OK
box.add(new Double(10.1));  // OK
```

이제 다음과 같은 메서드를 고려해 보겠습니다.

```java
public void boxTest(Box<Number> n) { /* ... */ }
```

이 경우에는 어떤 인자가 허용이 될까요? 보이는 그대로 타입이 Box<Number>인 단일 인자가 허용될 것입니다. 하지만 이것이 의미하는 바는 뭘까요? Box<Integer> 혹은 Box<Double>과 같은 것은 허용될까요? 정답은 `NO` 입니다. Box<Integer> 와 Box<Double>은 Box<Number>의 subtype이 아니기 때문입니다.

이거은 매우 generics 프로그래밍에서 일어나는 매우 흔한 오해이며 동시에 중요하게 배워야 할 개념입니다.

<p align="center"><img src="{{site.img_path}}/JavaGenerics/generics-subtypeRelationship.gif" style="width:50vw"/></p>

<p align="center">Integer가 Number의 subtype이라는 것은 Box&lt;Integer&gt;이 Box&lt;Number&gt;가 될수 있다는 것은 아닙니다.</p>

> #### Note
>
> 두 구체적인 타입 A, B(ex. Number & Integer)에서 MyClass<A>와 MyClass<B>의 관계는 A와 B의 관계와 상관이 없습니다.  MyClass <A> 와 MyClass <B>의 공통 상위클래스는 Object입니다.
>
> 두 타입 파라미터가 상관관계가 있을 때 두 generics를 subtype 관계로 만들고 싶다면 [Wildcards and Subtyping](https://docs.oracle.com/javase/tutorial/java/generics/subtyping.html)을 참조하세요.

<br>

### Generic Classes and Subtyping

generic 클래스 혹은 인터테이스를 subtype으로 만들고 싶다면 extend 혹은 implement 함으로써 만들수 있습니다. 클래스 혹은 인터페이스간의 타입 파라미터사이의 관계는 extends, implements에 의해 결정됩니다.

`Collections` 클래스를 예로 들겠습니다. ArrayList<E>는 List<E>를, List<E>는 Collection<E>를 각각 implements 합니다. 따라서 ArrayList<String>은 List<String>의 subtype이고 List<String>은 Collection<String>의 subtype입니다. type argument가 변경되지 않는 한, 타입간의 subtype 관계는 유지됩니다.

<p align="center"><img src="{{site.img_path}}/JavaGenerics/generics-sampleHierarchy.gif"/></p>

<p align="center">Collections의 hierarchy 예</p>

이제 list 인터페이스에서 **Payloadlist**라는 것을 정의할 것입니다. Payloadlist는 generic 타입 P의 값이 각각의 element와 결합합니다. Payloadlist는 다음과 같이 정의됩니다.

```java
interface PayloadList<E,P> extends List<E> {
  void setPayload(int index, P val);
  ...
}
```

PayloadList의 다음 파라미터화는 List <String>의 subtype입니다.

- PayloadList<String, String>
- PayloadList<String, Integer>
- PayloadList<String, Exception>

<p align="center"><img src="{{site.img_path}}/JavaGenerics/generics-payloadListHierarchy.gif" style="width:80vw"/></p>

<p align="center">Payloadlist hierarchy의 예</p>

<br><br>

> #### Reference
>
> - [Oracle : The Java Tutorials - Generics, Inheritance, and Subtypes](https://docs.oracle.com/javase/tutorial/java/generics/inheritance.html)

