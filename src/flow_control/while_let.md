# while let

`if let`과 비슷하게, `while let`을 이용해 짜증나는 `match` 시퀸스를 좀 더 통제 가능하게
바꿀 수 있습니다. `i`를 증가시키기 위한 다음 코드를 생각해 봅시다:

```rust
// Make `optional` of type `Option<i32>`
let mut optional = Some(0);

// Repeatedly try this test.
loop {
    match optional {
        // If `optional` destructures, evaluate the block.
        Some(i) => {
            if i > 9 {
                println!("Greater than 9, quit!");
                optional = None;
            } else {
                println!("`i` is `{:?}`. Try again.", i);
                optional = Some(i + 1);
            }
            // ^ Requires 3 indentations!
        },
        // 해체가 불가하면 반복문 밖으로 나갑니다:
        _ => { break; }
        // ^ 이 줄을 굳이 써야 할까요? 더 나은 방법이 분명 있을 겁니다!
    }
}
```

`while let`을 이용하면 이 과정이 좀 더 봐줄 만해집니다.

```rust,editable
fn main() {
    // Make `optional` of type `Option<i32>`
    let mut optional = Some(0);

    // 이 블록은 `let`이 `optional`을 `Some(i)`로 해체할 수 있으면 내부 블록을
    // 실행하고, 아니라면 `break`합니다
    while let Some(i) = optional {
        if i > 9 {
            println!("Greater than 9, quit!");
            optional = None;
        } else {
            println!("`i` is `{:?}`. Try again.", i);
            optional = Some(i + 1);
        }
        // ^ Less rightward drift and doesn't require
        // explicitly handling the failing case.
    }
    // ^ `if let`은 `else`나 `else if`를 붙일 수 있었죠.
    // 반면 `while let`은 그렇지 않습니다.
}
```

### 함께 읽기:

[`enum`][enum], [`Option`][option]와 [RFC][while_let_rfc]

[enum]: ../custom_types/enum.md
[option]: ../std/option.md
[while_let_rfc]: https://github.com/rust-lang/rfcs/pull/214
