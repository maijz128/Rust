
## crate

crate == 包，可以通过 [crates.io](http://crates.io) 分发给他人使用。

crate 可以编译成二进制可执行文件（binary）或库文件（library）。


### 示例

让我们创建一个库，然后看看如何把它链接到另一个 crate。

Filename: rary.rs
```rust
pub fn public_function() {
    println!("called rary's `public_function()`");
}

fn private_function() {
    println!("called rary's `private_function()`");
}

pub fn indirect_access() {
    print!("called rary's `indirect_access()`, that\n> ");

    private_function();
}
```

```
$ rustc rary.rs --crate-type=lib
$ ls lib*
library.rlib
```

链接一个 crate 到这个新库，必须使用 `extern crate` 声明。这不仅会链接库，还会导入与库名相同的模块里面的所有项。适用于模块的可见性规则也适用于库。

Filename: executable.rs
```rust
// 链接到 `library`（库），导入 `rary` 模块里面的项
extern crate rary;

fn main() {
    rary::public_function();

    // 报错！ `private_function` 是私有的
    //rary::private_function();

    rary::indirect_access();
}
```

```
# library.rlib 是已编译好的库的路径，假设在这里它在同一目录下：
$ rustc executable.rs --extern rary=library.rlib && ./executable
called rary's `public_function()`
called rary's `indirect_access()`, that
> called rary's `private_function()`
```


### Cargo 管理使用 crate

Cargo 创建的项目，可以通过编辑项目根目录下的 *Cargo.toml*，添加管理依赖 crate。
当构建项目时会自动从 *registry* （[crates.io](http://crates.io)）下载代码（最新兼容版本）并编译。


#### 例子：生成随机数

用 Cargo 创建一个项目，在 *Cargo.toml* 文件的 `[dependencies]` 标题之下，添加 `rand` 依赖：

Filename: Cargo.toml
```toml
[dependencies]
rand = "0.3.14"
```

使用 `rand` 生成一个随机数：

Filename: src/main.rs
```rust
// 使用外部依赖
extern crate rand;

use rand::Rng;

fn main() {
    let number = rand::thread_rng().gen_range(1, 101);

    println!("The number is: {}", number);
}
```


#### 更新 crate

在添加 crate 时需要指定版本号，这样 Cargo 才可以管理 crate 的下载和更新。
参考：[语义化版本（Semantic Versioning）](http://semver.org/)

默认情况下 Cargo 是不会自动更新 crate 的，只能运行命令显式升级。
```
$ cargo update
```

不过，Cargo 只会更新到最大修订号版本。例如： 如果 `rand` 发布了两个新版本，`0.3.22` 和 `0.4.0`，在运行 `cargo update` 时版本会更新到 `0.3.22`。


