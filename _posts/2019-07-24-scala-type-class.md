---
id: 940
title: Scala Type Class
date: 2019-07-24T20:10:05+09:00
author: yongjin0802
permalink: /2019/07/24/scala-type-class/
categories:
  - Scala
tags:
  - Functional Programming
  - Scala
---
# 스칼라 타입 클래스 패턴은 3가지다.

  1. 타입 클래스
  2. 타입 클래스 인스턴스
  3. 타입 클래스 인터페이스(메서드)

+ 4. 3번 대신 인터페이스 신택스를 사용할 수 있다.

# 1. 타입 클래스

일단 이건 JSON 추상문법트리를 나타낸 것이다.

```scala
sealed trait Json
final case class JsObject(get: Map[String, Json]) extends Json
final case class JsString(get: String)            extends Json
final case class JsNumber(get: Double)            extends Json
case object JsNull    
```

이 trait가 **타입 클래스**이다. &#8220;JSON으로 직렬화하기&#8221;라는 행동을 나타낸다. 

```scala
trait JsonWriter[A] {
  def write(value: A): Json
}
```

# 2. 타입 클래스 인스턴스

 **타입 클래스 인스턴스**는 타입 클래스를 구체적인 타입(ex: String, Person)을 가지고 구현한거다.

implicit 키워드를 앞에 붙인다. 

```scala
final case class Person(name: String, email: String)
 
object JsonWriterInstances {
  implicit val stringWriter: JsonWriter[String] =
    new JsonWriter[String] {
      def write(value: String): Json = JsString(value)
    }
 
  implicit val personWriter: JsonWriter[Person] =
    new JsonWriter[Person] {
      def write(value: Person): Json =
        JsObject(
          Map(
            "name"  -> JsString(value.name),
            "email" -> JsString(value.email)
          )
        )
    }
}
```

# 3. 타입 클래스 인터페이스

사용자가 사용할 기능을 나타낸다.

타입 클래스 인스턴스를 implicit 매개변수로 받는다. 

```scala
object Json {
  def toJson[A](value: A)(implicit w: JsonWriter[A]): Json =
    w.write(value)
}
```

이렇게 사용한다.

```scala
import JsonWriterInstances._
 
Json.toJson(Person("Dave", "dave@example.com"))
```

# 4. 인터페이스 신택스

기존 타입에 메서드를 확장할 때 쓴다.

자바 String같이 상속 불가능한 final 타입에 메서드를 추가할 때 쓸 수 있다. 

```scala
object JsonSyntax {
  implicit class JsonWriterOps[A](value: A) {
    def toJson(implicit w: JsonWriter[A]): Json =
      w.write(value)
  }
}
```

이렇게 사용한다.

```scala
import JsonWriterInstances._
import JsonSyntax._
 
Person("Yongjin", "yongjin@example.com").toJson
```

# 추가로

아래처럼 생긴 implicitly 함수로 implicit scope를 확인 가능하다.

```scala
def implicitly[A](implicit value: A): A = value
```

또한 implicit scope에 타입 클래스 인스턴스는 한 개만 있어야 컴파일러가 implicit 값을 잘 찾을 수 있다.(에러가 안 난다)

## 출처

<https://underscore.io/books/scala-with-cats/>