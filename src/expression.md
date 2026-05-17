# 표현식

(대부분의) 러스트 프로그램은 선언문들로 이루어져 있습니다.

```rust,editable
fn main() {
    // statement
    // statement
    // statement
}
```

러스트엔 몇몇 종류의 선언문이 있습니다.
가장 흔한 것은 변수 선언과 표현식 끝에 `;`를 두는 것이죠:

```rust,editable
fn main() {
    // variable binding
    let x = 5;

    // expression;
    x;
    x + 1;
    15;
}
```

블록 또한 표현식이어서, 값이나 대입에 사용될 수 있습니다. 블록의 가장 마지막 표현식의
결과가 내부 변수와 같은 대응식에 전달됩니다. 하지만 마지막 표현식이 `;`로 끝난다면,
`()`가 리턴됩니다.

```rust,editable
fn main() {
    let x = 5u32;

    let y = {
        let x_squared = x * x;
        let x_cube = x_squared * x;

        // This expression will be assigned to `y`
        x_cube + x_squared + x
    };

    let z = {
        // The semicolon suppresses this expression and `()` is assigned to `z`
        2 * x;
    };

    println!("x is {:?}", x);
    println!("y is {:?}", y);
    println!("z is {:?}", z);
}
```
