# `dead_code`

러스트 컴파일러는 `dead_code` [*lint*][lint]를 통해 사용되지 않은
함수에 대해 경고를 표시합니다. *속성*을 이용해 이를 비활성화할 수 있습니다.

```rust,editable
fn used_function() {}

// `#[allow(dead_code)]` is an attribute that disables the `dead_code` lint
#[allow(dead_code)]
fn unused_function() {}

fn noisy_unused_function() {}
// FIXME ^ Add an attribute to suppress the warning

fn main() {
    used_function();
}
```

실제 프로그램에서는 이러한 "죽은 코드"를 없애야 합니다. 이 예시들에서는
예시들의 대화형 특성에 의해 여러 "죽은 코드"를 허용하고 있습니다.

[lint]: https://en.wikipedia.org/wiki/Lint_%28software%29
