# use

`use` 선언을 통해 수동으로 스코핑하지 않고도 내부 상수를 이용할 수 있습니다:

```rust,editable
// An attribute to hide warnings for unused code.
#![allow(dead_code)]

enum Stage {
    Beginner,
    Advanced,
}

enum Role {
    Student,
    Teacher,
}

fn main() {
    // 각각을 `use`함으로서 스코핑 없이 사용하도록 합니다
    use crate::Stage::{Beginner, Advanced};
    // `Role` 안의 모든 항목을 자동으로 `use`합니다
    use crate::Role::*;

    //`Stage::Beginner`와 동일
    let stage = Beginner;
    // `Role::Student`와 동일
    let role = Student;

    match stage {
        // 위에서 `use`를 사용함으로서 수동 스코핑이 없음을 주목하세요
        Beginner => println!("Beginners are starting their learning journey!"),
        Advanced => println!("Advanced learners are mastering their subjects..."),
    }

    match role {
        // Note again the lack of scoping.
        Student => println!("Students are acquiring knowledge!"),
        Teacher => println!("Teachers are spreading knowledge!"),
    }
}
```

### 함께 읽기:

[`match`][match]와 [`use`][use]

[use]: ../../mod/use.md
[match]: ../../flow_control/match.md
