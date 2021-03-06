---
title: 퍼사드 패턴
date: 2020-01-05T20:00:00+09:00
author: yongjin0802
categories:
  - Design Pattern
---

복잡한 인터페이스들을 쓰기 쉬운 하나의 인터페이스로 단순화한다.

서브시스템 클래스를 캡슐화하는 것이아니라 서브시스템의 기능을 이용할 수 있는 간단한 인터페이스를 제공한다.

그래서 서브클래스가 필요하다면 그냥 사용하면 된다.

인터페이스를 단순화시킬 뿐만 아니라 클라이언트와 복잡한 서브시스템을 **분리**시키는 역할을 한다.

## 클래스 다이어그램

퍼사드 패턴은 단순한 인터페이스를 통해서 서브시스템을 더 쉽게 사용하기 위한 용도로 사용되는 것을 알 수 있다.

![facade](https://user-images.githubusercontent.com/22253556/71778892-e2197180-2ff6-11ea-85b8-c63a527045db.png)

## 최소 지식 원칙

정말 친한 친구하고만 얘기하라.

어떤 객체든 상호작용하는 클래스의 개수에 주의해야 한다.

이 원칙을 따른다면 시스템의 한 부분을 변경했을 때 다른 부분까지 줄줄이 고쳐야 되는 상황을 미리 방지할 수 있다.

## 친구를 만들지 않으면서 다른 객체에 영향력을 행사하는 방법

다음 네 종류의 객체의 메서드만 호출하면 된다.

- 객체 자체
- 메소드에 매개변수로 전달된 객체
- 그 메서드에서 생성하거나 인스턴스를 만든 객체
- 그 객체에 속하는 구성요소

## 마무리

퍼사드 패턴은 어디서든 볼 수 있어서 구현은 넣지 않았다.

복잡한 로우레벨 API를 편하게 사용하도록 도와주는 유틸리티 라이브러리가 퍼사드 패턴에 속한다.

배민, 여기어때 같이 복잡한 소비과정을 단순화해서 우리의 삶을 편하게 하는 서비스들도 파사드에 속한다고 볼 수 있다.

컴퓨터 과학의 기초인 복잡한 것을 단순하게 추상화시키는 것에 파사드라는 이름을 붙이니 뭔가 있어보인다.
