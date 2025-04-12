# 테스트 케이스: 연결 리스트

통상적으로 연결 리스트를 구현하는 방법은 `enum`을 활용하는 것입니다:

```rust,editable
// 역주: 이렇게 하면 해당 파일 전체에서 `List` 하위 객체를
//       스코핑 없이 바로 접근할 수 있게 됩니다.
use crate::List::*;

enum List {
    // Cons: 항목과 다음 노드로의 포인터를 감싸는 튜플 구조체
    Cons(u32, Box<List>),
    // Nil: 연결 리스트의 끝을 나타내는 선언자
    Nil,
}

// 열거형도 메서드를 붙일 수 있습니다
impl List {
    // 빈 `List`를 생성합니다
    fn new() -> List {
        // `Nil`은 `List` 타입입니다
        Nil
    }

    // `List`의 소유권을 가져와, 새 항목이 맨 앞에 추가된 `List`를
    // 만들어 리턴합니다.
    fn prepend(self, elem: u32) -> List {
        // `Cons`도 `List` 타입입니다
        Cons(elem, Box::new(self))
    }

    // `List`의 길이를 리턴합니다
    fn len(&self) -> u32 {
        // `self`의 종류에 따라 행동이 바뀌기에 매칭이 필요합니다.
        // `self`는 `&List` 타입이고 `*self`는 `List` 타입이며,
        // 정적 타입 `T`가 `&T`보다 매칭에 선호됩니다.
        // Rust 2018부터는 레퍼런스 없이 self나 tail을 사용할 수 있으며,
        // 이때 러스트는 `&s`와 `ref tail`을 추정해 컴파일합니다.
        // 더 보기: https://doc.rust-lang.org/edition-guide/rust-2018/ownership-and-lifetimes/default-match-bindings.html
        match *self {
            // `self`가 빌려온 것으로 `tail`을 가져올 수 없어, 이의 레퍼런스를
            // 가져옵니다.
            Cons(_, ref tail) => 1 + tail.len(),
            // 빈 리스트는 기본적으로 0의 길이이죠.
            Nil => 0
        }
    }

    // 리스트 전체를 (heap 할당된) `String`으로 리턴합니다
    fn stringify(&self) -> String {
        match *self {
            Cons(head, ref tail) => {
                // `format!`은 `print!`와 유사하지만, 콘솔에 뿌리는 대신
                // heap 할당된 string을 리턴합니다
                format!("{}, {}", head, tail.stringify())
            },
            Nil => {
                format!("Nil")
            },
        }
    }
}

fn main() {
    // 빈 연결 리스트를 만듭니다
    let mut list = List::new();

    // 서두에 아이템 몇 개를 추가합니다
    list = list.prepend(1);
    list = list.prepend(2);
    list = list.prepend(3);

    // 최종 상태를 확인합니다
    println!("linked list has length: {}", list.len());
    println!("{}", list.stringify());
}
```

### 함께 읽기:

[`Box`][box]와 [methods][methods]

[box]: ../../std/box.md
[methods]: ../../fn/methods.md
