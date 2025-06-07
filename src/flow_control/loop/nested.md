# 중첩과 라벨링

반복문이 중첩되었을 때 바깥의 반복문을 `break`하거나 `continue`할 수도 있습니다.
이 경우 반복문을 `'라벨`과 함께 선언해야 하며, 대상이 되는 라벨을 `break`/`continue`문에 제공해야 합니다.

```rust,editable
#![allow(unreachable_code)]

fn main() {
    'outer: loop {
        println!("Entered the outer loop");

        'inner: loop {
            println!("Entered the inner loop");

            // This would break only the inner loop
            //break;

            // This breaks the outer loop
            break 'outer;
        } // end of 'inner loop

        println!("This point will never be reached");
    } // end of 'outer loop

    println!("Exited the outer loop");
}
```