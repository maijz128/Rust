
## 表达式（Expression）

语句：执行一些操作但不返回值。
表达式：计算并产生返回一个值， 在赋值操作中充当[右值（r-values）](http://en.wikipedia.org/wiki/Value_%28computer_science%29#lrvalue)。

```rust
// 语句
let y = 6;   

// 表达式;
y;
y + 1;
5;
```


代码块 `{}` 也是表达式：

```rust
let y = {
    let x = 3;
    x + 1
};

println!("The value of y is: {}", y);   // value is 4
```

### 函数与代码块的返回值

在 Rust 中，函数的返回值等同于函数体最后一个**实际执行**表达式的值。（代码块也一样）


```rust
fn five() -> i32 {
    5   // == return 5;
}

fn main() {
    let x = five();

    println!("The value of x is: {}", x); value is 5
}
```

但如果在最后一条表达式结尾处有分号，返回值将变为 `()` unit type。
以下的代码会产生错误（类型不匹配）：

```rust
fn main() {
    let x = plus_one(5);

    println!("The value of x is: {}", x);
}

fn plus_one(x: i32) -> i32 {
    x + 1;  
}
```

