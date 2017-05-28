# 测试（Testing）

##### 运行测试

默认并行的运行所有测试

```rust
car go test
```

单线程运行所有测试，避免互相干涉

```rust
cargo test -- --test-threads=1
```

显示测试输出`println!`

```rust
cargo test -- --nocapture
```

通过名称来运行测试

- 运行单个测试或模块
    - `cargo test 测试名字`
- 运行多个测试或模块
    - `cargo test add_` // 运行所有名字带有`add_`的测试

忽略测试，增加`#[ignore]`行

```rust
#[test]
#[ignore]
fn expensive_test() {
    // code that takes an hour to run
}
```

运行被忽略的测试

```rust
cargo test -- --ignored
```

##### Test范例

```rust
#[cfg(test)]
mod tests {
    #[test]
    fn it_works() {
    }
}
```

##### assert宏

`assert!` : 条件是否为`true`

```rust
let is_true:bool = 1 > 0;    
assert!(is_true);
```

`assert_eq!` : 比较两个参数是否相等

```rust
let a:i32 = 23;
let b:i32 = 23;
assert_eq!(a, b);
```

`assert_ne!` : 比较两个参数是否不相等

```rust
let a:i32 = 32;
let b:i32 = 23;
assert_ne!(a, b);
```

##### 自定义错误信息

`assert!` : 条件是否为`true`

```rust
let is_true:bool = 1 < 0;    
assert!(is_true, "is_true : {}", is_true);
```

`assert_eq!` : 比较两个参数是否相等

```rust
let a:i32 = 32;
let b:i32 = 23;
assert_eq!(a, b, "a: {}, b: {}", a, b);
```

`assert_ne!` : 比较两个参数是否不相等

```rust
let a:i32 = 23;
let b:i32 = 23;
assert_ne!(a, b, "a: {}, b: {}", a, b);
```

##### 使用`should_panic`检查 panic

检查代码是否按预期一样触发`panic!`

```rust
#[cfg(test)]
mod tests {

    #[test]
    #[should_panic]
    fn fun1() {
        // do some thing
    }
}
```

添加`expected`参数，确保错误信息中包含其提供的文本

```rust
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
```

##### 集成测试

为了编写集成测试，需要在项目根目录创建一个 tests 目录，与 src 同级。Cargo 知道如何去寻找这个目录中的集成测试文件。接着可以随意在这个文件夹中创建任意多的测试文件，Cargo 会将每一个文件当作单独的 crate 来编译。

例：Filename: tests/integration_test.rs

```rust
extern crate adder; // 导入被测试的库

#[test]
fn it_adds_two() {
    assert_eq!(4, adder::add_two(2));
}
```

运行指定文件名的集成测试

```rust
cargo test --test integration_test
```


集成测试中的子模块

在`tests`目录中的创建的模块不会被作为单独的 crate 编译或作为一部分出现在测试输出中。




