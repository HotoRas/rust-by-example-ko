# 우선 선언하기

변수 할당을 우선 선언하고 나중에 초기화할 수도 있지만, 모든 변수는 사용되기 전에
초기화되어야 합니다: 컴파일러가 초기화되지 않은 변수의 사용을 금지하며, 이는
지정되지 않은 행위로 이어질 수 있기 때문입니다.

변수의 선언과 초기화를 따로 하는 경우는 흔치 않습니다. 코드를 읽을 때 초기화문이
떨어져 있으면 이를 찾기도 어렵고요. 변수 자체를 그 변수가 사용되는 곳 근처에 선언하는
경우가 일반적입니다.

```rust,editable,ignore,mdbook-runnable
fn main() {
    // Declare a variable binding
    let a_binding;

    {
        let x = 2;

        // Initialize the binding
        a_binding = x * x;
    } // 역주: a_binding을 초기화하기 위해 사용한 x: i32는 이제 없습니다

    println!("a binding: {}", a_binding);

    let another_binding;

    // Error! Use of uninitialized binding
    println!("another binding: {}", another_binding);
    // FIXME ^ Comment out this line

    another_binding = 1;

    println!("another binding: {}", another_binding);
}
```
