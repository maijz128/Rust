

## slice（切片）

slice（中文有“切片”之意） 类型和数组类似，但 slice 类型的大小在编译期间是不确定的。相反， slice 是一个双字对象（two-word object），第一个字是一个指向数据的指针，第二个字是切片的 长度。slice 可以用来借用数组的一部分。slice 的类型标记为 `&[T]`。

```rust
let xs: [i32; 5] = [1, 2, 3, 4, 5];

let ys: [i32; 500] = [0; 500];

// 数组可以自动地借用成为 slice
println!("borrow the whole array as a slice");
analyze_slice(&xs);

// slice 可以指向数组的一部分
println!("borrow a section of the array as a slice");
analyze_slice(&ys[1 .. 4]);
```


[官方参考](https://doc.rust-lang.org/nightly/std/primitive.slice.html)