


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