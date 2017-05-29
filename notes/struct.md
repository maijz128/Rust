

## 结构体（struct）

Rust中的结构体相当于其他语言的类（Class）

例：

```rust
struct  User {
    username: String,
    email: String,
    sign_in_count: u64,
    active: bool,
}
```

使用：

```rust
let user1 = User {
    email: String::from("someone@example.com"),
    username: String::from("someusername123"),
    active: true,
    sign_in_count: 1,
};
```

获取成员：

```rust
user1.username
```


### 方法

定义和使用：

```rust
struct Rectangle {
    length: u32,
    width: u32,
}

impl Rectangle {
    fn area(&self) -> u32 {
        self.length * self.width
    }
}

fn main() {
    let rect1 = Rectangle { length: 50, width: 30 };

    println!(
        "The area of the rectangle is {} square pixels.",
        rect1.area()
    );
}
```

### 关联函数 ≈ 类方法

```rust
impl Rectangle {
    fn square(size: u32) -> Rectangle {
        Rectangle { length: size, width: size }
    }
}
```

使用：

```rust
let sq = Rectangle::square(3);
```

### 输出结构体（struct）

```rust
#[derive(Debug)]
struct Rectangle {
    length: u32,
    width: u32,
}

fn main() {
    let rect1 = Rectangle { length: 50, width: 30 };

    println!("rect1 is {:?}", rect1);
}
```

为了输出结构体，我们需要在结构体定义之前加上`#[derive(Debug)]`注解。
在`{}`中加入`:?`指示符告诉`println!`我们想要使用叫做`Debug`的输出格式。Debug是一个 `trait`，它允许我们在调试代码时以一种对开发者有帮助的方式打印出结构体。

