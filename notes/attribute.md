

## 属性(Attribute)

在 Rust 可以添加属性标注，有两种不同方式：

```rust
#[test]
# fn foo() {}

mod bar {
    #![bar]
}
```

区别：`#[foo]` 作用于下一个项，在这就是 `struct` 声明。`#![bar]` 作用于包含它的项，在这是 `mod` 声明。



### 常用属性

```rust
// 隐藏未使用代码的警告。
#![allow(dead_code)]

// 消除会溢出的类型转换的所有警告。
#![allow(overflowing_literals)]
```




### 参考

[属性 | 官方](http://doc.rust-lang.org/reference/attributes.html)