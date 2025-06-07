# for 반복문

## for와 range

`for in` 생성자는 `Iterator`를 이용해 순서를 매길 수 있습니다.
가장 쉬운 방법은 범위 노테이션 `a..b`를 이용하는 거죠.
이는 `a`(포함)부터 `b`(미포함)까지 1 단위로 증가하는 값을 선언합니다.

FizzBuzz를 `while` 대신 `for`를 이용해 작성해봅시다.

```rust,editable
fn main() {
    // `n` will take the values: 1, 2, ..., 100 in each iteration
    for n in 1..101 {
        if n % 15 == 0 {
            println!("fizzbuzz");
        } else if n % 3 == 0 {
            println!("fizz");
        } else if n % 5 == 0 {
            println!("buzz");
        } else {
            println!("{}", n);
        }
    }
}
```

또는, `a..=b`를 이용할 수도 있습니다. 이 표현은 양쪽 끝이 범위에 포함됩니다.
그래서 위 코드는 아래처럼 작성될 수도 있습니다.

```rust,editable
fn main() {
    // `n` will take the values: 1, 2, ..., 100 in each iteration
    for n in 1..=100 {
        if n % 15 == 0 {
            println!("fizzbuzz");
        } else if n % 3 == 0 {
            println!("fizz");
        } else if n % 5 == 0 {
            println!("buzz");
        } else {
            println!("{}", n);
        }
    }
}
```

## for와 반복자

`for in` 구조는 `Iterator`를 여러 방법으로 접근할 수 있습니다.
[반복자][iter] 트레잇에서 얘기했듯이, `for` 반복문은 집합에서 `into_iter` 함수를 적용합니다.
하지만 이것만이 집합을 반복자로 변환하는 방법은 아닙니다.

`into_iter`, `iter`와 `iter_mut`는 내부의 데이터에 대한 서로 다른 시야를 제공함으로서 집합을 반복자로 변환합니다.

* `iter` - 매 반복마다 집합에서 각각의 항목을 빌려옵니다.
  원래 집합을 가져오지 않으므로, 원래 집합을 반복문 후에도 활용할 수 있죠.

```rust, editable
fn main() {
    let names = vec!["Bob", "Frank", "Ferris"];

    for name in names.iter() {
        match name {
            &"Ferris" => println!("There is a rustacean among us!"),
            _ => println!("Hello {}", name),
        }
    }
}
```

* `into_iter` - 원래 집합을 가져다 반복자로 만들기 때문에 매 반복마다 정확히 그 데이터가 제공됩니다.
  원래 집합을 그대로 가져다 썼기 때문에 그 집합이 반복문으로 '이동'했고,
  반복 이후에 해당 집합을 다시 사용할 수도 없습니다.

```rust, editable
fn main() {
    let names = vec!["Bob", "Frank", "Ferris"];

    for name in names.into_iter() {
        match name {
            "Ferris" => println!("There is a rustacean among us!"),
            _ => println!("Hello {}", name),
        }
    }
}
```

* `iter_mut` - 매 반복마다 항목을 수정 가능한 형태로 빌려오며, 그 값이 변경될 수 있도록 해줍니다.

```rust, editable
fn main() {
    let mut names = vec!["Bob", "Frank", "Ferris"];
    //  ^^^ 역주: iter_mut를 호출하려면 원본이 수정 가능해야 합니다. 따라서 mut 키워드를 붙입니다.

    for name in names.iter_mut() {
        *name = match name {
            &mut "Ferris" => "There is a rustacean among us!",
            _ => "Hello",
        }
    }

    println!("names: {:?}", names);
}
```

위 예시에서 `match` 분기의 타입을 확인하세요. 이 부분이 각 반복자 생성 함수의 핵심 차이점입니다.
타입이 다르다는 것은 또한 서로 다른 작업이 가능하다는 것을 의미하기도 합니다.

### 함께 읽기:

[Iterator][iter]

[iter]: ../trait/iter.md
