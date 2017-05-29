
## 函数

函数`add_nub`有一个名字是`nub`类型为`i32`的参数，和一个类型为`i32`的返回值，返回值是`nub + 1`表达式的结果

```rust
fn add_nub(nub: i32) -> i32{
    // do some thing

    nub + 1
}
```

### 提早返回`return`

```rust
fn foo(x: i32) -> i32 {
    return x;

    // we never run this code!
    x + 1
}
```

### 函数指针

```rust
fn plus_one(i: i32) -> i32 {
    i + 1
}

// without type inference
let f: fn(i32) -> i32 = plus_one;

// with type inference
let f = plus_one;

let six = f(5);
```



