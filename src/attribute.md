# Attributes

Attribute는 모듈, 크레이트 또는 아이템에 붙이는 메타데이터로,
다음과 같은 상황에 사용할 수 있습니다:

<!-- TODO: Link these to their respective examples -->

* [코드의 조건부 컴파일][cfg]
* [크레이트의 이름, 버전과 종류 지정 (바이너리나 라이브러리)][crate]
* [린팅][lint] (경고) 비활성화
* 컴파일러 기능 활성화 (매크로, 글로벌 임포트 등)
* 외부 라이브러리에 링크
* 함수를 유닛의 테스트로 표시
* 함수를 벤치마크의 일부로 표시
* [Attribute화 매크로][macros]

Attribute는 `#[outer_attribute]`나 `#![inner_attribute]`로 표기하며,
각각에 따라 적용하는 지점이 다릅니다.

* `#[outer_attribute]`는 이어지는 [항목][item]에 바로 적용됩니다.
  예를 들어 함수, 모듈 선언, 상수, 구조체, enum 등이 있습니다.
  구조체 `Rectangle`에 attribute `#[derive(debug)]`가 적용되는 예를 들어보겠습니다:

  ```rust
  #[derive(Debug)]
  struct Rectangle {
      width: u32,
      height: u32,
  }
  ```

* `#![inner_attribute]`는 이를 포함하는 [아이템][item] (보통 모듈 또는 크레이트) 전체에 적용됩니다.
  즉, 이는 배치된 모든 스코프에 적용하는 것으로 해석됩니다.
  `main.rs`에 배치함으로서 `#![allow(unused_variables)]`가 크레이트 전체에 적용되는 예를 들어보겠습니다:

  ```rust
  #![allow(unused_variables)]

  fn main() {
      let x = 3; // This would normally warn about an unused variable.
  }
  ```

Attribute는 여러 방식으로 인수를 받을 수 있습니다:

* `#[attribute = "value"]`
* `#[attribute(key = "value")]`
* `#[attribute(value)]`

인수를 여러 개 받을 수도, 여러 줄에 걸쳐 받을 수도 있습니다:

```rust,ignore
#[attribute(value, value2)]


#[attribute(value, value2, value3,
            value4, value5)]
```

[cfg]: attribute/cfg.md
[crate]: attribute/crate.md
[item]: https://doc.rust-lang.org/stable/reference/items.html
[lint]: https://en.wikipedia.org/wiki/Lint_%28software%29
[macros]: https://doc.rust-lang.org/book/ch19-06-macros.html#attribute-like-macros
