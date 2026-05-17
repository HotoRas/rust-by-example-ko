# 타입 리터럴

숫자 리터럴은 접미어를 통해 타입 선언될 수 있습니다. 예를 들어 `42`가 `i32`
타입이어야 하는 경우, `42i32`로 선언하면 됩니다.

접미어 없이 선언된 숫자 리터럴은 사용에 따라 타입이 지정됩니다. 맥락을 확인할 수
없는 경우, 컴파일러는 정수는 `i32`, 부동소수점은 `f64`로 지정합니다.

```rust,editable
fn main() {
    // Suffixed literals, their types are known at initialization
    let x = 1u8;
    let y = 2u32;
    let z = 3f32;

    // Unsuffixed literals, their types depend on how they are used
    let i = 1;
    let f = 1.0;

    // `size_of_val` returns the size of a variable in bytes
    println!("size of `x` in bytes: {}", std::mem::size_of_val(&x));
    println!("size of `y` in bytes: {}", std::mem::size_of_val(&y));
    println!("size of `z` in bytes: {}", std::mem::size_of_val(&z));
    println!("size of `i` in bytes: {}", std::mem::size_of_val(&i));
    println!("size of `f` in bytes: {}", std::mem::size_of_val(&f));
}
```

위 코드에는 아직 설명하지 않은 컨셉이 사용되어, 급한 분들을 위해 짧은 설명을
덧붙입니다:

* `std::mem::size_of_val`은 함수이지만 *전체 경로*를 통해 호출되었습니다. 코드는
  *모듈*이라는 논리적 단위로 나뉩니다. 여기서는 `size_of_val` 함수는 `mem` 모듈에,
  `mem` 모듈은 `std` *크레이트*에 선언되어 있습니다. 더 자세한 것은
  [모듈][mod]과 [크레이트][crate]를 참고하세요.

[mod]: ../mod.md
[crate]: ../crates.md
