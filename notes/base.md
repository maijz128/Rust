
# 基础（语言通用）


## 变量

### 绑定

```rust
let nub = 5;
```

### 类型注解

```rust
let nub: i32 = 5;
```

### 可变性

变量默认不可变，可变需要设置为`mut`

```rust
let mut nub: i32 = 5;
nub = 11;
```

### 覆盖（Shadowing）

定义一个与之前变量名称相同的新变量，而新变量会覆盖之前的变量。
可以用相同变量名称来覆盖它自己以及重复使用let关键字来多次覆盖。

```javascript
//  js
var str ='123';
var int = 123;
str = int;      //  ok
```

```csharp
//  c#
string  _str = "123";
int     _int =  123;
_str =  _int;   //  error
```

```rust
//  rust
let _str = "123";
let _int =  123;
let _str = _int;    //  ok
```


### 输出（Print）

例：在终端输出 `a: 1, b: 2`

```rust
let a = 1;
let b = 2;
println!("a: {}, b: {}", a, b);

```

字符串内的`{}`为输出占位符

## 函数

函数`add_nub`有一个名字是`nub`类型为`i32`的参数，和一个类型为`i32`的返回值，返回值是`nub + 1`表达式的结果

```rust
fn add_nub(nub: i32) -> i32{
    // do some thing

    nub + 1
}
```

### 提早返回`return`

```rust
fn foo(x: i32) -> i32 {
    return x;

    // we never run this code!
    x + 1
}
```

### 函数指针

```rust
fn plus_one(i: i32) -> i32 {
    i + 1
}

// without type inference
let f: fn(i32) -> i32 = plus_one;

// with type inference
let f = plus_one;

let six = f(5);
```



## 类型

### bool（布尔）

```rust
let t = true;

let f: bool = false;
```

### char（字符）

`char`类型代表一个单独的 Unicode 字符的值。在Rust中`char`占4个字节

```rust
let x = 'x';
let two_hearts = '💕';
```

### 数字类型

默认类型：

```rust
let x = 42; // x has type i32

let y = 1.0; // y has type f64
```




数字类型列表：


|   type   | 符号  |  位   |类型    |
|----------|:-----:|:------:|:----:|
|[i8][i8]       | 有    |  8       | 整数
|[i16][i16]     | 有    |  16      | 整数
|[i32][i32]     | 有    |  32      | 整数
|[i64][i64]     | 有    |  64      | 整数
|[u8][u8]       | 无    |  8       | 整数
|[u16][u16]     | 无    |  16      | 整数
|[u32][u32]     | 无    |  32      | 整数
|[u64][u64]     | 无    |  64      | 整数
|[isize][isize] | 有    | 依赖底层  | 整数
|[usize][usize] | 无    | 依赖底层  | 整数
|[f32][f32]     | 有    |  32      | 单精度浮点数
|[f64][f64]     | 有    |  64      | 双精度浮点数

[i8]: http://doc.rust-lang.org/std/primitive.i8.html
[i16]: http://doc.rust-lang.org/std/primitive.i16.html
[i32]: http://doc.rust-lang.org/std/primitive.i32.html
[i64]: http://doc.rust-lang.org/std/primitive.i64.html
[u8]: http://doc.rust-lang.org/std/primitive.u8.html
[u16]: http://doc.rust-lang.org/std/primitive.u16.html
[u32]: http://doc.rust-lang.org/std/primitive.u32.html
[u64]: http://doc.rust-lang.org/std/primitive.u64.html
[isize]: http://doc.rust-lang.org/std/primitive.isize.html
[usize]: http://doc.rust-lang.org/std/primitive.usize.html
[f32]: http://doc.rust-lang.org/std/primitive.f32.html
[f64]: http://doc.rust-lang.org/std/primitive.f64.html



### 数组

数组默认是不可变的。 
类型是`[T; N]`。

