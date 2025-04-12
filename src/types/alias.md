# 별명 만들기

`type` 선언문은 기존 타입에 새로운 이름을 제공합니다. 타입 이름은 반드시
`UpperCamelCase`(대문자 시작 카멜-케이스)로 지어야 하며, 아닌 경우 컴파일러에서
경고를 낼 겁니다. `usize`나 `f32` 등의 사전 정의된 타입은 예외입니다.

```rust,editable
// `NanoSecond`, `Inch`, and `U64` are new names for `u64`.
type NanoSecond = u64;
type Inch = u64;
type U64 = u64;

fn main() {
    // `NanoSecond` = `Inch` = `U64` = `u64`.
    let nanoseconds: NanoSecond = 5 as u64;
    let inches: Inch = 2 as U64;

    // Note that type aliases *don't* provide any extra type safety, because
    // aliases are *not* new types
    println!("{} nanoseconds + {} inches = {} unit?",
             nanoseconds,
             inches,
             nanoseconds + inches);
}
```

이런 타입 별명은 불필요한 코드를 줄이기 위해 사용됩니다. 예를 들어
- `io::Result<T>`는 `Result<T, io::Error>`의 별칭입니다.
- 역주: `Some<T>()`과 `None::<T>`은 각각 `std::option::Option<T>::Some()`과 `std::option::Option<T>::None`의 별칭입니다.
  * `Option<T>`는 다시 `std::option::Option<T>`의 별칭입니다.

### 함께 보기:

[속성](../attribute.md)
