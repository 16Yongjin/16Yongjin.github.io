---
title: \[Rust\] 컬렉션(벡터, 스트링, 해쉬맵)
date: 2020-02-10T20:00:00+09:00
author: yongjin0802
categories:
  - Rust
---

러스트의 대표적 컬렉션인 벡터, 스트링, 해쉬맵

# 러스트의 벡터

같은 타입의 값을 메모리 상에 이웃하도록 저장한다.

## 새 백터 만들기

비어있는 벡터를 생성한다.

값이 아무것도 들어있지 않아 타입을 명시해야 한다.

```rust
let v: Vec<i32> = Vec::new();
```

## `vec!` 매크로로 벡터 만들기

초기값을 제공해서 타입을 명시할 필요 없다.

```rust
let v = vec![1, 2, 3];
```

## 벡터 갱신하기

`mut` 키워드로 변수를 가변으로 만들어야 값을 추가할 수 있다.

추가되는 데이터에서 타입을 추론하기 때문에 `Vec<i32>` 명시할 필요 없다.

```rust
let mut v = Vec::new();

v.push(5);
v.push(6);
v.push(7);
v.push(8);
```

## 벡터의 요소 읽기

인덱스로 `T` 값을 얻거나 `get(인덱스)` 메서드로 `Option<T>` 값을 얻을 수 있다.

```rust
let v = vec![1, 2, 3, 4, 5];

let third: &i32 = &v[2];
let third: Option<&i32> = v.get(2);
```

벡터의 크기를 벗어나는 인덱스에 직접 접근하면 `panic!`을 일으킨다.

같은 인덱스를 `get()` 메서드로 접근하면 `None`이 반환된다.

```rust
let v = vec![1, 2, 3, 4, 5];

let does_not_exist = &v[100]; // panic!
let does_not_exist = v.get(100); // None
```

## 벡터에도 참조자 규칙이 그대로 적용됨

아래 코드는 불변 참조자를 만든 뒤 가변 참조자를 만들려고 해서 에러가 난다.

```rust
let mut v = vec![1, 2, 3, 4, 5];

let first = &v[0];

v.push(6);
```

벡터에 새 요소 추가 시, 저장 공간 부족으로 새로운 메모리 공간에 벡터 요소들을 옮기는 일이 발생할 수 있다.

이 경우 `first`는 할당 해제된 메모리를 가리키게 되는데, 빌림 규칙으로 이런 상황을 막을 수 있다.

## 벡터 요소 반복처리

불변 참조자를 얻어서 반복하기

```rust
let v = vec![100, 32, 57];
for i in &v {
    println!("{}", i);
}
```

가변 참조자를 얻어서 각 요소 변경하기

값을 변경하기 전에 역참조 연산자(`*`)를 사용해서 참조에서 값을 얻어야 한다.

```rust
let mut v = vec![100, 32, 57];
for i in &mut v {
    *i += 50;
}
```

## 열거형으로 여러 타입 저장하기

열거형 내에 다양한 값이 있어도 모두 같은 타입으로 다뤄진다.

벡터 내에 다양한 타입의 값을 넣고 싶으면 열거형을 사용하면 된다.

```rust
enum SpreadsheetCell {
    Int(i32),
    Float(f64),
    Text(String),
}

let row = vec![
    SpreadsheetCell::Int(3),
    SpreadsheetCell::Text(String::from("blue")),
    SpreadsheetCell::Float(10.12),
];
```

각 요소를 저장하기 위해 필요한 힙 메모리 크기를 알기 위해 컴파일 타임에 벡터에 저장할 타입을 알아야 한다.

저장할 타입이 런타임에 정해져서 모른다면 트레잇 객체를 사용한다.

&nbsp;

# 러스트의 스트링

러스트 코어는 스트링 슬라이스인 `str`만 제공한다.

`String` 타입은 표준 라이브러리를 통해 제공된다.

## `String` 타입의 특성

1. 가변적
2. 소유권
3. UTF-8 인코딩(어떤 문자라도 포함할 수 있다.)

## 새로운 스트링 만들기

`new` 함수로 비어있는 스트링을 생성할 수 있다.

```rust
let mut s = String::new();
```

`to_string` 메서드로 초기값이 있는 스트링을 만든다.

`Display` 트레잇이 구현된 타입은 모두 `to_string` 메서드 사용이 가능하다.

```rust
let s = "initial contents".to_string();
```

`String::from` 함수로도 스트링 리터럴에서 `String`을 생성할 수 있다.

```rust
let s = String::from("initial contents");
```

`String::from`과 `.to_string`은 기능이 똑같아서 어떤 것을 사용할 지는 개발자 마음이다.

