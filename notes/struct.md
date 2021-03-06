

## 结构体（struct）

Rust中的结构体相当于其他语言的类（Class）

定义：

```rust

// 单元结构体
struct Nil;

// 元组结构体
struct Pair(i32, f32);

// 带有字段的结构体
struct  User {
    username: String,
    email: String,
}
```

实例化：

```rust
// 实例化一个单元结构体
let _nil = Nil;

// 实例化一个元组结构体
let pair = Pair(1, 0.1);

let user1 = User {
    email: String::from("someone@example.com"),
    username: String::from("someusername123"),
};
```

访问字段：

```rust
println!("user name: {}", user1.username);

// 访问元组结构体的字段
println!("pair contains {:?} and {:?}", pair.0, pair.1);
```

解构：

```rust
 // 解构带有字段的结构体并使用 `let` 来绑定
let User { email: u_email, username: u_name} = user1;

println!("name: {:?}  email: {:?}", u_name, u_email);

 // 解构一个元组结构体
let Pair(integer, decimal) = pair;

println!("pair contains {:?} and {:?}", integer, decimal);
```


### 方法

定义和使用：

```rust
struct Rectangle {
    length: u32,
    width: u32,
}

impl Rectangle {
    // `&self` 为 `self: &Self` 的语法糖
    fn area(&self) -> u32 {
        self.length * self.width
    }

    // 这个方法要求调用者对象是可变的
    // `&mut self` 为 `self: &mut Self` 的语法糖
    fn zoom(&mut self, size: u32) {
        self.length *= size;
        self.width *= size;
    }
}

fn main() {
    let mut rect1 = Rectangle { length: 50, width: 30 };
    
    rect1.zoom(2);
    
    println!(
        "The area of the rectangle is {} square pixels.",
        rect1.area()
    );
}
```

### 


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

### 实现析构函数

`destroy` 方法会拿到 `Rectangle` 对象的[所有权](core/ownership.md)，并且会在离开作用域后释放它。

```rust
impl Rectangle {
    // 这个方法“消费”调用者对象的资源
    // `self` 为 `self: Self` 的语法糖
    fn destroy(self) {
        // 解构 `self`
        let Rectangle{length, width} = self;

        println!("Destroying Rectangle({}, {})", length, width);

        // `length` 和 `width` 离开作用域后释放
    }
}
```

使用：

```rust
rect1.destroy();

// rect1析构后再使用将会触发error
println!(
    "The area of the rectangle is {} square pixels.",
    rect1.area()
);
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

