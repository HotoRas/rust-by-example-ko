# loop에서 리턴하기

`loop`의 용법 중 하나는 작업이 성공할 때까지 반복하는 겁니다. 하지만 작업이 값을 반환하면 나머지를 건너뛸 수도 있겠죠.
반환할 값을 `break` 뒤에 얹어주세요. 값이 `loop` 제어문에서 반환될 겁니다.

```rust,editable
fn main() {
    let mut counter = 0;

    let result = loop {
        counter += 1;

        if counter == 10 {
            break counter * 2;
        }
    };

    assert_eq!(result, 20);
}
```
