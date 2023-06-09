# 3.2 基本数据类型

Rust 是静态类型语言，编译时就必须知道所有变量的类型。根据值以及其使用方式，Rust 编译器通常能自动推导出变量的类型。Rust 有两种数据类型子集，分别是：标量（scalar）类型和复合（compound）类型。

## 3.2.1 标量类型

标量类型包括：整型、浮点型、布尔类型和字符类型。

### 3.2.1.1 整型和浮点型

Rust 中的整型和浮点型如下：

| 长度    | 有符号 | 无符号 | 浮点型 |
|---------|--------|--------|--------|
| 8 bit   | i8     | u8     |        |
| 16 bit  | i16    | u16    |        |
| 32 bit  | i32    | u32    | f32    |
| 64 bit  | i64    | u64    | f64    |
| 128 bit | i128   | u128   |        |
| arch    | isize  | usize  |        |

说明：`isize` 和 `usize` 的长度是和平台相关，如果 CPU 是 32 位的，则这两个类型是 32 位的，如果 CPU 是 64 位的，则这两个类型是 64 位的。

上面的表格中，`f32` 和 `f64` 为浮点型，其它为整型。浮点型和整型一起构成数值类型。

（1）可以在数值字面量后面加上类型表示该数值的类型，如下：

```rust
fn main(){
  let _a = 33u32;    // 直接加类型后缀
  let _b = 33_i32;   // 使用 _ 分隔数值和类型
  let _c = 33_isize;
  let _d = 33_f32;
}
```

（2）可以在数值的任意位置使用下划线分割来增强可读性，如下：

```rust
fn main(){
  let _a = 10_000_000u32;
  let _b = 1_234_3_u32;
  let _c = 1_33_333f32;
}
```

（3）当既不明确指定变量的类型，也不明确指定数值字面量的类型后缀时，Rust 默认将整数当做 `i32` 类型，将浮点数当做 `f64` 类型，如下：

```rust
fn main(){
  let _a = 33;     // 等价于 let _a: i32 = 33;     等价于 let _a = 33i32;
  let _b = 64.123; // 等价于 let _b: f64 = 64.123; 等价于 let _b = 64.123f64;
}
```

（4）Rust 使用 `0b` 表示二进制、`0o` 表示八进制、`0x` 表示十六进制，如下：

```rust
fn main(){
  let a: u32 = 0b101; // 二进制整数
  let b: i32 = 0o17;  // 八进制整数
  let c: u8 = 1;      // 十进制
  let d: i32 = 0xac;  // 十六进制整数
  println!("{}, {}, {}, {}", a, b, c, d); // 5, 15, 1, 172
}
```

（5）Rust 中所有的数值类型都支持基本数学运算：加、减、乘、除、取余，如下：

```rust
fn main() {
    let sum = 5 + 10;
    let difference = 95.5 - 4.3;
    let product = 4 * 30;
    let quotient = 56.7 / 32.2;
    let truncated = -5 / 3; // 结果为 -1
    let remainder = 43 % 5;
}
```

### 3.2.1.2 布尔型

Rust 中的布尔型用 `bool` 表示，有两个可能的值，为 `true` 和 `false`。布尔类型使用的场景主要是条件表达式（控制流的内容），使用如下：

```rust
fn main() {
    // 定义方式
    let a: bool = true;
    let b: bool = false;

    // 使用场景
    if a {
        println!("a is true");
    } else {
        println!("a is false");
    }

    if b {
        println!("b is true");
    } else {
        println!("b is false");
    }
}
```

### 3.2.1.3 字符类型

Rust 用 `char` 表示字符类型，用于存放单个 unicode 字符，占用 4 个字节空间。当存储 `char` 类型数据时，Rust 会将其转换为 utf-8 编码的数据存储。`char` 字面量是单引号包裹的任意单个字符，字符类型使用示例如下：

```rust
fn main() {
    let c: char = 'z';
    let x: char = 'x';
    let heart_eyed_cat: char = '😻';
}
```

## 3.2.2 原生复合类型

复合类型是将多个值组合成一个类型。Rust 有两个原生复合类型：元组和数组。

### 3.2.2.1 元组

圆括号以及其中逗号分割的值列表组成元组，定义一个元组方式如下：

```rust
fn main() {
    let tup: (i32, f64, u8) = (500, 6.4, 1);
}
```

可以将元组重新解构到变量上，如下：

```rust
fn main() {
    let tup = (500, 6.4, 1);
    let (x, y, z) = tup;
    // 接下来你可以使用 x、y、z
}
```

也可以直接使用元组的元素，如下：

```rust
fn main() {
    let x: (i32, f64, u8) = (500, 6.4, 1);
    let first = x.0;
    let second = x.1;
    let third = x.2;
}
```

不带任何值的元组，称为 `unit` 类型（单元元组），可以代表空值或者空的返回类型，如下：

```rust
fn main() {
    let x: () = (); // 将值 () 保存到类型为 () 的变量 x 中
}
```

### 3.2.2.2 数组

数组中的每个元素的类型必须相同，数组的长度是固定的，数组的定义方式如下：

```rust
fn main() {
    let a = [1, 2, 3, 4, 5];           // 直接写数组的值
    let b: [i32; 5] = [1, 2, 3, 4, 5]; // 显示指定数组的类型和长度
    let c: [i32; 5] = [3; 5];          // 数组每个元素为同样的值，等价于 let a = [3, 3, 3, 3, 3];
}
```

数组通过索引来访问元素，索引从 0 开始计数，如下：

```rust
fn main() {
    let a = [1, 2, 3, 4, 5];

    let first = a[0];   // first = 1
    let second = a[1];  // second = 2
}
```

Rust 中，访问无效的索引元素会报错，如下：

```rust
fn main() {
    let a = [1, 2, 3, 4, 5];
    let b = a[5]; // 错误，只能放为 0~4，所以这个代码将无法编译
}
```

## 3.2.3 类型转换

TODO (少一个From, Into, TryFrom, TryInto)

Rust 中可以使用 `as` 进行类型转换。

- 数值类型之间默认不会隐式转换，如果要转换，则需手动使用 `as` 进行转换。
- `bool` 类型可以转换为各种数值类型，`false` 对应 `0`，`true` 对应 `1`。
- 可以使用 `as` 将 `char` 类型转换为各种整型，目标类型小于 4 字节时，会从高位截断。
- 可以使用 `as` 将 `u8` 转换为 `char` 类型。
- 可以使用 `std::char::from_u32` 将 `u32` 转换为 `char` 类型。
- 可以使用 `std::char::from_digit` 将十进制整型转换为 `char` 类型。

```rust
fn main() {
    // 数值类型的转换
    assert_eq!(10i8 as u16, 10u16);
    assert_eq!(123u16 as i16, 123i16);
    // bool 类型转换
    assert_eq!(false as u32, 0u32);
    assert_eq!(true as i8, 1i8);
    // char 类型相关转换
    assert_eq!('我' as i32, 25105i32);  // char 转换到 i32
    assert_eq!('是' as u8, 47u8);       // char 转换到 u8，会被截断
    assert_eq!(97u8 as char, 'a');      // u8 转换到 char
    assert_eq!(std::char::from_u32(0x2764).unwrap(), '❤');
    assert_eq!(std::char::from_digit(4, 10).unwrap(), '4');
}
```
