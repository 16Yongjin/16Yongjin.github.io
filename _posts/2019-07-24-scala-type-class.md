---
id: 940
title: Scala Type Class
date: 2019-07-24T20:10:05+09:00
layout: default
author: yongjin0802
permalink: /2019/07/24/scala-type-class/
categories:
  - Scala
tags:
  - Functional Programming
  - Scala
---
### 스칼라 타입 클래스 패턴은 3가지다.

  1. 타입 클래스
  2. 타입 클래스 인스턴스
  3. 타입 클래스 인터페이스(메서드)

+ 4. 3번 대신 인터페이스 신택스를 사용할 수 있다.

### 1. 타입 클래스

일단 이건 JSON 추상문법트리를 나타낸 것이다.

<pre class="scala" style="font-family:monospace;"><span style="color: #0000ff; font-weight: bold;">sealed</span> <span style="color: #0000ff; font-weight: bold;">trait</span> Json
<span style="color: #0000ff; font-weight: bold;">final</span> <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #0000ff; font-weight: bold;">class</span> JsObject<span style="color: #F78811;">&#40;</span>get<span style="color: #000080;">:</span> Map<span style="color: #F78811;">&#91;</span>String, Json<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">extends</span> Json
<span style="color: #0000ff; font-weight: bold;">final</span> <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #0000ff; font-weight: bold;">class</span> JsString<span style="color: #F78811;">&#40;</span>get<span style="color: #000080;">:</span> String<span style="color: #F78811;">&#41;</span>            <span style="color: #0000ff; font-weight: bold;">extends</span> Json
<span style="color: #0000ff; font-weight: bold;">final</span> <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #0000ff; font-weight: bold;">class</span> JsNumber<span style="color: #F78811;">&#40;</span>get<span style="color: #000080;">:</span> Double<span style="color: #F78811;">&#41;</span>            <span style="color: #0000ff; font-weight: bold;">extends</span> Json
<span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #0000ff; font-weight: bold;">object</span> JsNull                                <span style="color: #0000ff; font-weight: bold;">extends</span> Json</pre>

이 trait가 **타입 클래스**이다. &#8220;JSON으로 직렬화하기&#8221;라는 행동을 나타낸다. 

<pre class="scala" style="font-family:monospace;"><span style="color: #0000ff; font-weight: bold;">trait</span> JsonWriter<span style="color: #F78811;">&#91;</span>A<span style="color: #F78811;">&#93;</span> <span style="color: #F78811;">&#123;</span>
  <span style="color: #0000ff; font-weight: bold;">def</span> write<span style="color: #F78811;">&#40;</span>value<span style="color: #000080;">:</span> A<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Json
<span style="color: #F78811;">&#125;</span></pre>

### 2. 타입 클래스 인스턴스

 **타입 클래스 인스턴스**는 타입 클래스를 구체적인 타입(ex: String, Person)을 가지고 구현한거다.

implicit 키워드를 앞에 붙인다. 

<pre class="scala" style="font-family:monospace;">&nbsp;
<span style="color: #0000ff; font-weight: bold;">final</span> <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #0000ff; font-weight: bold;">class</span> Person<span style="color: #F78811;">&#40;</span>name<span style="color: #000080;">:</span> String, email<span style="color: #000080;">:</span> String<span style="color: #F78811;">&#41;</span>
&nbsp;
<span style="color: #0000ff; font-weight: bold;">object</span> JsonWriterInstances <span style="color: #F78811;">&#123;</span>
  <span style="color: #0000ff; font-weight: bold;">implicit</span> <span style="color: #0000ff; font-weight: bold;">val</span> stringWriter<span style="color: #000080;">:</span> JsonWriter<span style="color: #F78811;">&#91;</span>String<span style="color: #F78811;">&#93;</span> <span style="color: #000080;">=</span>
    <span style="color: #0000ff; font-weight: bold;">new</span> JsonWriter<span style="color: #F78811;">&#91;</span>String<span style="color: #F78811;">&#93;</span> <span style="color: #F78811;">&#123;</span>
      <span style="color: #0000ff; font-weight: bold;">def</span> write<span style="color: #F78811;">&#40;</span>value<span style="color: #000080;">:</span> String<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Json <span style="color: #000080;">=</span> JsString<span style="color: #F78811;">&#40;</span>value<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
