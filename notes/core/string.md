

## 字符串

### `str`

Rust 的核心语言中事实上就只有一种字符串类型：`str`，字符串 slice，它通常以被借用的形式出现，`&str`。


### 字符串常量


```rust
const LANGUAGE: &'static str = "Rust";
```


### 字符串字面值

```rust
let language = "Rust";
// 转换到一个字符串
let s = language.to_string();
```


### 字符串类型

`String` 类型是由标准库提供的，它是可增长的、可变的、有所有权的、UTF-8 编码的字符串类型。

```rust
// type is String
let language = String::from("Rust");
```


### 遍历字符串

```rust
for c in "नमस्ते".chars() {
    println!("{}", c);
}
```

### 字符串 slice

使用 `[]` 和一个 range 来创建包含特定字节的字符串 slice：

```rust
let hello = "Здравствуйте";

let s = &hello[0..4];
```

这里，`s`是一个 `&str`，它包含字符串的头四个字节。 's' 的结果是“Зд”。
详情请了解计算机编码：[UTF-8](http://en.wikipedia.org/wiki/UTF-8)