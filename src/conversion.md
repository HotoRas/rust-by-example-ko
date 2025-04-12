# 타입 변환

기본 타입은 [캐스팅][casting]을 통해 변환이 가능합니다.

러스트에서는 커스텀 타입(`struct`, `enum`과 같은)간의 전환을 [트레잇][traits]을 이용해
진행합니다. 기본적인 변환은 [`From`]과 [`Into`] 트레잇을 이용합니다. 하지만
더 흔한 경우에 대해 특정한 행위가 있을 수 있습니다. 특히 `String`으로,
또는 `String`에서 전환하는 경우엔 말이죠.

[casting]: types/cast.md
[traits]: trait.md
[`From`]: https://doc.rust-lang.org/std/convert/trait.From.html
[`Into`]: https://doc.rust-lang.org/std/convert/trait.Into.html
