
## 模块

### `mod` 关键字

在Rust中的模块相当于其他语言的命名空间，使用 `mod` 关键字来定义。

模块内可以定义函数、结构体、枚举、trait、子模块。

```rust
mod mytool{
    pub fn open(){
        println!("mytool is open.");
    }

    pub mod toolone{
        pub fn open(){
            println!("mytool::toolone is open.");
        }
    }
}

fn main(){
    mytool::open();
    mytool::toolone::open();
}
```

### 可见性

在Rust中每一项（函数、结构体、模块等）的可见性默认都是私有（private）的，
需要设置为公开（public）可见性时，要加上 `pub` 关键字。



### `use` 声明

use 声明可以将一个完整的路径绑定到一个新的名字，从而更容易访问。

```rust
// 将 `deeply::nested::function` 路径绑定到 `other_function`。
use deeply::nested::function as other_function;

fn function() {
    println!("called `function()`");
}

mod deeply {
    pub mod nested {
        pub fn function() {
            println!("called `deeply::nested::function()`")
        }
    }
}

fn main() {
    // 更容易访问 `deeply::nested::funcion`
    other_function();

    println!("Entering block");
    {
        // 这和 `use deeply::nested::function as function` 等价。
        // 此 `function()` 将覆盖掉的外部同名函数。
        use deeply::nested::function;
        function();

        // `use` 绑定拥有局部作用域。在这个例子中，`function()`
        // 的覆盖只限定在这个代码块中。
        println!("Leaving block");
    }

    function();
}
```

### `super` 和 `self`

在路径上使用 `super` （父级）和 `self`（自身）关键字，可以在访问项时消除歧义和防止不必要的路径的硬编码。


```rust
fn function() {
    println!("called `function()`");
}

mod cool {
    pub fn function() {
        println!("called `cool::function()`");
    }
}

mod my {
    fn function() {
        println!("called `my::function()`");
    }

    mod cool {
        pub fn function() {
            println!("called `my::cool::function()`");
        }
    }

    pub fn indirect_call() {
        // 让我们从这个作用域中访问所有名为 `function` 的函数！
        print!("called `my::indirect_call()`, that\n> ");

        // `self` 关键字表示当前的模块作用域——在这个例子是 `my`。
        // 调用 `self::function()` 和直接访问 `function()` 两者都得到相同的结果，
        // 因为他们表示相同的函数。
        self::function();
        function();

        // 我们也可以使用 `self` 来访问 `my` 内部的另一个模块：
        self::cool::function();

        // `super` 关键字表示父级作用域（在 `my` 模块外面）。
        super::function();

        // 这将在 *crate* 作用域内绑定 `cool::function` 。
        // 在这个例子中，crate 作用域是最外面的作用域。
        {
            use cool::function as root_function;
            root_function();
        }
    }
}

fn main() {
    my::indirect_call();
}
```


### 文件分层

模块代码可以分配到文件/目录的层次结构中：

```rust
$ tree .
.
|-- my
|   |-- inaccessible.rs
|   |-- mod.rs
|   `-- nested.rs
`-- main.rs
```

```rust
// main.rs
// 此声明将会查找名为 `my.rs` 或 `my/mod.rs` 的文件，并将该文件的内容插入到
// 此作用域名为 `my` 的模块里面。
mod my;

fn function() {
    println!("called `function()`");
}

fn main() {
    my::function();

    function();

    my::indirect_access();

    my::nested::function();
}
```

```rust
// my/mod.rs
// 类似地，`mod inaccessible` 和 `mod nested` 将找到 `nested.rs` 和
// `inaccessible.rs` 文件，并在它们各自的模块中插入它们的内容。
mod inaccessible;
pub mod nested;

pub fn function() {
    println!("called `my::function()`");
}

fn private_function() {
    println!("called `my::private_function()`");
}

pub fn indirect_access() {
    print!("called `my::indirect_access()`, that\n> ");

    private_function();
}
```

```rust
// my/nested.rs
pub fn function() {
    println!("called `my::nested::function()`");
}

#[allow(dead_code)]
fn private_function() {
    println!("called `my::nested::private_function()`");
}
```

```rust
// my/inaccessible.rs
#[allow(dead_code)]
pub fn public_function() {
    println!("called `my::inaccessible::public_function()`");
}
```