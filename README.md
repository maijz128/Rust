
<p align="center"><a href="http://www.rust-lang.org" target="_blank"><img src="http://www.rust-lang.org/logos/rust-logo-blk.svg"></a></p>

<center><h3><a href="http://www.rust-lang.org">Rust</a> 是一种系统编程语言。 它有着惊人的运行速度，能够防止段错误，并保证线程安全。</h3>
</center>




# Rust 学习笔记

### Rust Version: 1.17.0 (2017-04-27)



----------



## 变量

##### 绑定

    let nub = 5;

##### 类型注解

    let nub: i32 = 5;

##### 可变性

变量默认不可变，可变需要设置为`mut`

    let mut nub: i32 = 5;
    nub = 11;


##### 覆盖（Shadowing）

定义一个与之前变量名称相同的新变量，而新变量会覆盖之前的变量。
可以用相同变量名称来覆盖它自己以及重复使用let关键字来多次覆盖。

    //  js
    var str ='123';
    var int = 123;
    str = int;      //  ok

    //  c#
    string  _str = "123";
    int     _int =  123;
    _str =  _int;   //  error

    //  rust
    let _str = "123";
    let _int =  123;
    let _str = _int;    //  ok



## 函数

函数`add_nub`有一个名字是`nub`类型为`i32`的参数，和一个类型为`i32`的返回值，返回值是`nub + 1`表达式的结果

    fn add_nub(nub: i32) -> i32{
        // do some thing

        nub + 1
    }

##### 提早返回`return`

    fn foo(x: i32) -> i32 {
        return x;
    
        // we never run this code!
        x + 1
    }

##### 函数指针

    fn plus_one(i: i32) -> i32 {
        i + 1
    }
    
    // without type inference
    let f: fn(i32) -> i32 = plus_one;
    
    // with type inference
    let f = plus_one;
    
    let six = f(5);



## 原生类型

##### bool（布尔）

    let t = true;
    
    let f: bool = false;

##### char

`char`类型代表一个单独的 Unicode 字符的值。在Rust中`char`占4个字节

    let x = 'x';
    let two_hearts = '💕';

##### 数字类型

默认类型：

    let x = 42; // x has type i32

    let y = 1.0; // y has type f64


数字类型列表：

|       *  | 符号  |  位   |类型    |
|----------|:-----:|:------:|:----:|
|[i8][i8]       | 有    |  8       | 整数
|[i16][i16]     | 有    |  16      | 整数
|[i32][i32]     | 有    |  32      | 整数
|[i64][i64]     | 有    |  64      | 整数
|[u8][u8]       | 无    |  8       | 整数
|[u16][u16]     | 无    |  16      | 整数
|[u32][u32]     | 无    |  32      | 整数
|[u64][u64]     | 无    |  64      | 整数
|[isize][isize] | 有    | 依赖底层  | 整数
|[usize][usize] | 无    | 依赖底层  | 整数
|[f32][f32]     | 有    |  32      | 单精度浮点数
|[f64][f64]     | 有    |  64      | 双精度浮点数

[i8]: http://doc.rust-lang.org/nightly/std/primitive.i8.html
[i16]: http://doc.rust-lang.org/nightly/std/primitive.i16.html
[i32]: http://doc.rust-lang.org/nightly/std/primitive.i32.html
[i64]: http://doc.rust-lang.org/nightly/std/primitive.i64.html
[u8]: http://doc.rust-lang.org/nightly/std/primitive.u8.html
[u16]: http://doc.rust-lang.org/nightly/std/primitive.u16.html
[u32]: http://doc.rust-lang.org/nightly/std/primitive.u32.html
[u64]: http://doc.rust-lang.org/nightly/std/primitive.u64.html
[isize]: http://doc.rust-lang.org/nightly/std/primitive.isize.html
[usize]: http://doc.rust-lang.org/nightly/std/primitive.usize.html
[f32]: http://doc.rust-lang.org/nightly/std/primitive.f32.html
[f64]: http://doc.rust-lang.org/nightly/std/primitive.f64.html


##### 数组

数组默认是不可变的。 
类型是`[T; N]`。

    let a = [1, 2, 3]; // a: [i32; 3]
    let mut m = [1, 2, 3]; // m: [i32; 3]

初始化简写：`a`的每个元素都被初始化为`1`

    let a = [1, 20] // a: [i32; 20]

长度：`a.len()`

访问*下标*：`a[0]`

切片


##### 元组（Tuples）

元组（tuples）是固定大小的有序列表。

    let x = (1, "hello");

访问索引： 

    let x0 = x.0; //  1
    let x1 = x.1; //  hello


##### `()`

##### `_`


## struct（结构体≈类）

例：

```
struct  User {
    username: String,
    email: String,
    sign_in_count: u64,
    active: bool,
}
```

使用：

```
let user1 = User {
    email: String::from("someone@example.com"),
    username: String::from("someusername123"),
    active: true,
    sign_in_count: 1,
};
```

获取成员：

```
user1.username
```


##### 方法

定义和使用：

```
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

##### 关联函数（≈类方法）

```
impl Rectangle {
    fn square(size: u32) -> Rectangle {
        Rectangle { length: size, width: size }
    }
}
```

使用：

```
let sq = Rectangle::square(3);
```



## 枚举（enum）

定义：

```
enum IpAddrKind {
    V4,
    V6,
}
```

使用：

```
let six = IpAddrKind::V6;

