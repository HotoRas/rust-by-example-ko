# 상수

러스트에는 글로벌을 포함해 어느 스코프에서나 선언될 수 있는 두 가지의 상수가
있습니다. 특정한 타입 어노테이션이 요구됩니다:

* `const`: 변경되지 않는 값 (일반적인 경우)
* `static`: [`'static`][static] 라이프타임을 가지는 값이 바뀔 수 있는 변수입니다.
  static 라이프타입은 추정되므로 선언할 필요가 없습니다. static mutable 변수에
  접근하거나 수정하는 행위는 [`unsafe`][unsafe]로 정의됩니다. 

```rust,editable,ignore,mdbook-runnable
// 글로벌 상수는 모든 스코프 밖에 선언됩니다
static LANGUAGE: &str = "Rust";
const THRESHOLD: i32 = 10;

fn is_big(n: i32) -> bool {
    // 함수 안에서 상수 접근
    n > THRESHOLD
}

fn main() {
    let n = 16;

    // 메인 스레드에서 상수 접근
    println!("This is {}", LANGUAGE);
    println!("The threshold is {}", THRESHOLD);
    println!("{} is {}", n, if is_big(n) { "big" } else { "small" });

    // 오류! `const`는 수정할 수 없습니다.
    THRESHOLD = 5;
    // FIXME ^ Comment out this line
}
```

### 함께 읽기:

[The `const`/`static` RFC](
https://github.com/rust-lang/rfcs/blob/master/text/0246-const-vs-static.md),
[`'static` lifetime][static]

[static]: ../scope/lifetime/static_lifetime.md
[unsafe]: ../unsafe.md