## 스트링 갱신하기

`push_str` 메서드로 `String`을 늘릴 수 있다.

```rust
let mut s = String::from("foo");
s.push_str("bar");
```

`push_str` 메서드는 파라미터의 소유권을 가져올 필요가 없어서 스트링 슬라이스를 파라미터로 갖는다.

아래 코드에서 `s2`는 소유권이 보존돼서 오류가 나지 않는다.

```rust
let mut s1 = String::from("foo");
let s2 = "bar";
s1.push_str(&s2);
println!("s2 is {}", s2);
```

`push`로 문자 하나를 `String`에 추가할 수 있다.

```rust
let mut s = String::from("lo");
s.push('l');
```

## `+`로 스트링 붙이기

`+` 연산자로 두 개의 스트링을 조합할 수 있다.

```rust
let s1 = String::from("Hello, ");
let s2 = String::from("world!");
let s3 = s1 + &s2; // s1은 이동되어 유효하지 않아짐
```

`+` 연산은 아래 처럼 생긴 `add` 메서드를 사용하는데 `String`에 `&str`을 더하는 형태이다.

```rust
fn add(self, s: &str) -> String {
```

`&s2`는 `&String`이지만 **역참조 강제**에 의해 `&str`로 강제 변환된다.

`&s2`가 `&s2[..]`로 바뀌는 것이다.

`add`가 `s2`의 소유권은 가져가지 않지만

`&`가 없는 `self`로 `s1`을 인자로 받아서 `s1`의 소유권을 가져간다.

## `format!` 매크로로 스트링 합치기

`format!` 매크로는 `println!`처럼 작동하면서 결과를 스크린에 출력하는 대신 `String`을 반환한다.

또한, `format!`은 파라미터의 소유권을 가져가지 않는다.

```rust
let s1 = String::from("tic");
let s2 = String::from("tac");
let s3 = String::from("toe");

let s = format!("{}-{}-{}", s1, s2, s3);
```

## 스트링을 인덱싱로 접근하기

는 지원되지 않는다.

## 스트링의 내부적 표현

`String`은 `Vec<u8>`을 감싼 것이다.

아래의 `len`은 4인 반면

```rust
let len = String::from("Hola").len();
```

아래의 `len`은 12가 아닌 24이다.

```rust
let len = String::from("Здравствуйте").len();
```

각각의 유니코드 스칼라 값이 2바이트 씩 차지하기 때문이다.

## 바이트, 스칼라 값, 문자소 클러스터(우리가 보는 글자)

“नमस्ते” 이렇게 생긴 힌디어는 18바이트의 `Vec<u8>`로 저장된다.

```
[224, 164, 168, 224, 164, 174, 224, 164, 184, 224, 165, 141, 224, 164, 164, 224, 165, 135]
```

`char` 타입으로 본다면 이렇다.

```
['न', 'म', 'स', '्', 'त', 'े']
```

우리가 보는 글자처럼 문자로 클러스터로 보면 이렇다.

```
["न", "म", "स्", "ते"]
```

셋 중에 어떤게 유효한지는 문자열 내용을 모두 알아야 알 수 있다.

그래서 `String`의 인덱스 연산이 O(1) 성능이 보장되지 않는다.

## 스트링 슬라이스할 때는 조심

스트링 슬라이스를 만들 때는 스트링 인덱스로 접근하는 것과 같은 연산을 하면 안 된다.

아래는 괜찮은데

```rust
let hello = "Здравствуйте";

let s = &hello[0..4];
```

아래와 같이 하면 인덱스로 접근하는 것과 같아서 런타임에 패닉이 발생한다.

```rust
&hello[0..1]
```

## 스트링 요소 접근

### 1. 캐릭터로 반복하기(`.chars()`)

```rust
for c in "नमस्ते".chars() {
    println!("{}", c);
}
```

### 2. 바이트로 반복하기(`.bytes()`)

```rust
for b in "नमस्ते".bytes() {
    println!("{}", b);
}
```

### 3. 문자소 클러스터로 반복하기

방법이 복잡해서 라이브러리를 가져다 쓴다.

## 스트링이 복잡한 만큼 사용하기 까다롭다.

러스트가 다루기 까다로운데 본성이 복잡한 스트링은 러스트 내에서 다루기 더 까다롭다.

하지만, 까다로움 덕분에 개발 후반에 스트링 관련 에러를 마주할 일을 막을 수 있다.

&nbsp;

# 러스트의 해쉬맵

키 타입 `K`에 값 타입 `V`를 매핑한 해쉬맵 타입 `HashMap<K, V>`

JS의 오브젝트, 맵, 파이썬의 딕셔너리와 같다.

