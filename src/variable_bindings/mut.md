# 수정 가능성

변수 할당은 기본적으로 수정 불가능하지만, `mut` 수정자를 통해 덮어씌울 수 있습니다.

```rust,editable,ignore,mdbook-runnable
fn main() {
    let _immutable_binding = 1;
    let mut mutable_binding = 1;

    println!("Before mutation: {}", mutable_binding);

    // Ok
    mutable_binding += 1;

    println!("After mutation: {}", mutable_binding);

    // Error!
    _immutable_binding += 1;
    // FIXME ^ Comment out this line
}
```

컴파일러는 수정 가능성 오류에 대해 자세한 분석을 리턴합니다.