```rust
let a = [1, 2, 3]; // a: [i32; 3]
let mut m = [1, 2, 3]; // m: [i32; 3]
```

初始化简写：`a`的每个元素都被初始化为`1`

```rust
let a = [1, 20] // a: [i32; 20]
```

长度：`a.len()`

访问*下标*：`a[0]`

切片： 


### 元组（Tuples）

元组（tuples）是固定大小的有序列表。

```rust
let x = (1, "hello");
```

访问索引： 

```rust
let x0 = x.0; //  1
let x1 = x.1; //  hello
```

### 字符串（String）


字符串 slice



## 运算符


关系运算符 |  作用     | 重载（trait）
----------|:---------:|:---------:
==        |  等于     |   [PartialEq][PartialEq]
!=        |  不等于   |   [PartialEq][PartialEq]
\>        |  大于     |   [PartialOrd][PartialOrd]
\>=       |  大于等于  |  [PartialOrd][PartialOrd]
<         |  小于     |   [PartialOrd][PartialOrd]
<=        |  小于等于  |  [PartialOrd][PartialOrd]
&#124;&#124;          |   逻辑或
&&                    |   逻辑与

[PartialEq]: https://doc.rust-lang.org/core/cmp/trait.PartialEq.html
[PartialOrd]: https://doc.rust-lang.org/core/cmp/trait.PartialOrd.html

算术运算符 |   作用     | 重载（trait）
----------|:----------:|:---------:
\+        |  加法      |   [Add][Add]
\-        |  减法      |   [Sub][Sub]
\*        |  乘法      |   [Mul][Mul]
/         |  除法      |   [Div][Div]
%         |  取余      |   [Rem][Rem]
+=        |  加法并赋值 |   [AddAssign][AddAssign]
-=        |  减法并赋值 |   [SubAssign][SubAssign]
*=        |  乘法并赋值 |   [MulAssign][MulAssign]
/=        |  除法并赋值 |   [DivAssign][DivAssign]
%=        |  取余并赋值 |   [RemAssign][RemAssign]

[Add]: https://doc.rust-lang.org/core/ops/trait.Add.html
[Sub]: https://doc.rust-lang.org/core/ops/trait.Sub.html
[Mul]: https://doc.rust-lang.org/core/ops/trait.Mul.html
[Div]: https://doc.rust-lang.org/core/ops/trait.Div.html
[Rem]: https://doc.rust-lang.org/core/ops/trait.Rem.html

[AddAssign]: https://doc.rust-lang.org/core/ops/trait.AddAssign.html
[SubAssign]: https://doc.rust-lang.org/core/ops/trait.SubAssign.html
[MulAssign]: https://doc.rust-lang.org/core/ops/trait.MulAssign.html
[DivAssign]: https://doc.rust-lang.org/core/ops/trait.DivAssign.html
[RemAssign]: https://doc.rust-lang.org/core/ops/trait.RemAssign.html


单目运算符 |  作用     | 重载（trait）
----------|:---------:|:---------:
\-        |  取反      |   [Neg][Neg]
!         |  逻辑非    |   [Not][Not]

[Neg]: https://doc.rust-lang.org/core/ops/trait.Neg.html
[Not]: https://doc.rust-lang.org/core/ops/trait.Not.html


位运算符  |  作用     | 重载（trait）
---------|:---------:|:---------:
<<       |  左移       |   [Shl][Shl]
\>\>     |  右移       |   [Shr][Shr]
&#124;   |  按位或      |   [BitOr][BitOr]
^        |  按位异或    |   [BitXor][BitXor]
&        |  按位与      |   [BitAnd][BitAnd]
<<=      |  左移并赋值   |  [ShlAssign][ShlAssign]
\>\>=    |  右移并赋值   |  [ShrAssign][ShrAssign]
&#124;=  |  按位或并赋值   |  [BitOrAssign][BitOrAssign]
^=       |  按位异或并赋值 |  [BitXorAssign][BitXor]
&=       |  按位与并赋值   | [BitAndAssign][BitAndAssign]

