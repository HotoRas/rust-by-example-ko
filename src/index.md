# 예제로 배우는 러스트 (Rust by Example) 한국어판

[러스트][rust]는 안전성과 속도 그리고, 병렬 처리에 초점을 맞춘 최신 시스템 프로그래밍 언어
입니다. 러스트는 이를 위해 가비지 컬렉션 기술을 사용하지 않고 메모리 안전성을 지원합니다.

이 문서는 실행 가능한 예제들로 러스트의 여러가지 개념과 표준 라이브러리를 소개합니다. 
예제들을 사용하려면 로컬에 러스트를 [설치][install]하고 [공식 문서][std]도 읽어보기 
바랍니다. 관심있는 분은 이 문서의 [소스][home]도 보아주세요.

(역주: 보고 계신 한글판의 번역은 [여기][home-ko]에서 진행하고 있습니다.)

이제 시작할까요!

- [인사하기](hello.md) - 전통의 Hello World 부터 만들어봅시다.

- [기본 자료형](primitives.md) - 부호있는 정수형과 부호없는 정수형, 기타 기본 자료형들에 대해 배웁시다.

- [사용자 정의 자료형](custom_types.md) - `struct` 와 `enum`.

- [변수 바인딩](variable_bindings.md) - mutable bindings, scope, shadowing.

- [자료형](types.md) - 타입을 변경하고 정의하는 방법에 대해 배워 봅니다.

- [형변환](conversion.md) - String, integer, float와 같은 서로 다른 타입으로 변환해 봅니다.

- [표현식](expression.md) - 표현식과 이를 이용하는 방법에 대해 배워 봅니다.

- [제어문](flow_control.md) - `if`/`else`, `for`, 그리고 여러 다른 것들.

- [함수](fn.md) - Learn about Methods, Closures and High Order Functions.

- [모듈](mod.md) - Organize code using modules

- [크레이트(Crate)](crates.md) - A crate is a compilation unit in Rust. Learn to create a library.

- [카고(Cargo)](cargo.md) - Go through some basic features of the official Rust package management tool.

- [Attributes](attribute.md) - An attribute is metadata applied to some module, crate or item.

- [Generics](generics.md) - Learn about writing a function or data type which can work for multiple types of arguments.

- [Scoping rules](scope.md) - Scopes play an important part in ownership, borrowing, and lifetimes.

- [Traits](trait.md) - A trait is a collection of methods defined for an unknown type: `Self`

- [Macros](macros.md) - Macros are a way of writing code that writes other code, which is known as metaprogramming.

- [Error handling](error.md) - Learn Rust way of handling failures.

- [Std library types](std.md) - Learn about some custom types provided by `std` library.

- [Std misc](std_misc.md) - More custom types for file handling, threads.

- [Testing](testing.md) - All sorts of testing in Rust.

- [Unsafe Operations](unsafe.md) - "안전하지 않은" 동작 블록에 진입하는 방법을 알아봅니다.

- [Compatibility](compatibility.md) - 러스트의 발전과 가능한 호환성 문제를 다룹니다.

- [Meta](meta.md) - Documentation, Benchmarking.


[rust]: https://www.rust-lang.org/
[install]: https://www.rust-lang.org/tools/install
[std]: https://doc.rust-lang.org/std/
[home]: https://github.com/rust-lang/rust-by-example
[home-ko]: https://github.com/rust-kr/rust-by-example-ko
