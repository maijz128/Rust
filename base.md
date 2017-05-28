
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

[i8]: http://doc.rust-lang.org/nightly/std/primitive.i8.html
[i16]: http://doc.rust-lang.org/nightly/std/primitive.i16.html
[i32]: http://doc.rust-lang.org/nightly/std/primitive.i32.html
[i64]: http://doc.rust-lang.org/nightly/std/primitive.i64.html
[u8]: http://doc.rust-lang.org/nightly/std/primitive.u8.html
[u16]: http://doc.rust-lang.org/nightly/std/primitive.u16.html
[u32]: http://doc.rust-lang.org/nightly/std/primitive.u32.html
[u64]: http://doc.rust-lang.org/nightly/std/primitive.u64.html
[isize]: http://doc.rust-lang.org/nightly/std/primitive.isize.html
[usize]: http://doc.rust-lang.org/nightly/std/primitive.usize.html
[f32]: http://doc.rust-lang.org/nightly/std/primitive.f32.html
[f64]: http://doc.rust-lang.org/nightly/std/primitive.f64.html



### 运算符

基本数学运算操作：加法、减法、乘法、除法以及余数。

```rust
fn main() {
    // addition
    let sum = 5 + 10;

    // subtraction
    let difference = 95.5 - 4.3;

    // multiplication
    let product = 4 * 30;

    // division
    let quotient = 56.7 / 32.2;

    // remainder
    let remainder = 43 % 5;
}
```

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

