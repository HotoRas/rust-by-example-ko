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

- [변수 바인딩](variable_bindings.md) - 수정 가능한 변수와 스코프, 섀도잉.

- [자료형](types.md) - 타입을 변경하고 정의하는 방법에 대해 배워 봅니다.

- [형변환](conversion.md) - String, integer, float와 같은 서로 다른 타입으로 변환해 봅니다.

- [표현식](expression.md) - 표현식과 이를 이용하는 방법에 대해 배워 봅니다.

- [제어문](flow_control.md) - `if`/`else`, `for`, 그리고 여러 다른 것들.

- [함수](fn.md) - 메서드, 클로저와 상위 순서의 함수를 알아봅시다.

- [모듈](mod.md) - 모듈을 통해 코드를 정리해봅시다.

- [크레이트(Crate)](crates.md) - 크레이트는 러스트의 컴파일 단위입니다. 라이브러리도 만들어봅시다.

- [카고(Cargo)](cargo.md) - 러스트의 공식 패키지 관리 툴의 기본 기능을 알아봅시다.

- [속성](attribute.md) - 속성은 모듈, 크레이트 또는 아이템에 적용하는 메타데이터입니다.

- [제네릭](generics.md) - 여러 타입의 매개변수를 가지는 함수나 데이터 타입을 작성하는 법을 알아봅시다.

- [스코프 규칙](scope.md) - 스코프는 소유권, 빌리기와 수명 주기에 중요한 역할을 합니다.

- [트레잇](trait.md) - 트레잇은 알 수 없는 타입 `Self`를 위해 선언된 메서드 모음입니다.

- [매크로](macros.md) - 매크로는 다른 코드를 작성하는 코드로, 메타프로그래밍이라고 부르기도 합니다.

- [오류 다루기](error.md) - 러스트에서 실패를 다루는 법을 배워봅니다.

- [std 라이브러리 타입](std.md) - `std` 라이브러리에서 제공하는 몇몇 커스텀 타입을 알아봅시다.

- [std 라이브러리 잡동사니](std_misc.md) - 파일 핸들링과 스레드에 대한 더 많은 커스텀 타입입니다.

- [테스트하기](testing.md) - 러스트에서의 모든 방식의 테스트.

- [Unsafe한 작업](unsafe.md) - "안전하지 않은" 동작 블록에 진입하는 방법을 알아봅니다.

- [호환성](compatibility.md) - 러스트의 발전과 가능한 호환성 문제를 다룹니다.

- [메타데이터](meta.md) - 문서화와 벤치마크.


[rust]: https://www.rust-lang.org/
[install]: https://www.rust-lang.org/tools/install
[std]: https://doc.rust-lang.org/std/
[home]: https://github.com/rust-lang/rust-by-example
[home-ko]: https://github.com/rust-kr/rust-by-example-ko
