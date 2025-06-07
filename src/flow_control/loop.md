# loop

러스트는 무한 반복을 위해 `loop` 키워드를 제공합니다.

`break` 선언문을 이용해 무한 반복을 언제든 빠져나올 수 있으며,
`continue` 선언문을 이용해 남은 순서를 건너뛰고 다음 반복으로 넘어갈 수 있습니다.

```rust,editable
fn main() {
    let mut count = 0u32;

    println!("Let's count until infinity!");

    // Infinite loop
    loop {
        count += 1;

        if count == 3 {
            println!("three");

            // Skip the rest of this iteration
            continue;
        }

        println!("{}", count);

        if count == 5 {
            println!("OK, that's enough");

            // Exit this loop
            break;
        }
    }
}
```