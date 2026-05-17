# 변수 할당

러스트는 정적 타입을 이용해 타입 안전을 제공합니다. 이에 따라 변수를 할당할 때 타입을
지정할 수 있습니다. 하지만 대부분의 경우, 컴파일러가 타입을 사용으로부터 추정할
수 있기 때문에, 타입 선언의 필요성이 크게 줄어듭니다.

리터럴과 같은 모든 값은 `let` 바인딩을 통해 변수에 할당할 수 있습니다.

```rust,editable
fn main() {
    let an_integer = 1u32;
    let a_boolean = true;
    let unit = ();

    // copy `an_integer` into `copied_integer`
    let copied_integer = an_integer;

    println!("An integer: {:?}", copied_integer);
    println!("A boolean: {:?}", a_boolean);
    println!("Meet the unit value: {:?}", unit);

    // The compiler warns about unused variable bindings; these warnings can
    // be silenced by prefixing the variable name with an underscore
    let _unused_variable = 3u32;

    let noisy_unused_variable = 2u32;
    // FIXME ^ Prefix with an underscore to suppress the warning
}
```