---
title: \[Rust\] 열거형과 패턴매칭
date: 2020-02-08T21:00:00+09:00
author: yongjin0802
categories:
  - Rust
---

하나의 타입이 가질 수 있는 값을 열거하는 열거형, 패턴에 따라 실행 흐름을 조절하는 `match`, 하나의 패턴만 매칭하는 `if let`

# 열거형

하나의 타입이 가질 수 있는 값을 열거한다.

## 열거형 정의하기

IP 주소 버전을 나타내는 `IpAddrKind`

```rust
enum IpAddrKind {
    V4,
    V6,
}
```

## 열거형 값

`IpAddrKind`의 인스턴스는 다음과 같이 만든다.

```rust
let four = IpAddrKind::V4;
let six = IpAddrKind::V6;
```

## 열거형에 직접 데이터 붙이기

열거형의 각 변종(variant)에 데이터를 넣어서 구조체 사용을 대신할 수 있다.

```rust
enum IpAddr {
    V4(u8, u8, u8, u8),
    V6(String),
}

let home = IpAddr::V4(127, 0, 0, 1);

let loopback = IpAddr::V6(String::from("::1"));
```

## 열거형과 구조체가 비슷한 점

아래와 같이 열거형을 정의하는 것은

```rust
enum Message {
    Quit,
    Move { x: i32, y: i32 },
    Write(String),
    ChangeColor(i32, i32, i32),
}
```

아래와 같은 구조체들을 정의하는 것과 같다.

```rust
struct QuitMessage; // 유닛 구조체
struct MoveMessage {
    x: i32,
    y: i32,
}
struct WriteMessage(String); // 튜플 구조체
struct ChangeColorMessage(i32, i32, i32); // 튜플 구조체
```

다만 이와 같이 여러 개의 구조체를 정의하면, 함수를 정의할 때 한 가지 인수로 받기 어렵다.

연관된 구조체들은 열거형으로 묶어주는게 좋다.

## 열거형 메서드

구조체처럼 열거형에도 메서드를 정의할 수 있다.

열거형 값을 가져오기 위해 `self`를 사용하는 것도 같다.

```rust
impl Message {
    fn call(&self) {
        // 메소드 내용은 여기 정의할 수 있습니다.
    }
}

let m = Message::Write(String::from("hello"));
m.call();
```

## Option 열거형

러스트에는 `null`이 없다.

대신, 값이 존재하거나 부재하는 것을 표현하기 위해 `Option<T>` 열거형을 사용한다.

```rust
enum Option<T> {
    Some(T),
    None,
}
```

# match 흐름 제어 연산자

패턴으로 값에 따라 코드를 수행할 수 있다.

패턴에 리터럴 값, 변수명, 와일드카드 등을 사용할 수 있다.

`match` 덕분에 컴파일러는 열거형의 모든 경우가 다뤄지는지 검사할 수 있다.

## `Option<T>`를 이용하는 매칭

아래는 `Option<i32>`를 파라미터로 받아서 값이 있으면 1을 더하는 `plus_one` 함수다.

값이 없으면 계산이 계속 `None` 값으로 진행된다.

```rust
fn plus_one(x: Option<i32>) -> Option<i32> {
    match x {
        None => None,
        Some(i) => Some(i + 1),
    }
}

let five = Some(5);
let six = plus_one(five);
let none = plus_one(None);
```

## 모든 가능성을 다루는 `match`

아래와 같이 위의 `plus_one` 함수에 `None` 케이스를 다루지 않으면

```rust
fn plus_one(x: Option<i32>) -> Option<i32> {
    match x {
        Some(i) => Some(i + 1),
    }
}
```

컴파일러는 `` non-exhaustive patterns: `None` not covered ``에러를 낸다.

## `_` 플레이스홀더

가능한 값 모두를 나열하고 싶지 않다면 `_` 패턴을 사용한다.

`u8`은 0에서 255까지의 값을 갖는다.

1, 3, 5, 7 값만 사용하고 나머지는 신경 쓰고 싶지 않다면

`_` 패턴으로 0, 2, 4, 6, 8, 9, ..., 255까지의 값을 대신할 수 있다.

```rust
let some_u8_value = 0u8;
match some_u8_value {
    1 => println!("one"),
    3 => println!("three"),
    5 => println!("five"),
    7 => println!("seven"),
    _ => (),
}
```

# `if let`을 사용한 간결한 흐름제어

하나의 패턴만 매칭하고 나머지는 무시할 수 있다.

코드가 짧아지는 건 덤이다.

## `match`를 사용한 경우

`Option<u8>`에서 값이 3인 경우에만 코드를 실행하고 싶다면 아래와 같이 코드를 작성한다.

```rust
let some_u8_value = Some(0u8);
match some_u8_value {
    Some(3) => println!("three"),
    _ => (),
}
```

한 가지 경우만 사용하지만 `match` 표현식을 만족하기 위해 너무 많은 보일러 플레이트를 작성하고 있다.

## `if let` 사용하기

`if let`을 사용하면 타이핑을 줄일 수 있다.

```rust
if let Some(3) = some_u8_value {
    println!("three");
}
```

다만, `match`가 강제했던 빠짐없는 검사를 잃게 된다.
