
# Cargo 

Cargo 是 Rust 的构建系统和包管理工具， 负责构建代码、下载代码依赖的库并编译这些库。

检查是否安装了 Cargo：

```
$ cargo --version
```

### 创建项目

创建可执行二进制项目

```
$ cargo new hello_cargo --bin
```

默认创建一个库项目

```
$ cargo new hello_cargo
```


项目

- 代码位于 src 目录
- 项目根目录包含一个 Cargo.toml 配置文件

### 构建并运行项目

#### 构建

```
$ cargo build
```

可执行文件在`./target/debug/`目录下。


#### 发布构建

```
cargo build --release
```

可执行文件在`./target/release/`目录下。


#### 一步构建并运行

```
$ cargo run
```


### Cargo.toml

项目的配置文件，使用[TOML](https://github.com/toml-lang/toml) (Tom's Obvious, Minimal Language) 格式。

Filename: Cargo.toml

```toml
[package]
name = "hello_cargo"
version = "0.1.0"
authors = ["Your Name <you@example.com>"]

[dependencies]
```

`[package]`部分为项目基本信息。

`[dependencies]`部分为项目依赖的`crates`（我们这么称呼 Rust 代码包）列表。


### 依赖管理

#### update

```
$ cargo update
```