&nbsp;
  <span style="color: #0000ff; font-weight: bold;">implicit</span> <span style="color: #0000ff; font-weight: bold;">val</span> personWriter<span style="color: #000080;">:</span> JsonWriter<span style="color: #F78811;">&#91;</span>Person<span style="color: #F78811;">&#93;</span> <span style="color: #000080;">=</span>
    <span style="color: #0000ff; font-weight: bold;">new</span> JsonWriter<span style="color: #F78811;">&#91;</span>Person<span style="color: #F78811;">&#93;</span> <span style="color: #F78811;">&#123;</span>
      <span style="color: #0000ff; font-weight: bold;">def</span> write<span style="color: #F78811;">&#40;</span>value<span style="color: #000080;">:</span> Person<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Json <span style="color: #000080;">=</span>
        JsObject<span style="color: #F78811;">&#40;</span>
          Map<span style="color: #F78811;">&#40;</span>
            <span style="color: #6666FF;">"name"</span>  -<span style="color: #000080;">&gt;</span> JsString<span style="color: #F78811;">&#40;</span>value.<span style="color: #000000;">name</span><span style="color: #F78811;">&#41;</span>,
            <span style="color: #6666FF;">"email"</span> -<span style="color: #000080;">&gt;</span> JsString<span style="color: #F78811;">&#40;</span>value.<span style="color: #000000;">email</span><span style="color: #F78811;">&#41;</span>
          <span style="color: #F78811;">&#41;</span>
        <span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span></pre>

### 3. 타입 클래스 인터페이스

사용자가 사용할 기능을 나타낸다.

타입 클래스 인스턴스를 implicit 매개변수로 받는다. 

<pre class="scala" style="font-family:monospace;"><span style="color: #0000ff; font-weight: bold;">object</span> Json <span style="color: #F78811;">&#123;</span>
  <span style="color: #0000ff; font-weight: bold;">def</span> toJson<span style="color: #F78811;">&#91;</span>A<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#40;</span>value<span style="color: #000080;">:</span> A<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#40;</span><span style="color: #0000ff; font-weight: bold;">implicit</span> w<span style="color: #000080;">:</span> JsonWriter<span style="color: #F78811;">&#91;</span>A<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Json <span style="color: #000080;">=</span>
    w.<span style="color: #000000;">write</span><span style="color: #F78811;">&#40;</span>value<span style="color: #F78811;">&#41;</span>
<span style="color: #F78811;">&#125;</span></pre>

이렇게 사용한다.

<pre class="scala" style="font-family:monospace;"><span style="color: #0000ff; font-weight: bold;">import</span> JsonWriterInstances.<span style="color: #000080;">_</span>
&nbsp;
Json.<span style="color: #000000;">toJson</span><span style="color: #F78811;">&#40;</span>Person<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">"Dave"</span>, <span style="color: #6666FF;">"dave@example.com"</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span></pre>

### 4. 인터페이스 신택스

기존 타입에 메서드를 확장할 때 쓴다.

자바 String같이 상속 불가능한 final 타입에 메서드를 추가할 때 쓸 수 있다. 

<pre class="scala" style="font-family:monospace;"><span style="color: #0000ff; font-weight: bold;">object</span> JsonSyntax <span style="color: #F78811;">&#123;</span>
  <span style="color: #0000ff; font-weight: bold;">implicit</span> <span style="color: #0000ff; font-weight: bold;">class</span> JsonWriterOps<span style="color: #F78811;">&#91;</span>A<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#40;</span>value<span style="color: #000080;">:</span> A<span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> toJson<span style="color: #F78811;">&#40;</span><span style="color: #0000ff; font-weight: bold;">implicit</span> w<span style="color: #000080;">:</span> JsonWriter<span style="color: #F78811;">&#91;</span>A<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Json <span style="color: #000080;">=</span>
      w.<span style="color: #000000;">write</span><span style="color: #F78811;">&#40;</span>value<span style="color: #F78811;">&#41;</span>
  <span style="color: #F78811;">&#125;</span>
<span style="color: #F78811;">&#125;</span></pre>

이렇게 사용한다.

<pre class="scala" style="font-family:monospace;"><span style="color: #0000ff; font-weight: bold;">import</span> JsonWriterInstances.<span style="color: #000080;">_</span>
<span style="color: #0000ff; font-weight: bold;">import</span> JsonSyntax.<span style="color: #000080;">_</span>
&nbsp;
Person<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">"Yongjin"</span>, <span style="color: #6666FF;">"yongjin@example.com"</span><span style="color: #F78811;">&#41;</span>.<span style="color: #000000;">toJson</span></pre>

### 추가로

아래처럼 생긴 implicitly 함수로 implicit scope를 확인 가능하다.

<pre class="scala" style="font-family:monospace;"><span style="color: #0000ff; font-weight: bold;">def</span> implicitly<span style="color: #F78811;">&#91;</span>A<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#40;</span><span style="color: #0000ff; font-weight: bold;">implicit</span> value<span style="color: #000080;">:</span> A<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> A <span style="color: #000080;">=</span> value</pre>

또한 implicit scope에 타입 클래스 인스턴스는 한 개만 있어야 컴파일러가 implicit 값을 잘 찾을 수 있다.(에러가 안 난다)

#### 출처

<https://underscore.io/books/scala-with-cats/>