# C 방식 열거형

`enum`은 C 방식 열거형도 사용 가능합니다.

```rust,editable
// An attribute to hide warnings for unused code.
#![allow(dead_code)]

// 타입과 값을 지정하지 않은 열거형 (0i32에서 시작)
enum Number {
    Zero,
    One,
    Two,
}

// 값이 지정된 열거형
enum Color {
    Red = 0xff0000,
    Green = 0x00ff00,
    Blue = 0x0000ff,
}

fn main() {
    // C 방식 열거형은 정수형으로 타입 캐스팅할 수 있습니다.
    println!("zero is {}", Number::Zero as i32);
    println!("one is {}", Number::One as i32);

    println!("roses are #{:06x}", Color::Red as i32);
    println!("violets are #{:06x}", Color::Blue as i32);
}
```

### See also:

[casting][cast]

[cast]: ../../types/cast.md
