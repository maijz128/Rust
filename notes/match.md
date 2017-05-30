
# 模式匹配

## `match`

Rust 通过 `match` 关键字来提供模式匹配，用法和 C 语言的的 `switch` 类似。

在匹配复合数据类型（元组、枚举、结构体）时，需要解构它。

注：Rust 中的匹配是穷尽的（*exhaustive）：必须穷举到最后的可能性来使代码有效。


例子：硬币（美国）分类器

```rust
#[derive(Debug)] // So we can inspect the state in a minute
enum UsState {
    Alabama,
    Alaska,
    // ... etc
}

enum Coin {
    Penny,
    Nickel,
    Dime,
    Quarter(UsState),
}

fn value_in_cents(coin: Coin) -> i32 {
    match coin {
        Coin::Penny => {
            println!("Lucky penny!");
            1
        },
        Coin::Nickel => 5,
        Coin::Dime => 10,
        Coin::Quarter(state) => {
            println!("State quarter from {:?}!", state);
            25
        },
    }
}
```

### 匹配 `Option<T>` ：

```rust
fn plus_one(x: Option<i32>) -> Option<i32> {
    match x {
        None => None,
        Some(i) => Some(i + 1),
    }
}

let five = Some(5);
let six = plus_one(five);
let none = plus_one(None);
```


### `_` 通配符

```rust
let some_u8_value = 0u8;
match some_u8_value {
    1 => println!("one"),
    3 => println!("three"),
    5 => println!("five"),
    7 => println!("seven"),
    _ => (),
}
```

`_` 模式会匹配所有的值。`()` 就是 unit 值，所以 `_` 的情况什么也不会发生。

### 多重模式（Multiple patterns）

```rust
let x = 1;

match x {
    1 | 2 => println!("one or two"),
    3 => println!("three"),
    _ => println!("anything"),
}
```

### 范围（Ranges）

```rust
let x = 1;

match x {
    1...5 => println!("one through five"),
    _ => println!("anything"),
}
```

### 绑定名字

使用 `@` 把值绑定到名字上：

```rust
let x = 1;

match x {
    e @ 1...5 => println!("got a range element {}", e),
    _ => println!("anything"),
}
```

### 匹配元组

```rust
fn main() {
    let point = (0, -2); // 试一试将不同的值赋给 `point`

    println!("point: {:?}", point);
    // match 可以解构一个元组
    match point {
        (0, y) => println!("`y` is `{:?}", y),
        (x, y) => println!("`x` is `{:?}` and `y` is `{:?}", x, y),
    }
}
```

### 匹配结构体

```rust
struct Point {
    x: i32,
    y: i32,
}

let origin = Point { x: 0, y: 0 };

match origin {
    Point { x, y } => println!("({},{})", x, y),
}

// 给字段不同的名字
match origin {
    Point { x: x1, y: y1 } => println!("({},{})", x1, y1),
}

// 只匹配部分字段 `y`，忽略其他的
match origin {
    Point { y, .. } => println!("y is {}", y),
}
```

### 守卫

可以加上 `match` 守卫（guard） 来过滤分支。

```rust
fn main() {
    let pair = (2, -2);
    // 试一试 ^ 将不同的值赋给 `pair`

    println!("Tell me about {:?}", pair);
    match pair {
        (x, y) if x == y => println!("These are twins"),
        // ^ `if condition`(if 条件)部分是一个守卫
        (x, y) if x + y == 0 => println!("Antimatter, kaboom!"),
        (x, _) if x % 2 == 1 => println!("The first one is odd"),
        _ => println!("No correlation..."),
    }
}
```


## `if let` 简单匹配

匹配一个 `Option<u8>` 值并只希望当值是 `3` 时执行代码：

```rust
let some_u8_value = Some(3u8);

match some_u8_value {
    Some(3) => println!("three"),
    _ => (),
}

// 跟上面代码功能一样
if let Some(3u8) = some_u8_value {
    println!("three");
}
``` 

计数所有不是 25 美分的硬币的同时也报告 25 美分硬币所属的州：

```rust
let mut count = 0;
match coin {
    Coin::Quarter(state) => println!("State quarter from {:?}!", state),
    _ => count += 1,
}

let mut count = 0;
if let Coin::Quarter(state) = coin {
    println!("State quarter from {:?}!", state);
} else {
    count += 1;
}
```

## while let 循环匹配

```rust
fn main() {
    // 将 `optional` 设为 `Option<i32>` 类型
    let mut optional = Some(0);

    // 分析：当 `let` 将 `optional` 解构成 `Some(i)` 时，就
    // 执行语句块（`{}`）。否则中断退出（`break`）。
    while let Some(i) = optional {
        if i > 9 {
            println!("Greater than 9, quit!");
            optional = None;
        } else {
            println!("`i` is `{:?}`. Try again.", i);
            optional = Some(i + 1);
        }
        // ^ 使用的缩进更少，并且不用显式地处理失败情况。
    }
    // ^ `if let` 有额外可选的 `else`/`else if` 分句，
    // 而 `while let` 没有。
}
```

参考：
[RFC | 官方](http://github.com/rust-lang/rfcs/pull/214)， 
[while let | 通过例子学Rust](http://rustwiki.org/rust-by-example/flow_control/while_let.html)