# `From`과 `Into`

[`From`]과 [`Into`]는 내부적으로 연결되어 있고, 실제로 구현의 일부입니다.
타입 A에서 B로 변환이 가능하다면, B에서 A로 또한 손쉽게 가능하다고 확신할 수 있죠.

## `From`

`From` 트레잇은 다른 타입에서 자신을 만드는 방법을 정의하게 합니다. 이로서 서로 다른
많은 타입과 전환하는 아주 간단한 방식을 제공할 수 있죠.
표준 라이브러리만에서도 이미 사전 정의 타입과 표준 타입 간의 변환을 수행하는
수많은 구현체가 있습니다.

예를 들어 `&str`에서 `String`으로 아주 간단하게 변환할 수 있죠.

```rust
let my_str = "hello";
let my_string = String::from(my_str);
```

비슷한 동작을 우리가 만든 타입에서도 변환을 선언해 진행할 수 있습니다.

```rust,editable
use std::convert::From;

#[derive(Debug)]
struct Number {
    value: i32,
}

impl From<i32> for Number {
    fn from(item: i32) -> Self {
        Number { value: item }
    }
}

fn main() {
    let num = Number::from(30);
    println!("My number is {:?}", num);
}
```

## `Into`

`Into` 트레잇은 `From` 트레잇의 반대 동작입니다. 타입을 다른 타입으로 전환하는
방법을 선언하죠.

`into()`를 호출하는 경우 도착 타입을 지정해야 합니다. 대부분의 경우 컴파일러가
타입 추정을 확실하게 하기 어렵거든요.

```rust, editable
use std::convert::Into;

#[derive(Debug)]
struct Number {
    value: i32,
}

impl Into<Number> for i32 {
    fn into(self) -> Number {
        Number { value: self }
    }
}

fn main() {
    let int = 5;
    // 타입 어노테이션을 지워보세요
    let num: Number = int.into();
    println!("My number is {:?}", num);
}
```

## `From`과 `Into`는 상호 전환이 가능합니다

`From`과 `Into`는 상호 전환이 가능하도록 설계되어 있어, 두 트레잇 모두에 대해 선언할
필요가 없습니다. `From` 트레잇을 타입에 선언했다면 `Into`는 필요할 때 선언됩니다.
하지만 반대 방향은 그렇지 않습니다: `Into`를 선언한 타입은 `From` 트레잇을 자동으로
선언하지 않습니다.

```rust,editable
use std::convert::From;

#[derive(Debug)]
struct Number {
    value: i32,
}

// `From`을 선언합니다
impl From<i32> for Number {
    fn from(item: i32) -> Self {
        Number { value: item }
    }
}

fn main() {
    let int = 5;
    // `Into`를 사용합니다
    let num: Number = int.into();
    println!("My number is {:?}", num);
}
```

[`From`]: https://doc.rust-lang.org/std/convert/trait.From.html
[`Into`]: https://doc.rust-lang.org/std/convert/trait.Into.html