fn route(ip_type: IpAddrKind) { 

}

route(IpAddrKind::V6);
```

##### 类型嵌入：

```
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

```
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

```
enum Option<T> {
    Some(T),
    None,
}
```

## trait(≈接口)



## 泛型

##### 泛型参数

函数`some_function`有一个参数`t`的类型为泛型`T`, 返回值的类型也是泛型`T`

    fn some_function<T>(t: T) -> T {
        // do some thing
    }

##### 多泛型参数

    fn some_function<T, U>(t: T, u: U) -> i32 {
        // do some thing
    }


##### 泛型限定

泛型`T`的类型实现了`Summarizable`

    pub fn notify<T: Summarizable>(item: T) {
         // do some thing
    }


##### 多泛型限定

泛型`T`是任何实现了`Summarizable`和`CloneObj`的类型

    pub fn notify<T: Summarizable + CloneObj>(item: T) {
        // do some thing
    }

##### where从句写法

    fn some_function<T: Display + Clone, U: Clone + Debug>(t: T, u: U) -> i32 {
        // do some thing
    }
和下面的写法意思一样

    fn some_function<T, U>(t: T, u: U) -> i32
        where T: Display + Clone, U: Clone + Debug{
        // do some thing
    }




## Test（测试）

##### 运行测试

默认并行的运行所有测试

    cargo test

单线程运行所有测试，避免互相干涉

    cargo test -- --test-threads=1

显示测试输出`println!`

    cargo test -- --nocapture

通过名称来运行测试

- 运行单个测试或模块
    - `cargo test 测试名字`
- 运行多个测试或模块
    - `cargo test add_` // 运行所有名字带有`add_`的测试

忽略测试，增加`#[ignore]`行

    #[test]
    #[ignore]
    fn expensive_test() {
        // code that takes an hour to run
    }

运行被忽略的测试

    cargo test -- --ignored

##### Test范例

    #[cfg(test)]
    mod tests {
        #[test]
        fn it_works() {
        }
    }


##### assert宏

`assert!` : 条件是否为`true`

    let is_true:bool = 1 > 0;    
    assert!(is_true);

`assert_eq!` : 比较两个参数是否相等

    let a:i32 = 23;
    let b:i32 = 23;
    assert_eq!(a, b);

`assert_ne!` : 比较两个参数是否不相等

    let a:i32 = 32;
    let b:i32 = 23;
    assert_ne!(a, b);

##### 自定义错误信息

`assert!` : 条件是否为`true`

    let is_true:bool = 1 < 0;    
    assert!(is_true, "is_true : {}", is_true);

`assert_eq!` : 比较两个参数是否相等

    let a:i32 = 32;
    let b:i32 = 23;
    assert_eq!(a, b, "a: {}, b: {}", a, b);

`assert_ne!` : 比较两个参数是否不相等

    let a:i32 = 23;
    let b:i32 = 23;
    assert_ne!(a, b, "a: {}, b: {}", a, b);

##### 使用`should_panic`检查 panic

检查代码是否按预期一样触发`panic!`

    #[cfg(test)]
    mod tests {
    
        #[test]
        #[should_panic]
        fn fun1() {
            // do some thing
        }
    }

添加`expected`参数，确保错误信息中包含其提供的文本

    struct Guess {
        value: u32,
    }
    
    impl Guess {
        pub fn new(value: u32) -> Guess {
            if value < 1 {
                panic!("Guess value must be greater than or equal to 1, got {}.",
                       value);
            } else if value > 100 {
                panic!("Guess value must be less than or equal to 100, got {}.",
                       value);
            }
    
            Guess {
                value: value,
            }
        }
    }
    
    #[cfg(test)]
    mod tests {
        use super::*;
    
        #[test]
        #[should_panic(expected = "Guess value must be less than or equal to 100")]
        fn greater_than_100() {
            Guess::new(200);
        }
    }


##### 集成测试

为了编写集成测试，需要在项目根目录创建一个 tests 目录，与 src 同级。Cargo 知道如何去寻找这个目录中的集成测试文件。接着可以随意在这个文件夹中创建任意多的测试文件，Cargo 会将每一个文件当作单独的 crate 来编译。

例：Filename: tests/integration_test.rs

    extern crate adder; // 导入被测试的库
    
    #[test]
    fn it_adds_two() {
        assert_eq!(4, adder::add_two(2));
    }


运行指定文件名的集成测试

     cargo test --test integration_test


集成测试中的子模块

在`tests`目录中的创建的模块不会被作为单独的 crate 编译或作为一部分出现在测试输出中。










## 格式化输出（Formatted Print）


##### println!


```
let a = 1;
let b = 2;
println!("a: {}, b: {}", a, b);

```

字符串内的`{}`为输出占位符


##### 输出结构体（struct）

```
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




## prelude（预加载）

##### [`core::result`](https://doc.rust-lang.org/nightly/core/result/)

```
enum Result<T, E> {
   Ok(T),
   Err(E),
}
```

##### [`core::option`](https://doc.rust-lang.org/nightly/core/option/)

```
enum Option<T> {
    None,
    Some(T),
}
```


##### trait

- `Debug`
- `std::cmp::PartialOrd` （实现了可以用比较符（<、>、 ==、!=）来比较对象）
- `PartialEq`
- `Copy`
- `Clone`
