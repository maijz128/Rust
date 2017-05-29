

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
