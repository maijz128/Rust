
# 交叉编译（Cross Compiler）

第一层平台：


Target | std | rustc | cargo | notes
-------|-----|-------|-------|------
i686-apple-darwin   | ✓ |    | ✓ |    | ✓ |  32-bit OSX (10.7+, Lion+)
i686-pc-windows-gnu  | ✓ |   | ✓ |   | ✓ |  32-bit MinGW (Windows 7+)
i686-pc-windows-msvc  | ✓ |   | ✓ |   | ✓ |  32-bit MSVC (Windows 7+)
i686-unknown-linux-gnu  | ✓ |   | ✓ |   | ✓ |  32-bit Linux (2.6.18+)
x86_64-apple-darwin  | ✓ |   | ✓ |   | ✓ |  64-bit OSX (10.7+, Lion+)
x86_64-pc-windows-gnu  | ✓ |   | ✓ |   | ✓ |  64-bit MinGW (Windows 7+)
x86_64-pc-windows-msvc  | ✓ |   | ✓ |   | ✓ |  64-bit MSVC (Windows 7+)
x86_64-unknown-linux-gnu  | ✓ |   | ✓ |   | ✓ |  64-bit Linux (2.6.18+)



[查看更多支持的平台](https://forge.rust-lang.org/platform-support.html)



### 添加目标平台-工具链（toolchain） ＝　标准库

例：添加	32-bit Linux (2.6.18+)

```
$ rustup target add i686-unknown-linux-gnu
```

### 添加目标平台-编译器（compiler）


### 添加目标平台-链接器（linker ）

```toml
[target.armv7-unknown-linux-gnueabihf]
linker = "arm-linux-gnueabihf-gcc-4.7"
```


### 查看目标平台

```
$ rustup target list
```




### 交叉编译工具链


#### linux



### 编译到目标平台

```
$ cargo build --target=i686-unknown-linux-gnu
```