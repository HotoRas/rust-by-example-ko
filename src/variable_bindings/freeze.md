# 고정하기

수정 가능한 변수가 같은 이름의 수정되지 않는 변수로 추가 선언되면, *고정* 상태가
됩니다. *고정된* 데이터는 수정되지 않는 변수의 스코프 밖으로 나갈 때까지 수정할 수
없게 됩니다:

```rust,editable,ignore,mdbook-runnable
fn main() {
    let mut _mutable_integer = 7i32;

    {
        // Shadowing by immutable `_mutable_integer`
        let _mutable_integer = _mutable_integer;

        // Error! `_mutable_integer` is frozen in this scope
        _mutable_integer = 50;
        // FIXME ^ Comment out this line

        // `_mutable_integer` goes out of scope
    }

    // Ok! `_mutable_integer` is not frozen in this scope
    _mutable_integer = 3;
}
```