[Shl]: https://doc.rust-lang.org/core/ops/trait.Shl.html
[Shr]: https://doc.rust-lang.org/core/ops/trait.Shr.html
[BitOr]: https://doc.rust-lang.org/core/ops/trait.BitOr.html
[BitXor]: https://doc.rust-lang.org/core/ops/trait.BitXor.html
[BitAnd]: https://doc.rust-lang.org/core/ops/trait.BitAnd.html

[ShlAssign]: https://doc.rust-lang.org/core/ops/trait.ShlAssign.html
[ShrAssign]: https://doc.rust-lang.org/core/ops/trait.ShrAssign.html
[BitOrAssign]: https://doc.rust-lang.org/core/ops/trait.BitOrAssign.html
[BitXorAssign]: https://doc.rust-lang.org/core/ops/trait.BitXorAssign.html
[BitAndAssign]: https://doc.rust-lang.org/core/ops/trait.BitAndAssign.html


不支持自增`++`、自减`--`

```rust
let mut value = 3;

value++; // error
value--; // error
```





## 控制流

### `if` 表达式


```rust
fn main() {
    let number = 6;

    if number % 4 == 0 {
        println!("number is divisible by 4");
    } else if number % 3 == 0 {
        println!("number is divisible by 3");
    } else if number % 2 == 0 {
        println!("number is divisible by 2");
    } else {
        println!("number is not divisible by 4, 3, or 2");
    }
}
```

注：条件的值必须是`bool`。

#### 在`let`语句中使用`if`

```rust
fn main() {
    let condition = true;
    let number = if condition {
        5
    } else {
        6
    };

    println!("The value of number is: {}", number);
}
```

注： `if` 和 `else` 分支的值类型必须是相同的。

### 循环

`break` 语句：终止整个循环

`continue` 语句：结束本次循环

#### `for` 

反转输出 `1` 到 `3`

```rust
fn main() {
    for number in (1..4).rev() {
        println!("{}!", number);
    }
    println!("LIFTOFF!!!");
}
```

遍历一个元素集合

```rust
fn main() {
    let a = [10, 20, 30, 40, 50];

    for element in a.iter() {
        println!("the value is: {}", element);
    }
}
```

#### `while` 

当条件为真，执行循环。当条件不再为真，停止循环。

```rust
fn main() {
    let mut number = 3;

    while number != 0  {
        println!("{}!", number);

        number = number - 1;
    }

    println!("LIFTOFF!!!");
}
``` 

#### `loop` 

`loop` 关键字告诉 Rust 一遍又一遍的执行一段代码直到你明确要求停止 `break`。

```rust
fn main() {
    let mut count = 0;
    loop{
        if count >= 10 {
            break;
        } else {
            count = count + 1;
            println!("Count: {}", count);
        }
    }
}
```


## 注释

### 行注释（line comments）

```rust
// Line comments are anything after ‘//’ and extend to the end of the line.

let x = 5; // this is also a line comment.
```


### 文档注释（doc comments）

文档注释使用 `///` 而不是 `//`，并且内建[Markdown](http://en.wikipedia.org/wiki/Markdown)标记支持：

```rust
/// Adds one to the number given.
///
/// # Examples
///
/// 
/// let five = 5;
///
/// assert_eq!(6, add_one(5));
/// # fn add_one(x: i32) -> i32 {
/// #     x + 1
/// # }
/// 
fn add_one(x: i32) -> i32 {
    x + 1
}
```

#### 文档注释-Toggle样式


使用 `//!` 的注释块，在HTML文档中可以切换显示或隐藏。



### 生成HTML文档

可以使用 `rustdoc`工具来将文档注释生成为HTML文档，也可以将代码示例作为测试运行！

Cargo生成HTML文档并打开:

```
$ cargo doc --open
```