# 스코프와 섀도잉

변수 할당은 스코프를 가지며, *블록* 안에서 존재하는 것으로 간주됩니다. 블록은
중괄호 `{}`로 묶인 선언문 덩어리입니다.

```rust,editable,ignore,mdbook-runnable
fn main() {
    // 이 할당문은 main 함수에 있습니다.
    let long_lived_binding = 1;

    // 이것이 블록이며, main 함수보다 작은 스코프입니다.
    {
        // 이 바인딩은 이 스코프에만 있습니다.
        let short_lived_binding = 2;

        println!("inner short: {}", short_lived_binding);
    }
    // 블록 끝

    // 오류! `short_lived_binding`이 더이상 존재하지 않습니다.
    println!("outer short: {}", short_lived_binding);
    // FIXME ^ Comment out this line

    println!("outer long: {}", long_lived_binding);
}
```

또, [변수 섀도잉][variable-shadow]도 가능합니다.

```rust,editable,ignore,mdbook-runnable
fn main() {
    let shadowed_binding = 1;

    {
        println!("before being shadowed: {}", shadowed_binding);

        // This binding *shadows* the outer one
        let shadowed_binding = "abc";

        println!("shadowed in inner block: {}", shadowed_binding);
    }
    println!("outside inner block: {}", shadowed_binding);

    // This binding *shadows* the previous binding
    let shadowed_binding = 2;
    println!("shadowed in outer block: {}", shadowed_binding);
}
```

[variable-shadow]: https://en.wikipedia.org/wiki/Variable_shadowing
