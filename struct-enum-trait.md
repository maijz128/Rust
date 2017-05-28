


## 结构体（struct） ≈ 类

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


##### 方法

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

##### 关联函数 ≈ 类方法

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

##### 输出结构体（struct）

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




## 枚举（enum）

定义：

```rust
enum IpAddrKind {
    V4,
    V6,
}
```

使用：

```rust
let six = IpAddrKind::V6;

fn route(ip_type: IpAddrKind) { 

}

route(IpAddrKind::V6);
```

##### 类型嵌入：

```rust
enum Message {
    Quit,
    Move { x: i32, y: i32 },
    Write(String),
    ChangeColor(i32, i32, i32),
}
```


这个枚举有四个含有不同类型的成员：

- `Quit`没有关联任何数据。
- `Move`包含一个匿名结构体。
- `Write`包含单独一个`String`。
- `ChangeColor`包含三个`i32`。


##### 方法

可以使用`impl`来为结构体定义方法那样，也可以在枚举上定义方法。

```rust
impl Message {
    fn call(&self) {
        // method body would be defined here
    }
}

let m = Message::Write(String::from("hello"));
m.call();
```

##### 泛型

标准库中的`Option<T>`

```rust
enum Option<T> {
    Some(T),
    None,
}
```


## trait ≈ 接口






