# 구조체

`struct` 키워드로 만들 수 있는 구조체에는 3가지 타입이 있습니다.

* 튜플 구조체. 이것은 기본적으로 네임드 튜플입니다.
* 고전적인 [C 언어의 구조체][c_struct].
* 유닛 구조체. 필드가 없는 제너릭에 유용한 구조체입니다.

```rust,editable
// 미사용 코드에 대한 오류를 숨기기 위해
#![allow(dead_code)]

#[derive(Debug)]
struct Person {
    name: String,
    age: u8,
}

// 유닛 구조체
struct Unit;

// 튜플 구조체
struct Pair(i32, f32);

// 2개의 필드를 가진 구조체
struct Point {
    x: f32,
    y: f32,
}

// 구조체는 다른 구조체의 필드로 이용될 수 있습니다
struct Rectangle {
    // A rectangle can be specified by where the top left and bottom right
    // corners are in space.
    top_left: Point,
    bottom_right: Point,
}

fn main() {
    // Create struct with field init shorthand
    let name = String::from("Peter");
    let age = 27;
    let peter = Person { name, age };

    // Print debug struct
    println!("{:?}", peter);


    // Instantiate a `Point`
    let point: Point = Point { x: 5.2, y: 0.4 };
    let another_point: Point = Point { x: 10.3, y: 0.2 };

    // Access the fields of the point
    println!("point coordinates: ({}, {})", point.x, point.y);

    // Make a new point by using struct update syntax to use the fields of our
    // other one
    let bottom_right = Point { x: 10.3, ..another_point };

    // `bottom_right.y` will be the same as `point.y` because we used that field
    // from `point`
    println!("second point: ({}, {})", bottom_right.x, bottom_right.y);

    // Destructure the point using a `let` binding
    let Point { x: left_edge, y: top_edge } = point;

    let _rectangle = Rectangle {
        // struct instantiation is an expression too
        top_left: Point { x: left_edge, y: top_edge },
        bottom_right: bottom_right,
    };

    // Instantiate a unit struct
    let _unit = Unit;

    // Instantiate a tuple struct
    let pair = Pair(1, 0.1);

    // Access the fields of a tuple struct
    println!("pair contains {:?} and {:?}", pair.0, pair.1);

    // Destructure a tuple struct
    let Pair(integer, decimal) = pair;

    println!("pair contains {:?} and {:?}", integer, decimal);
}
```

### 실습

1. 직사각형의 넓이를 계산하는 `rect_area` 함수를 추가해보세요.
    (아이템 중첩 해체를 활용해보세요)
2. `Point`와 `f32`를 인수로 받아 왼쪽 바닥의 점을 `Point`에서,
    폭과 높이를 `f32`에서 계산해 `Rectangle`을 리턴하는
    `square` 함수를 추가해보세요.

### 참고

[`attributes`][attributes], [raw identifiers][raw_identifiers]와 [destructuring][destructuring]

[attributes]: ../attribute.md
[c_struct]: https://ko.wikipedia.org/wiki/Struct_(C_programming_language)
[destructuring]: ../flow_control/match/destructuring.md
[raw_identifiers]: ../compatibility/raw_identifiers.md
