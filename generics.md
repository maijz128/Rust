

# 泛型（Generics）

### 泛型参数

函数`some_function`有一个参数`t`的类型为泛型`T`, 返回值的类型也是泛型`T`

```rust
fn some_function<T>(t: T) -> T {
    // do some thing
}
```

### 多泛型参数

```rust
fn some_function<T, U>(t: T, u: U) -> i32 {
    // do some thing
}
```

### 泛型限定

泛型`T`的类型实现了`Summarizable`

```rust
pub fn notify<T: Summarizable>(item: T) {
     // do some thing
}
```

### 多泛型限定

泛型`T`是任何实现了`Summarizable`和`CloneObj`的类型

```rust
pub fn notify<T: Summarizable + CloneObj>(item: T) {
    // do some thing
}
```

### where从句写法

```rust
fn some_function<T: Display + Clone, U: Clone + Debug>(t: T, u: U) -> i32 {
    // do some thing
}
```

和下面的写法意思一样

```rust
fn some_function<T, U>(t: T, u: U) -> i32
    where T: Display + Clone, U: Clone + Debug{
    // do some thing
}
```

