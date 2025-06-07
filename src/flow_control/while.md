# while

`while` 키워드는 조건이 참인 동안 반복할 때 사용할 수 있습니다.

유명한 [FizzBuzz][fizzbuzz] 예제를 `while` 반복을 이용해 작성해봅시다.

```rust,editable
fn main() {
    // A counter variable
    let mut n = 1;

    // Loop while `n` is less than 101
    while n < 101 {
        if n % 15 == 0 {
            println!("fizzbuzz");
        } else if n % 3 == 0 {
            println!("fizz");
        } else if n % 5 == 0 {
            println!("buzz");
        } else {
            println!("{}", n);
        }

        // Increment counter
        n += 1;
    }
}
```

[fizzbuzz]: https://en.wikipedia.org/wiki/Fizz_buzz
