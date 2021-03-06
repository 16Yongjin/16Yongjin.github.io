---
title: \[Rust\] 라이프타임
date: 2020-02-15T20:10:00+09:00
author: yongjin0802
categories:
  - Rust
---

모든 참조자는 라이프타임을 갖고 있다.

대부분의 경우 참조자의 라이프타임이 암묵적을 추론된다.

러스트가 추론에 실패한 경우, 제네릭 라이프타임 파라미터를 명시해서 런타임에 참조자의 유효성을 확실히 한다.

## 댕글링 참조자를 방지하는 라이프타임

라이프타임은 의도하지 않은 데이터를 참조하는 일을 예방한다.

아래 프로그램은 외부와 내부 스코프를 가지고 있다.

내부 스코프에서 `x`의 참조자를 외부에서 선언된 `r`에 대입한다.

내부 스코프 종료 후 `r`의 값을 출력한다.

```rust
{
    let r;

    {
        let x = 5;
        r = &x;
    }

    println!("r: {}", r);
}
```

컴파일 시 `` `x` does not live long enough ``이라는 에러가 발생한다.

`x`가 스코프 밖으로 벗어났을 때, `r`이 할당 해제된 메모리를 참조해서 생긴 에러다.

러스트는 **빌림 검사기**를 이용해서 위와 같이 잘못된 코드의 컴파일을 막는다.

## 빌림 검사기(Borrow checker)

주석으로 변수의 라이프타임을 표시했다.

```rust
{
    let r;         // -------+-- 'a
                   //        |
    {              //        |
        let x = 5; // -+-----+-- 'b
        r = &x;    //  |     |
    }              // -+     |
                   //        |
    println!("r: {}", r); // |
                   //        |
                   // -------+
}
```

`r`의 라이프타임은 `'a`로, `x`의 라이프타임은 `'b`로 표현됐다.

`'a` 라이프타임을 가진 `r`이 `'b` 라이프타임을 가진 오브젝트를 참조하고 있다.

`'b` 라이프타임이 `'a` 라이프타임보다 작아서 컴파일러가 이 프로그램을 거부한다.

참조자가 오래 살지 못하기 때문이다.

&nbsp;

아래 프로그램은 댕글링 참조자가 없어서 정상적으로 컴파일된다.

```rust
{
    let x = 5;            // -----+-- 'b
                          //      |
    let r = &x;           // --+--+-- 'a
                          //   |  |
    println!("r: {}", r); //   |  |
                          // --+  |
}                         // -----+
```

`x`의 라이프타임인 `'b`가 `'a`보다 커서 `r`이 `x`를 참조할 수 있다.

## 함수 내의 제네릭 라이프타임

두 스트링 슬라이스 중 긴 쪽을 출력하는 `longest` 함수를 구현해서 `The longest string is abcd`를 출력해야 한다.

```rust
fn main() {
    let string1 = String::from("abcd");
    let string2 = "xyz";

    let result = longest(string1.as_str(), string2);
    println!("The longest string is {}", result);
}
```

아래와 같이 `longest` 함수를 구현하면 컴파일에 실패한다.

```rust
fn longest(x: &str, y: &str) -> &str {
    if x.len() > y.len() {
        x
    } else {
        y
    }
}
```

`missing lifetime specifier`라는 에러 메시지가 나온다.

반환 타입에 제네릭 라이프타임 파라미터가 필요하다는 뜻이다.

러스트가 반환되는 참조자가 `x`를 참조하는지, `y`를 참조하는지 알 수 없기 때문이다.

## 라이프타임 명시 문법

제네릭 타입이 아무 타입이나 받듯이

제니릭 라이프타임 파라미터도 아무 라이프타임을 받을 수 있다.

여러 개의 참조자가 난립하는 상황에서 라이프타임들을 서로 연관 짓기 위해 라이프타임을 명시한다.

> 라이프타임들을 연관 짓는다 == 입력되는 참조자의 라이프타임과 반환되는 참조자의 라이프타임을 연결한다.

&nbsp;

라이프타임 파라미터 이름은 `'`로 시작한다.

참조자 `&` 뒤에 온다.

`&i32` = 참조자
`&'a i32` = 라이프타임을 가진 참조자
`&'a mut i32` = 라이프타임을 가진 가변 참조자

두 참조자가 같은 라이프타임 파라미터를 갖는다면, 둘 다 같은 제네릭 라이프타임만큼 살아야 한다는 뜻이다.

## 함수 시그니처에 라이프타임 명시하기

제네릭 타입 파라미터처럼 , 제네릭 라이프타임 파리미터도 함수이름 뒤에 정의된다.

