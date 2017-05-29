


## [运算符](base.md#运算符)重载


实现特定的 `trait` ，可以令一个类型使用特定的运算符。

例如， `+` 运算符可以通过 `Add` 特性（trait）重载：

```rust
use std::ops::Add;

#[derive(Debug)]
struct Point {
    x: i32,
    y: i32,
}

impl Add for Point {
    type Output = Point;

    fn add(self, other: Point) -> Point {
        Point { x: self.x + other.x, y: self.y + other.y }
    }
}

fn main() {
    let p1 = Point { x: 1, y: 0 };
    let p2 = Point { x: 2, y: 3 };

    let p3 = p1 + p2;

    println!("{:?}", p3);
}
```

有一系列可以这样被重载的运算符，并且所有与之相关的 `trait` 都在 [std::ops](http://doc.rust-lang.org/stable/std/ops/) 模块中。查看它的文档来获取完整的列表。





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