벡터처럼 인덱스 사용하기 보단 임의 타입의 키로 데이터를 찾을 때 유용하다.

## `new`로 해쉬맵 생성하기

해쉬맵의 `new` 함수로 생성하고 `insert`로 요소를 추가한다.

해쉬맵이 다른 컬렉션보다 잘 사용되는 편이 아니라 prelue에 불러져 있지 않아서, 표준 라이브러리에서 가져와야 한다. (해쉬맵 생성 매크로도 없다.)

```rust
use std::collections::HashMap;

let mut scores = HashMap::new();

scores.insert(String::from("Blue"), 10);
scores.insert(String::from("Yellow"), 50);
```

## 벡터의 `collect()` 메서드로 해쉬맵 생성하기

키, 값으로 된 튜플 벡터에 `collect()` 함수를 호출해서 해쉬맵을 생성한다.

```rust
use std::collections::HashMap;

let teams  = vec![String::from("Blue"), String::from("Yellow")];
let initial_scores = vec![10, 50];

let scores: HashMap<_, _> = teams.iter().zip(initial_scores.iter()).collect();
```

`HashMap<_, _>`로 타입 명시를 해서 벡터에 담긴 타입으로 해쉬에 담길 타입을 추론하게 한다.

## 해쉬맵과 소유권

`Copy` 트레잇을 구현 타입(ex, `i32`)은 값들이 해쉬맵으로 복사된다.

`String` 등은 해쉬맵으로 소유권이 옮겨진다.

```rust
use std::collections::HashMap;

let field_name = String::from("Favorite color");
let field_value = String::from("Blue");

let mut map = HashMap::new();
map.insert(field_name, field_value);
// field_name과 field_value은 이 지점부터 유효하지 않다.
```

해쉬맵에 참조자를 넣으면 소유권은 이동하지 않지만 참조하는 값들이 해쉬맵이 유효할 때까지 유효해야 한다.

## `get` 메서드로 해쉬맵 내의 값 접근하기

`get` 메서드에 키를 제공해서 값을 얻어온다.

얻어온 값은 `Option<&V>` 타입을 가지고 있다.

```rust
use std::collections::HashMap;

let mut scores = HashMap::new();

scores.insert(String::from("Blue"), 10);
scores.insert(String::from("Yellow"), 50);

let team_name = String::from("Blue");
let score = scores.get(&team_name);
```

## `for` 루프로 키/값 쌍에 반복작업하기

```rust
use std::collections::HashMap;

let mut scores = HashMap::new();

scores.insert(String::from("Blue"), 10);
scores.insert(String::from("Yellow"), 50);

for (key, value) in &scores {
    println!("{}: {}", key, value);
}
```

## 해쉬맵 값 덮어쓰기

이미 있는 키에 다른 값을 삽입하면 값이 새 값으로 대신된다.

```rust
use std::collections::HashMap;

let mut scores = HashMap::new();

scores.insert(String::from("Blue"), 10); // 블루가 10이었다가
scores.insert(String::from("Blue"), 25); // 25가 됨

println!("{:?}", scores); // {"Blue": 25} 출력
```

## `entry` 메서드로 키에 할당된 값이 없을 경우에만 삽입하기

`entry` 메서드는 열거형 `Entry`를 반환하면서 해당 키 존재 여부를 나타낸다.

`Entry`의 `or_insert or_insert` 메서드는 키가 존재하면 해당 값을 반환하고

아니면 새 값을 삽입 후 수정된 `Entry` 값을 반환한다.

```rust
use std::collections::HashMap;

let mut scores = HashMap::new();
scores.insert(String::from("Blue"), 10); // "Blue" 키는 이미 존재

scores.entry(String::from("Yellow")).or_insert(50); // 없어서 잘 들감
scores.entry(String::from("Blue")).or_insert(50); // 이미 있어서 안 들감

println!("{:?}", scores); // {"Yellow": 50, "Blue": 10}
```

## 예전 값을 기초로 값을 갱신하기

아래 코드는 `text` 내의 각 단어의 빈도수를 센다.

처음 본 단어면 0을, 아니면 해당 빈도수에 1을 더한 값을 삽입한다.

```rust
use std::collections::HashMap;

let text = "hello world wonderful world";

let mut map = HashMap::new();

for word in text.split_whitespace() {
    let count = map.entry(word).or_insert(0);
    *count += 1;
}

println!("{:?}", map); // {"world": 2, "hello": 1, "wonderful": 1}
```

## 해쉬 함수

`HashMap`의 기본 해쉬 함수는 보안을 위해 성능을 절충했다.

원한다면, 해쉬 함수를 `BuildHasher` 트레잇을 구현한 다른 함수로 변경할 수 있다.
