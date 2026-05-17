# 타입 캐스팅

러스트는 기본 타입에서 특정하지 않은 경우의 타입 변경(간주하기)을 지원하지 않습니다.
하지만 특정된 타입 변환(캐스팅)은 `as` 키워드를 통해 제공합니다.

일반적인 경우 타입 변환은 C를 준수하지만, C에서 정의되지 않는 경우는 그렇지 않습니다.
러스트는 모든 숫자 타입 변환 방식에 대해 자세하게 정의하고 있습니다.

```rust,editable,ignore,mdbook-runnable
// Suppress all warnings from casts which overflow.
#![allow(overflowing_literals)]

fn main() {
    let decimal = 65.4321_f32;

    // Error! 특정하지 않은 타입 변경 불가
    let integer: u8 = decimal;
    // FIXME ^ Comment out this line

    // 특정된 타입 변환
    let integer = decimal as u8;
    let character = integer as char;

    // Error! 타입 변환에는 제한이 있습니다.
    // float는 char로 바로 변환할 수 없습니다.
    let character = decimal as char;
    // FIXME ^ Comment out this line

    println!("Casting: {} -> {} -> {}", decimal, integer, character);

    // 값을 음수가 없는 타입 T로 캐스팅할 때, 값이 새 타입에 맞아들어갈 때까지
    // T::MAX + 1을 더하거나 뺍니다.

    // 1000은 이미 u16에 들어갑니다
    println!("1000 as a u16 is: {}", 1000 as u16);

    // 1000 - 256 - 256 - 256 = 232
    // 내부적으로, 낮은 8비트 값(LSB)은 유지되고 높은 8비트 값(MSB)는 삭제됩니다.
    println!("1000 as a u8 is : {}", 1000 as u8);
    // -1 + 256 = 255
    println!("  -1 as a u8 is : {}", (-1i8) as u8);

    // 양수에서 이 작업은 modulus와 같습니다
    println!("1000 mod 256 is : {}", 1000 % 256);

    // 음수가 있는 타입으로 변환하면 (이진 수준) 결과가 음수가 없는 것과 동일하게
    // 변환됩니다. 가장 높은 비트가 1이면 음수가 됩니다.

    // 당연히, 이미 맞는 경우엔 딱히 뭐가 없죠.
    println!(" 128 as a i16 is: {}", 128 as i16);

    // 경계면의 경우로, 128의 8비트 2의 보수는 -128입니다
    println!(" 128 as a i8 is : {}", 128 as i8);

    // 위의 예시를 반복합니다
    // 1000 as u8 -> 232
    println!("1000 as a u8 is : {}", 1000 as u8);
    // 그리고 232의 2의 보수는 -24죠
    println!(" 232 as a i8 is : {}", 232 as i8);
    
    // 러스트 1.45부터, `as` 키워드가 float -> int 캐스팅에서 
    // *saturating cast*로 동작합니다. 부동소수점 값이 최대값을 넘거나 최소값보다
    // 작아지면, 그 결과값은 그 경계값이 됩니다.
    
    // 300.0 as u8 is 255
    println!("300.0 is {}", 300.0_f32 as u8);
    // -100.0 as u8 is 0
    println!("-100.0 as u8 is {}", -100.0_f32 as u8);
    // nan as u8 is 0
    println!("nan as u8 is {}", f32::NAN as u8);
    
    // 약간의 런타임 비용을 소모하며, unsafe 메서드를 이용해 피할 수 있습니다.
    // 결과값이 오버플로우되어 **이상한 값**을 리턴하는 경우도 있으니,
    // 현명하게 사용해 주세요!
    unsafe {
        // 역주: unsafe fn {f32, f64}.to_int_unchecked::<T> -> T
        //       where T is one of
        //         {u8 u16, u32, u64, u128, i8, i16, i32, i64, i128}

        // 300.0 is 44
        println!("300.0 is {}", 300.0_f32.to_int_unchecked::<u8>());
        // -100.0 as u8 is 156
        println!("-100.0 as u8 is {}", (-100.0_f32).to_int_unchecked::<u8>());
        // nan as u8 is 0
        println!("nan as u8 is {}", f32::NAN.to_int_unchecked::<u8>());
    }
}
```
