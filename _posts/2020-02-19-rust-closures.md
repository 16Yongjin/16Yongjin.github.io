---
title: \[Rust\] 클로저
date: 2020-02-19T20:10:00+09:00
author: yongjin0802
categories:
  - Rust
---

환경을 캡처할 수 있는 익명 함수

클로저는 호출되는 스코프의 변수를 캡처할 수 있다.

이는 함수로는 할 수 없는 일이다.

## 클로저 타입 추론과 어노테이션

클로저의 파라미터나 반환값의 타입 명시는 강제가 아니다.

컴파일러가 문맥 안에서 타입을 추론한다.

굳이 클로저의 타입을 표현하고 싶다면 함수처럼 타입을 명시하면 된다.

```rust
fn  add_one_v1   (x: u32) -> u32 { x + 1 }
let add_one_v2 = |x: u32| -> u32 { x + 1 };
let add_one_v3 = |x|             { x + 1 };
let add_one_v4 = |x|               x + 1  ;
```

## 제너릭 파라미터와 `Fn` 트레잇을 사용하여 클로저 저장하기

표준 라이브러리는 `Fn`, `FnMut`, `FnOnce` 트레잇을 제공하고 모든 클로저는 이 트레잇 중 하나를 구현한다.

제너릭 파라미터와 `Fn` 트레잇을 사용해서 클로저를 구조체 필드에 넣을 수 있다.

`u32`를 입력과 반환하는 클로저의 트레잇 바운드는 `Fn(u32) -> u32`이다.

```rust
struct Cacher<T>
    where T: Fn(u32) -> u32
{
    calculation: T,
    value: Option<u32>,
}
```

함수는 `Fn*` 트레잇 세 개를 모두 구현한다.

환경에서 값을 캡처할 필요가 없을 때, `Fn` 트레잇 구현이 필요한 곳에서 클로저 대신 함수를 사용해도 된다.

## 클로저로 환경 캡처하기

아래의 `equal_to_x` 클로저는 자신이 정의된 스코프에 있는 변수 `x`를 사용할 수 있다.

```rust
fn main() {
    let x = 4;

    let equal_to_x = |z| z == x;

    let y = 4;

    assert!(equal_to_x(y));
}
```

함수로 위와 동일하게 하려면 에러가 난다.

```rust
fn main() {
    let x = 4;

    fn equal_to_x(z: i32) -> bool { z == x }

    let y = 4;

    assert!(equal_to_x(y));
}
```

에러는 `can't capture dynamic environment in a fn item; use the || { ... } closure form instead`라면서 친절하게도 클로저를 사용하라고 제안한다.

&nbsp;

클로저가 환경에서 값을 캡처할 때, 캡처값을 저장할 메모리를 사용한다.

함수는 환경을 캡처하지 않아서 이런 오버헤드가 발생하지 않는다.

## 클로저가 환경에서 값을 캡처하는 세 가지 방식

소유권 받기, 불변으로 빌려오기, 가변으로 빌려오는 방식이다.

1. `FnOnce`는 캡처한 변수의 소유권을 클로저 안으로 옮긴다. 클로저가 동일한 변수에 대해 한 번만 소유권을 얻을 수 있어서 `Once`라는 이름이 들어갔다.

2. `Fn`은 캡처한 값을 불변으로 빌려온다.

3. `FnMut`은 값을 가변으로 빌려와서 환경을 변경할 수 있다.

## `move` 키워드로 캡처값의 소유권을 강제로 갖기

클로저를 다른 스레드로 넘길 때, 새로운 스레드가 이동하는 데이터를 소유하도록 할 때 유용하다.

정수는 복사돼서 아래 예제는 벡터를 사용했다.

`equal_to_x` 클로저가 `x`의 소유권을 가져가기 때문에 `println!`문에 `x`를 사용할 수 없어서 아래 코드는 컴파일 에러가 난다.

```rust
fn main() {
    let x = vec![1, 2, 3];

    let equal_to_x = move |z| z == x;

    println!("can't use x here: {:?}", x);

    let y = vec![1, 2, 3];

    assert!(equal_to_x(y));
}
```