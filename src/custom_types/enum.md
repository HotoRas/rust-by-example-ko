# 열거형

`enum` 키워드는 여러 종류 중 하나일 수 있는 타입을 만들 수 있게 해줍니다.
`struct`에서 유효한 어느 타입도 `enum`에서 유효합니다.

```rust,editable
// 웹 이벤트를 클래스화하는 `enum`을 생성합니다.
// 이름과 타입 정보가 어떻게 선언되는지에 주목하세요:
// `PageLoad != PageUnload`이고 `KeyPress(char) != Paste(string)`입니다.
// 각각은 서로 다르고 독립적입니다.
enum WebEvent {
    // `enum`의 각 항목은 `unit-like`일수도,
    PageLoad,
    PageUnload,
    // 튜플 구조체일수도,
    KeyPress(char),
    Paste(String),
    // C 스타일 구조체일 수도 있습니다.
    Click { x: i64, y: i64 },
}

// `WebEvent` 열거형을 받아 아무것도 리턴하지 않는 함수입니다.
// 역주: 함수가 정상적으로 종료되고 로직이 이어지므로 `()`를 리턴하는 것으로
//       해석할 수 있습니다.
fn inspect(event: WebEvent) {
    match event {
        WebEvent::PageLoad => println!("page loaded"),
        WebEvent::PageUnload => println!("page unloaded"),
        // Destructure `c` from inside the `enum` variant.
        WebEvent::KeyPress(c) => println!("pressed '{}'.", c),
        WebEvent::Paste(s) => println!("pasted \"{}\".", s),
        // Destructure `Click` into `x` and `y`.
        WebEvent::Click { x, y } => {
            println!("clicked at x={}, y={}.", x, y);
        },
    }
}

fn main() {
    let pressed = WebEvent::KeyPress('x');
    // `to_owned()` creates an owned `String` from a string slice.
    let pasted  = WebEvent::Paste("my text".to_owned());
    let click   = WebEvent::Click { x: 20, y: 80 };
    let load    = WebEvent::PageLoad;
    let unload  = WebEvent::PageUnload;

    inspect(pressed);
    inspect(pasted);
    inspect(click);
    inspect(load);
    inspect(unload);
}

```

## 타입 별칭

타입 별칭을 사용하면 각 열거형의 항목을 별칭으로 호출할 수 있습니다.
열거형의 이름이 너무 길거나 너무 일반적이어서,
이름을 다시 지정하고 싶을 때 유용합니다.

```rust,editable
enum 이름이아주긴_숫자로할수있는작업_열거형 {
    Add,
    Subtract,
}

// Creates a type alias
type Operations = 이름이아주긴_숫자로할수있는작업_열거형;

fn main() {
    // We can refer to each variant via its alias, not its long and inconvenient
    // name.
    let x = Operations::Add;
}
```

가장 자주 볼 수 있는 곳은 `impl` 블록의 `Self` 별칭일 것입니다.

```rust,editable
enum VeryVerboseEnumOfThingsToDoWithNumbers {
    Add,
    Subtract,
}

impl VeryVerboseEnumOfThingsToDoWithNumbers {
    fn run(&self, x: i32, y: i32) -> i32 {
        match self {
            Self::Add => x + y,
            Self::Subtract => x - y,
        }
    }
}
```

열거형과 타입 별칭에 대해 더 알고 싶다면,
이 기능이 Rust로서 안정화될 때의 [안정화 리포트][aliasreport]를
참고할 수 있습니다.

### 함께 읽기:

[`match`][match], [`fn`][fn]과 [`String`][str], ["Type alias enum variants" RFC][type_alias_rfc]

[c_struct]: https://en.wikipedia.org/wiki/Struct_(C_programming_language)
[match]: ../flow_control/match.md
[fn]: ../fn.md
[str]: ../std/str.md
[aliasreport]: https://github.com/rust-lang/rust/pull/61682/#issuecomment-502472847
[type_alias_rfc]: https://rust-lang.github.io/rfcs/2338-type-alias-enum-variants.html