참조자 `x`와 `y`가 동일한 라이프타임을 갖고 있다는 것을 나타내기 위해, 각 참조자에 라이프타임 `'a`를 추가한다.

```rust
fn longest<'a>(x: &'a str, y: &'a str) -> &'a str {
    if x.len() > y.len() {
        x
    } else {
        y
    }
}
```

라이프타임이 다른 참조자가 파라미터로 넘겨지면, 빌림 검사기가 거부한다.

잘 보면, 함수 시그니처에만 라이프타임이 명시되어 있고, 함수 본체에는 라이프타임 관련 코드가 없다.

러스트가 함수 안에 있는 참조자는 잘 분석하지만, 함수 밖에 있는 참조자는 다 분석할 수가 없어서 그렇다.

&nbsp;

참조자들이 `longest` 함수로 넘겨질 때, `'a`에는 `x`와 `y`의 겹치는 스코프가 대입된다.

즉, `x`와 `y`의 라이프타임 중 더 작은 쪽의 라이프타임이 `'a`로 들어간다.

반환되는 참조자에도 `'a`가 명시됐으니, `'a` 만큼의 라이프타임을 갖고 있음을 보장한다.

아래 코드에서 `string1`은 외부 스코프, `string2`는 내부 스코프, `result`는 내부 스코프까지 유효한 것을 참조한다.

빌림 검사기는 이 코드를 승인해서 컴파일에 성공한다.

```rust
fn main() {
    let string1 = String::from("long string is long");

    {
        let string2 = String::from("xyz");
        let result = longest(string1.as_str(), string2.as_str());
        println!("The longest string is {}", result);
    }
}
```

아래 코드에서 `result`는 내부 스코프에서 선언됐지만, 외부 스코프에서 사용된다.

`string2`가 스코프를 벗어난 후에 `result`를 사용하고자 해서 컴파일에 실패한다.

```rust
fn main() {
    let string1 = String::from("long string is long");
    let result;
    {
        let string2 = String::from("xyz");
        result = longest(string1.as_str(), string2.as_str());
    }
    println!("The longest string is {}", result);
}
```

입력 참조자의 라이프타임(`string1`과 `string2` 중 짧은 쪽인 `string2`의 라이프타임)과 반환 참조자의 라이프타임(`result`의 라이프타임)의 길이가 달라서 그렇다.

## 라이프타임의 측면에서 생각하기

아래 코드는 `y`에 라이프타임을 명시하지 않았는데도 컴파일된다.

`y`의 라이프타임이 `x`나 반환값의 라이프타임과 아무 관련이 없기 때문이다.

```rust
fn longest<'a>(x: &'a str, y: &str) -> &'a str {
    x
}
```

&nbsp;

반환되는 참조가 입력 인자를 하나도 참조하지 않는다면, 함수 내에서 생성된 값을 참조한다는 뜻이다. (무조건이다.)

이 값은 함수가 끝나면 스코프 밖으로 벗어나서 댕글링 참조자가 된다.

아래와 같은 함수는 `` `result` does not live long enough ``에러를 내며 컴파일에 실패한다.

```rust
fn longest<'a>(x: &'a str, y: &str) -> &'a str {
    let result = String::from("really long string");
    result.as_str()
}
```

라이프타임 문법은 함수의 인자와 반환 값 사이를 연결하는 것에 대한 것이다.

라이프타임 명시를 통해 메모리 안전을 저해하는 연산을 막을 충분한 정보를 갖게 된다.

## 구조체 정의 상에서의 라이프타임 명시

구조체가 참조자를 가지기 위해서는 참조자에 라이프타임을 표시해야 한다.

구조체 이름 뒤에 제네릭 라이프타임 파라미터를 적는다.

```rust
struct ImportantExcerpt<'a> {
    part: &'a str,
}

fn main() {
    let novel = String::from("Call me Ishmael. Some years ago...");
    let first_sentence = novel.split('.')
        .next()
        .expect("Could not find a '.'");
    let i = ImportantExcerpt { part: first_sentence };
}
```

`main` 함수는 변수 `novel`이 소유한 `String` 첫 문장의 참조자를 들고 있는 `ImportantExcerpt` 구조체 인스턴스를 생성한다.

## 라이프타임 생략

모든 참조자가 라이프타임을 가지고 있지만, 모든 참조자에 라이프타임을 적을 필요가 없다.

라이프타임 명시가 없는 아래 코드는 잘만 컴파일 된다.

```rust
fn first_word(s: &str) -> &str {
    let bytes = s.as_bytes();

    for (i, &item) in bytes.iter().enumerate() {
        if item == b' ' {
            return &s[0..i];
        }
    }

    &s[..]
}
```

