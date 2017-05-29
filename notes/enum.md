

## 枚举（enum）

定义：

```rust
// 拥有隐式辨别值（implicit discriminator）的 enum（从0开始计数）
enum IpAddrKind {
    V4,
    V6,
}

// 拥有显式辨别值（explicit discriminator）的 enum
enum Color {
    Red = 0xff0000,
    Green = 0x00ff00,
    Blue = 0x0000ff,
}
```

使用：

```rust
let six = IpAddrKind::V6;

fn route(ip_type: IpAddrKind) { 

}

route(six);
route(IpAddrKind::V6);

// `enum` 可以转成整形。
println!("color is {}", Color::Red as i32);
```

### 类型嵌入：

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


### 方法

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

### 泛型

标准库中的`Option<T>`

```rust
enum Option<T> {
    Some(T),
    None,
}
```
