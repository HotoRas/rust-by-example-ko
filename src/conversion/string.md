# `String`으로, `String`에서

## 문자열로 변환하기

어떤 타입을 `String`으로 변환하는 것은 [`ToString`] 트레잇을 타입에 구현하는 것
정도로 아주 간단합니다만, 이를 직접 하는 것보다는 [`ToString`]과 [`print!`]에서
다룬 타입 프린팅을 자동으로 제공하는 [`fmt::Display`][Display] 트레잇을 구현해야
합니다.

```rust,editable
use std::fmt;

struct Circle {
    radius: i32
}

impl fmt::Display for Circle {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        write!(f, "Circle of radius {}", self.radius)
    }
}

fn main() {
    let circle = Circle { radius: 6 };
    println!("{}", circle.to_string());
}
```

## 문자열 파싱하기

문자열을 여러 타입으로 변환하는 것은 매우 유용하지만, 대부분의 일반적인 문자열 작업은
이를 수로 변환하는 것입니다. 이상적인 접근은 [`parse`] 함수를 사용하고 타입 추정으로
정형화하거나, 고속 파싱을 이용하는 것입니다. 두 방식 모두 아래에 잘 설명되어
있습니다.

```rust,editable
fn main() {
    let parsed: i32 = "5".parse().unwrap();
    let turbo_parsed = "10".parse::<i32>().unwrap();

    let sum = parsed + turbo_parsed;
    println!("Sum: {:?}", sum);
}
```

이런 작업을 사용자 지정 타입에 가져오려면 [`FromStr`] 트레잇을 그 타입에 구현하면
됩니다.

```rust,editable
use std::num::ParseIntError;
use std::str::FromStr;

#[derive(Debug)]
struct Circle {
    radius: i32,
}

impl FromStr for Circle {
    type Err = ParseIntError;
    fn from_str(s: &str) -> Result<Self, Self::Err> {
        match s.trim().parse() {
            Ok(num) => Ok(Circle{ radius: num }),
            Err(e) => Err(e),
        }
    }
}

fn main() {
    let radius = "    3 ";
    let circle: Circle = radius.parse().unwrap();
    println!("{:?}", circle);
}
```

[`ToString`]: https://doc.rust-lang.org/std/string/trait.ToString.html
[Display]: https://doc.rust-lang.org/std/fmt/trait.Display.html
[print]: ../hello/print.md
[`parse`]: https://doc.rust-lang.org/std/primitive.str.html#method.parse
[`FromStr`]: https://doc.rust-lang.org/std/str/trait.FromStr.html
