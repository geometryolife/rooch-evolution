# 4.1. Rust代码风格与格式化

## 4.1.1 Rust官方的编码风格

遵循Rust官方编码风格有助于提高代码的可读性和可维护性。以下为一些关键的Rust编码风格规范：

1. 命名规范
    - 变量名和函数名：使用小写字母和下划线的蛇形命名法（snake_case），如 `variable_name` 和 `function_name`。
    - 类型名（包括结构体、枚举和类型别名）：使用大驼峰式命名法（UpperCamelCase），如 TypeName。
    - 常量名：使用大写字母和下划线的蛇形命名法（SCREAMING_SNAKE_CASE），如 `CONSTANT_NAME`。
    - 生命周期参数名：使用小写字母和撇号（tick），如 `'a`。

2. 代码布局
    - 缩进：使用 4 个空格而非制表符（tab）进行缩进。
    - 空行：在函数和模块之间使用空行进行分隔。
    - 括号和操作符：在括号和操作符两侧使用空格进行分隔，例如 `let x = a + b`;。
    - 逗号：在逗号后面使用空格，如 `fn example(a: i32, b: String) { ... }`。
    - 最大行宽：建议将每行代码的长度限制在 100 个字符以内。在某些情况下，可以适当增加到 120 个字符。

3. 注释：
    - 单行注释：使用 // 进行单行注释，注释文字与 // 之间留一个空格。
    - 多行注释：使用 `/* */` 进行多行注释。将注释内容与 /* 和 */ 之间分隔一个空格。

4. 文档注释：
    - 单行文档注释：使用 `///` 进行单行文档注释，注释文字与 `///` 之间留一个空格。
    - 多行文档注释：使用 `/** */` 进行多行文档注释。将注释内容与 `/**` 和 `*/` 之间分隔一个空格。

5. 模块和包导入：
    - 模块导入：将导入语句放在文件顶部，按字母顺序排序，使用空行分隔不同来源的导入。
    - 尽量使用绝对导入路径：在导入路径前添加 `crate::` 或 `self::`。

6. 错误处理：
    - 使用 `Result` 类型进行错误处理，避免使用 `panic!` 和 `unwrap()`。
    - 使用 `?` 运算符进行错误传递。

## 4.1.2 使用rustfmt进行自动格式化

1. 安装rustfmt

    安装rustfmt的命令如下：

    ```bash
    rustup component add rustfmt
    ```

    安装rustfmt命令后，可以执行Cargo fmt或者rustfmt 文件名进行格式化。

2. 配置rustfmt

    可以为项目添加一个rustfmt的配置，添加方式如下：
    - 在项目根目录下创建一个名为rustfmt.toml的文件，此文件将包含所有rustfmt的配置选项。
    - 下面为比较常见的rustfmt.toml配置：
        ```toml
        max_width = 100                   // 设置最大行宽为 100 个字符
        tab_spaces = 4                    // 设置缩进宽度为 4 个空格
        edition = "2018"                  // 设置 Rust 版本（根据实际项目版本进行调整）
        use_small_heuristics = "Max"      // 设置换行策略
        newline_style = "Auto"            // 设置换行符风格，根据平台自动选择
        ```
    - 更多配置选项可以在 官方文档 中找到。

3. 使用rustfmt格式化代码

    - 对整个目录中的所有rust代码格式化，需在项目根目录下运行如下命令：
        ```bash
        cargo fmt
        ```
    - 如果只对某个文件进行格式化，则运行如下命令：
        ```bash
        rustfmt src/lib.rs
        ```
    - 如果只想检查代码格式是否符合规范，而不进行实际格式化操作，则可以运行如下命令：
        ```bash
        cargo fmt -- --check
        ```