옛날의 러스트는 위와 같은 간단한 함수에도 라이프타임을 명시하지 않으면 컴파일이 안 됐다.

나중에, 자주 쓰는 간단한 패턴에서는 빌림 검사기가 라이프타임을 추론할 수 있도록 한 것이다.

참조자 분석이 가능한 패턴을 라이프 타임 생략 규칙이라고 한다.

명시적인 라이프타임이 없으면 참조자가 어떤 라이프타임을 갖는지 알아낸다.

우선, 파라미터의 라이프타임은 _입력 라이프타입_, 반환 값의 라이프타임은 _출력 라이프타임_ 이라고 한다.

### 1. 각 참조자 파라미터는 고유한 라이프타임 파라미터를 갖는다.

파라미터가 하나면 하나의 라이프타임 파라미터를 갖는다:

```rust
fn foo<'a>(x: &'a i32)
```

파라미터가 두 개면 라이프타임도 두 개 갖는다.

```rust
fn foo<'a, 'b>(x: &'a i32, y: &'b i32)
```

### 2. 라이프타임 파라미터가 딱 한 개만 있으면, 그 라이프타임이 모든 출력 라이프타임 파리미터에 적용된다.

```rust
fn foo<'a>(x: &'a i32) -> &'a i32
```

### 3. 메서드에서 입력 라이프타임 파라미터가 여러 개 있을 때, 파라미터 중 `&self`나 `&mut self`가 있다면, `self`의 라이프타임이 모든 출력 라이프타임 파라미터에 적용된다.

직접 라이프타임 추론해본다.

아래 `first_word` 함수 시그니처에는 아무 라이프타입도 없다.

```rust
fn first_word(s: &str) -> &str {
```

1번 규칙을 적용하면, 모든 파라미터가 고유의 라이프타임을 갖는다.

함수 시그니처에 `'a`를 추가한다.

```rust
fn first_word<'a>(s: &'a str) -> &str {
```

입력 파라미터가 한 개라서 2번 규칙을 적용하면, 출력 파라미터에 입력 파라미터의 라이프타임을 적용한다.

```rust
fn first_word<'a>(s: &'a str) -> &'a str {
```

끝!

&nbsp;

아래 `longest` 함수의 라이프타임을 추론해본다.

```rust
fn longest(x: &str, y: &str) -> &str {
```

1번 규칙으로 각각의 파라미터는 고유의 라이프타임을 갖는다.

```rust
fn longest<'a, 'b>(x: &'a str, y: &'b str) -> &str {
```

입력 파라미터가 한 개 이상이라 2번 규칙은 스킬한다.

또, 함수가 아니라서 3번 규칙도 스킵한다.

라이프타임 추론에 실패해서, 컴파일에 성공하려면 라이프타임을 직접 명시해야 한다.

## 메서드 정의 시 라이프타임 명시

`impl` 뒤에 라이프타임을 붙인다.

아래 `level` 메서드에서 반환 타입이 참조자가 아니고, 1번 생략 규칙이 적용되기에 라이프타임을 명시하지 않아도 된다.

```rust
impl<'a> ImportantExcerpt<'a> {
    fn level(&self) -> i32 {
        3
    }
}
```

아래는 3번 라이프타임 생략 규칙이 적용된다.

```rust
impl<'a> ImportantExcerpt<'a> {
    fn announce_and_return_part(&self, announcement: &str) -> &str {
        println!("Attention please: {}", announcement);
        self.part
    }
}
```

위의 코드에는 입력 라이프타임이 2개 있다.

1번 생략 규칙을 적용해서 `&self`와 `announcement`에 라이프타임을 부여한다.

파라미터 중에 `&self`가 있으므로 3번 생략 규칙을 적용해서 반환 타임은 `&self`의 라이프타임을 얻어서, 모든 라이프타임을 추론할 수 있다.

## 정적 라이프타임(`'static`)

`'static` 라이프타임은 프로그램 전체 라이프타임과 동일하다.

모든 스트링 리터럴은 `'static` 라이프타임을 가지고 있어서 아래처럼 작성해도 된다.

```rust
let s: &'static str = "I have a static lifetime.";
```

## 제네릭 타입 파라미터, 트레잇 바운드, 라이프타임을 함께 써보기

라이프타임과 제네릭 타입 파라미터를 `<'a, T>`와 같이 나열하고

`where T: Display`로 트레잇 바운드를 설정한다.

```rust
use std::fmt::Display;

fn longest_with_an_announcement<'a, T>(x: &'a str, y: &'a str, ann: T) -> &'a str
    where T: Display
{
    println!("Announcement! {}", ann);
    if x.len() > y.len() {
        x
    } else {
        y
    }
}
```
