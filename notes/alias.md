
## 别名


`type` 语句可以给一个已存在类型起一个新的名字。新名字的命名风格必须是 `CamelCase`（[驼峰方式](http://en.wikipedia.org/wiki/Camel_case)），否则 编译器会产生一个警告。

```rust
// `NanoSecond` 是 `u64` 的新名字。
type NanoSecond = u64;
type Inch = u64;
type u64_t = u64;

// `NanoSecond` = `Inch` = `u64_t` = `u64`.
let nanoseconds: NanoSecond = 5 as u64_t;
let inches: Inch = 2 as u64_t;
```