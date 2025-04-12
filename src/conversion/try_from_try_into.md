# `TryFrom`과 `TryInto`

[`From`과 `Into`][from-into]와 비슷하게, [`TryFrom`]과 [`TryInto`]는 두 타입간
변환을 수행하는 표준 트레잇입니다. `From`/`Into`와 다르게 `TryFrom`/`TryInto`는
실패할 수 있는 변환을 위해 사용하며, 그에 따라 [`Result`]를 반환하죠.

[from-into]: from_into.html
[`TryFrom`]: https://doc.rust-lang.org/std/convert/trait.TryFrom.html
[`TryInto`]: https://doc.rust-lang.org/std/convert/trait.TryInto.html
[`Result`]: https://doc.rust-lang.org/std/result/enum.Result.html

```rust,editable
use std::convert::TryFrom;
use std::convert::TryInto;

#[derive(Debug, PartialEq)]
struct EvenNumber(i32);

impl TryFrom<i32> for EvenNumber {
    type Error = ();

    fn try_from(value: i32) -> Result<Self, Self::Error> {
        if value % 2 == 0 {
            Ok(EvenNumber(value))
        } else {
            Err(())
        }
    }
}

fn main() {
    // TryFrom

    assert_eq!(EvenNumber::try_from(8), Ok(EvenNumber(8)));
    assert_eq!(EvenNumber::try_from(5), Err(()));

    // TryInto

    let result: Result<EvenNumber, ()> = 8i32.try_into();
    assert_eq!(result, Ok(EvenNumber(8)));
    let result: Result<EvenNumber, ()> = 5i32.try_into();
    assert_eq!(result, Err(()));
}
```
