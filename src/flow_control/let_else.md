# let-else

> 🛈 안정화 버전: rust 1.65
>
> 🛈 다음과 같이 컴파일해 해당 에디션으로 컴파일할 수 있습니다:  
> `rustc --edition=2021 main.rs`

`let`-`else`를 사용하면, 일반 `let`처럼 실패할 수 있는 패턴을 매칭하고 해당 스코프에 변수를 할당할
수 있습니다. 패턴이 맞지 않는다면 `break`, `return`, `panic!`으로 발산하는 것도 가능합니다.

```rust
use std::str::FromStr;

fn get_count_item(s: &str) -> (u64, &str) {
    let mut it = s.split(' ');
    let (Some(count_str), Some(item)) = (it.next(), it.next()) else {
        // 매칭 실패, panic!
        panic!("Can't segment count item pair: '{s}'");
    };
    let Ok(count) = u64::from_str(count_str) else {
        panic!("Can't parse integer: '{count_str}'");
    };
    (count, item)
}

fn main() {
    assert_eq!(get_count_item("3 chairs"), (3, "chairs"));
}
```

이름 바인딩의 스코프가 `match`와 `if let`-`else` 표현의 차이를 만듭니다.
처음을 `match`로 바인딩할 때는, 약간의 표현 반복과 외부 `let`을 이용해야 위 표현을 유사하게 구현할 수 있죠:

```rust
# use std::str::FromStr;
# 
# fn get_count_item(s: &str) -> (u64, &str) {
#     let mut it = s.split(' ');
    let (count_str, item) = match (it.next(), it.next()) {
        (Some(count_str), Some(item)) => (count_str, item),
        _ => panic!("Can't segment count item pair: '{s}'"),
    };
    let count = if let Ok(count) = u64::from_str(count_str) {
        count
    } else {
        panic!("Can't parse integer: '{count_str}'");
    };
#     (count, item)
# }
# 
# assert_eq!(get_count_item("3 chairs"), (3, "chairs"));
```

### 함께 읽기:

[option][option], [match][match], [if let][if_let] and the [let-else RFC][let_else_rfc].

[match]: ./match.md
[if_let]: ./if_let.md
[let_else_rfc]: https://rust-lang.github.io/rfcs/3137-let-else.html
[option]: ../std/option.md
