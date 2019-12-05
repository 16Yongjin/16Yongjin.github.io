---
id: 600
title: 코틀린 기본 문법
date: 2017-11-10T20:55:19+09:00
author: yongjinsite

guid: https://yongjinsite.wordpress.com/?p=600
permalink: '/2017/11/10/%ec%bd%94%ed%8b%80%eb%a6%b0-%ea%b8%b0%eb%b3%b8-%eb%ac%b8%eb%b2%95/'
categories:
  - 기타
---
코틀린 클래스는 생성자 함수가 자동으로 생성된다.

생성자 함수 바디를 가지기 위해서는 init {} 함수를 사용한다.

<pre>public class Person (var name:String?) {
    init {
      if (name.isNullOrBlank()) name ="No name"
    }
}</pre>

get/set함수는 field라는 키워드로 변수에 접근하고 변경해야 한다.

<pre>class Person {
    var name: String = "Json"
    get() = "Name: ${field}"

    var age: Int = 0
    set(age) { field = age }
}

</pre>

접근 제한자는 private, protected, internal, public 이렇게 4가지이다.

internal은 같은 모듈 내 접근을 허락하는 것이다.

접근 제한자가 없으면 public으로 선언된다.

함수는 기본적으로 final로 선언되며 오버라이드 허용을 위해서는 앞에 open을 붙여야 한다.

sealed 키워드는 같은 .kt 파일 내 클래스에만 상속을 허용한다.

익명 클래스 생성 시 object라는 객체로 선언해준다.

public 함수에서 object를 리턴할 때, object가 Any로 변경된다.

즉, 함수가 리턴값이 없는 것으로 변경되며 반환된 object 내부의 값을 참조할 수가 없게 된다.

클래스 내부에서 선언된 값에 외부 접근을 막기 위함이다.