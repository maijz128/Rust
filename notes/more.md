


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

### 普通注释

普通注释的内容将被编译器忽略掉

```
 // 单行注释，注释内容直到行尾。
 /* 块注释， 注释内容一直到结束分隔符。 */
```


### 文档注释

文档注释的内容将被解析成 HTML 帮助文档，内建[Markdown](http://en.wikipedia.org/wiki/Markdown)标记支持。

文档注释有两种风格：外部和内部。

内部文档注释用于（crate，模块或者函数）。

注：不能同时使用 *内部行文档注释* 和 *内部块文档注释* 。

##### 外部文档注释

```rust
/// 外部行文档注释
/// 外部行文档注释
/// 外部行文档注释

/**
    外部块文档注释
    外部块文档注释
    外部块文档注释
 */
```

##### 内部文档注释

```rust
//! 内部行文档注释
//! 内部行文档注释
//! 内部行文档注释

/*!
    内部块文档注释
    内部块文档注释
    内部块文档注释
 */
```







### 生成HTML文档

可以使用 `rustdoc`工具来将文档注释生成为HTML文档，也可以将代码示例作为测试运行！

Cargo生成HTML文档并打开:

```
$ cargo doc --open
```